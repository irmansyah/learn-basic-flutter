# Flutter State Managemnet and Architecture


![] (https://pub.dev/packages/flutter_bloc)


### Organize project

```bash
 lib
     data
         models
            user_list_model.dart
         entities
            user_list_entity.dart
         data_provider
             remote
                app_service.dart
             local
                local_service.dart
         repositories
            app_repository.dart
            auth_repository.dart

     bloc
        user_list
            user_list_bloc.dart
            user_list_state.dart
            user_list_event.dart

     ui
         page
            user_list_page.dart
         widget
            user_list_widget.dart
```


### Bloc

```yaml
# pubspec.yaml

dependencies:
  flutter:
    sdk: flutter

  flutter_bloc: ^8.1.3
```

```dart
class CounterCubit extends Cubit<int> {
  CounterCubit() : super(0);

  void increment() => emit(state + 1);
  void decrement() => emit(state - 1);
}
```

```dart
class CounterPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Counter')),
      body: BlocBuilder<CounterCubit, int>(
        builder: (context, count) => Center(child: Text('$count')),
      ),
      floatingActionButton: Column(
        crossAxisAlignment: CrossAxisAlignment.end,
        mainAxisAlignment: MainAxisAlignment.end,
        children: <Widget>[
          FloatingActionButton(
            child: const Icon(Icons.add),
            onPressed: () => context.read<CounterCubit>().increment(),
          ),
          const SizedBox(height: 4),
          FloatingActionButton(
            child: const Icon(Icons.remove),
            onPressed: () => context.read<CounterCubit>().decrement(),
          ),
        ],
      ),
    );
  }
}
```


### Bloc with state

```dart
// user_list_bloc.dart
class UserListBloc extends Bloc<UserListEvent, UserListState> {
  final AppRepository repository;

  static const int _pageLimit = 5;

  UserListBloc({
    required this.repository,
  }) : super(UserListLoading()) {

    on<GetUserList>((event, emit) async {
      try {
        //await Future.delayed(const Duration(seconds: 5));
        emit(UserListLoading());
        final data = await repository.getUserList(
          event.pageKey,
          false,
          _pageLimit,
        );
        final isLastPage = data.isLastPage;
        if (isLastPage) {
          emit(UserListLastPageLoaded(data: data));
        } else {
          final nextPageKey = event.pageKey + 1;
          emit(UserListLoaded(data: data, nextPageKey: nextPageKey));
        }
      } on DioException catch (e, stackTrace) {
        debugPrint(stackTrace.toString());
        emit(UserListError(code: e.statusCode, message: e.message));
      } catch (e, stackTrace) {
        debugPrint(stackTrace.toString());
      }
    });
  }
}
```

```dart
// user_list_state.dart
import 'package:equatable/equatable.dart';

abstract class UserListState extends Equatable {
  const UserListState();

  @override
  List<Object> get props => [];
}

class UserListEmpty extends UserListState {}

class UserListInitial extends UserListState {}

class UserListLoading extends UserListState {}

class UserListLoaded extends UserListState {
  final UserListData data;
  final int nextPageKey;

  const UserListLoaded({
    required this.data,
    required this.nextPageKey,
  });

  @override
  List<Object> get props => [data, nextPageKey];
}

class UserListLastPageLoaded extends UserListState {
  final UserListData data;

  const UserListLastPageLoaded({
    required this.data,
  });

  @override
  List<Object> get props => [data];
}

class UserListError extends UserListState {
  final String message;
  final int code;

  const UserListError({
    required this.message, 
    required this.code
  });

  @override
  List<Object> get props => [message, code];
}
```

```dart
// user_list_event.dart
import 'package:equatable/equatable.dart';

abstract class UserListEvent extends Equatable {
  const UserListEvent();

  @override
  List<Object> get props => [];
}

class GetUserList extends UserListEvent {
  final int pageKey;

  const GetUserList({
    required this.pageKey,
  });

  @override
  List<Object> get props => [pageKey];
}
```

```dart
//app_repository.dart
class AppRepository {
  final AppService appService;
  final LocalService localService;

  AppRepository({
    required this.appService,
    required this.localService,
  });

  Future<UserList> getContentUserList(
      int page, bool isProcess, int limit) async {
    UserListResponse response =
        await appService.fetchContentUserList(page, isProcess, limit);
    return UserList(
      isLastPage: response.currentPage == response.totalPages,
      datas: response.datas!
	  .map((data) => UserData(
		id: data.id,
		title: data.title,
      )).toList(),
    );
  }

}
```

```dart
//app_service.dart
class AppService {

  Future<BookListResponse> fetchContentBookList(int page, int limit) async {
    final res = await dio.get(
      'users?page=$page&limit=$limit',
    );
    if (res.statusCode != 200) {
      throw FailedException(res.data['errorMessage'], res.data['errorCode']);
    }
    return BookListResponse.fromJson(res.data);
  }
}
```

```dart
//home_page.dart
class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {

  final PagingController<int, UserData> _pagingUserController =
      PagingController(firstPageKey: 1);

  void _setListPaging() {
    _pagingUserController.addPageRequestListener((pageKey) {
      _loadUserList(pageKey);
    });
  }

  void _loadUserList(int pageKey) =>
      context.read<UserListBloc>().add(GetUserList(pageKey: pageKey));

  @override
  void initState() {
    _setListPaging();
    super.initState();
  }

  @override
  void dispose() {
    _pagingUserController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) => 
    Scaffold(
      backgroundColor: AppTheme.scaffold,
      appBar: AppBar(
        title: Text('User List'), 
        backgroundColor: AppTheme.lightLightGrey,
      ),
      body: _appBody(),
    );

  Widget _appBody() => Padding(
    padding: const EdgeInsets.symmetric(horizontal: 16.0),
    child: BlocListener<UserListBloc, UserListState>(
        listener: (context, state) {
    	if (state is UserListLastPageLoaded) {
    	  _pagingUserController
    	      .appendLastPage(state.data.datas);
    	} else if (state is UserListLoaded) {
    	  _pagingUserController.appendPage(
    	      state.data.datas, state.nextPageKey);
    	} else if (state is UserListError) {
    	  _pagingUserController.error = state.message;
    	}
        },
        child: RefreshIndicator(
    	onRefresh: () => Future.sync(
    	  () => _pagingUserController.refresh(),
    	),
    	child: Builder(
    	  builder: (context) {
    	    return PagedListView<int, UserData>(
    	      pagingController: _pagingUserController,
    	      builderDelegate: PagedChildBuilderDelegate<UserData>(
    	        itemBuilder: (context, item, index) => 
    		    _userListItem(context, item),
    	        firstPageProgressIndicatorBuilder: (_) =>
    		    const Center(child: CircularProgressIndicator()),
    	        newPageProgressIndicatorBuilder: (_) =>
    		    const Center(child: CircularProgressIndicator()),
    	        noItemsFoundIndicatorBuilder: (_) => Center(
    	    	child: Text(Strings.empty.tr(),
    	    	    style: AppTheme.text1.darkGrey.bold)),
    	      ),
    	    );
    	  }
    	),
        )),
  );

  Widget _userListItem(BuildContext context, UserData item) {
    return Card(
      child: Padding(
	padding: const EdgeInsets.symmetric(vertical: 8.0, horizontal: 16.0),
        child: Row(
	  children: [
	    CustomImageWidget(
	      width: 50,
	      height: 80,
	      rounded: 4,
	      imageUrl: item.coverImageUrl
	    ),
	    const SizedBox(width: 8.0),
	    Expanded(
	      child: Column(
	        crossAxisAlignment: CrossAxisAlignment.start,
	        children: [
		  Text(item.title, style: AppTheme.text2.grey.bold),
		  const SizedBox(height: 4.0),
		  Text(item.authorName, style: AppTheme.text3.grey),
		  const SizedBox(height: 4.0),
		  Text(item.description, style: AppTheme.subText1.grey),
	        ],
	      ),
	    ),
	  ],
        ),
      ),
    );
  }
}
```
