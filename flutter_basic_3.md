# Flutter Mutiple Screen


![] (https://docs.flutter.dev/ui/navigation)
   - Navigation and routes

![] (https://pub.dev/)
   - External library



### Navigation to New Screen
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const SecondRoute()),
);
```

### Navigation to New Screen with Button onPressed
```dart
ElevatedButton(
  child: const Text('Open route'),
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => const SecondRoute()),
    );
  },
)
```

### Navigation with Routes
```dart
@override
Widget build(BuildContext context) {
  return MaterialApp(
    routes: {
      '/': (context) => HomeScreen(),
      '/details': (context) => DetailScreen(),
    },
  );
}
```

### Navigation with Routes send data to next Screen/Page

```dart
// main.dart

import 'package:flutter/material.dart';
import 'screens/home_screen.dart';
import 'screens/details_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen(),
        '/details': (context) => DetailsScreen(),
      },
    );
  }
}
```

```dart
// home_screen.dart

import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate to the Details Screen and pass data
            Navigator.pushNamed(
              context,
              '/details',
              arguments: 'Hello from Home Screen!',
            );
          },
          child: Text('Go to Details Screen'),
        ),
      ),
    );
  }
}
```

```dart
// detail_screen.dart

import 'package:flutter/material.dart';

class DetailsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Extract the data passed from the Home Screen
    final String data = ModalRoute.of(context).settings.arguments;

    return Scaffold(
      appBar: AppBar(title: Text('Details Screen')),
      body: Center(
        child: Text('Received Data: $data'),
      ),
    );
  }
}
```

### Add External packages

```bash
flutter pub add <package_name> 
```

```yaml
# pubspec.yaml

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.6
  carousel_slider: ^4.2.1
  # add new external library here
```

### Add External packages Carousel Slider

![] (https://pub.dev/packages/carousel_slider)

```dart
CarouselSlider(
  options: CarouselOptions(height: 400.0),
  items: [1,2,3,4,5].map((i) {
    return Builder(
      builder: (BuildContext context) {
        return Container(
          width: MediaQuery.of(context).size.width,
          margin: EdgeInsets.symmetric(horizontal: 5.0),
          decoration: BoxDecoration(
            color: Colors.amber
          ),
          child: Text('text $i', style: TextStyle(fontSize: 16.0),)
        );
      },
    );
  }).toList(),
)
```
