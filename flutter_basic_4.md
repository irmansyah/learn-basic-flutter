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
