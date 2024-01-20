# Flutter Rest API using DIO


![] (https://pub.dev/packages/dio)


### Dio Initial

```yaml
# pubspec.yaml

dependencies:
  flutter:
    sdk: flutter

  dio: ^5.4.0
```

```dart
import 'package:dio/dio.dart';

final dio = Dio();

void getHttp() async {
  final response = await dio.get('https://test.com');
  print(response);
}
```

### Dio Get data on tap

```dart
import 'package:flutter/material.dart';
import 'package:dio/dio.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  Dio dio = Dio();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Dio Tutorial'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            fetchData();
          },
          child: Text('Fetch Data'),
        ),
      ),
    );
  }

  void fetchData() async {
    try {
      // Make a GET request to a sample API
      Response response = await dio.get('https://jsonplaceholder.typicode.com/posts/1');

      // Print the response data
      print('Response Data: ${response.data}');
      
      // You can now handle the response data as needed
    } catch (error) {
      // Handle error
      print('Error: $error');
    }
  }
}
```

### Dio Get data and put it into ListView

```dart
class Post {
  final int id;
  final String title;
  final String body;

  Post({required this.id, required this.title, required this.body});

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      id: json['id'],
      title: json['title'],
      body: json['body'],
    );
  }
}
```

```dart
import 'package:dio/dio.dart';

class ApiService {
  final Dio _dio = Dio();

  final String baseUrl;

  ApiService(this.baseUrl);

  Future<List<Post>> getPosts() async {
    try {
      final response = await _dio.get('$baseUrl/posts');
      if (response.statusCode == 200) {
        final List<dynamic> data = response.data;
        return data.map((json) => Post.fromJson(json)).toList();
      } else {
        throw Exception('Failed to load data');
      }
    } catch (e) {
      throw Exception('Error: $e');
    }
  }
}
```

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final ApiService apiService = ApiService('https://jsonplaceholder.typicode.com');

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Dio GET with Model'),
        ),
        body: FutureBuilder(
          future: apiService.getPosts(),
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return CircularProgressIndicator();
            } else if (snapshot.hasError) {
              return Text('Error: ${snapshot.error}');
            } else {
              List<Post> posts = snapshot.data as List<Post>;
              return ListView.builder(
                itemCount: posts.length,
                itemBuilder: (context, index) {
                  return ListTile(
                    title: Text(posts[index].title),
                    subtitle: Text(posts[index].body),
                  );
                },
              );
            }
          },
        ),
      ),
    );
  }
}
```
