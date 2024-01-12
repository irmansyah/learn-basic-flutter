# Flutter Basic Widget


![] (https://docs.flutter.dev/ui/widgets/basics)
   - Container
   - SizedBox
   - Text
   - Center
   - Icon
   - Image
   - Button
   - Row
   - Column
   - Scaffold
   - AppBar
   - FloatingActionButton


### Text
```dart
Text('Hello World'),
```

### Center
```dart
Center(
  child: Text('Hello World'),
),
```

### Container
```dart
Container(
  padding: const EdgeInsets.all(8.0),
  color: Colors.blue[600],
  child: Text('Hello World'),
),
```

### SizedBox
```dart
SizedBox(
  width: 200,
  height: 200,
  child: Text('Hello World'),
),
```

### Icon
```dart
Icon(
  Icons.favorite,
  color: Colors.green,
  size: 30.0,
),
```

### Image
```dart
Image(
  image: NetworkImage('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl.jpg'),
),
```

### Button
```dart
ElevatedButton(
  style: style,
  child: const Text('Enabled'),
  onPressed: () {},
),
```

### Row
```dart
Row(
  children: <Widget>[
    Expanded(
      child: Text('Deliver features faster', textAlign: TextAlign.center),
    ),
    Expanded(
      child: Text('Craft beautiful UIs', textAlign: TextAlign.center),
    ),
    Expanded(
      child: FittedBox(
        child: FlutterLogo(),
      ),
    ),
  ],
),
```

### Row
```dart
Column(
  children: <Widget>[
    Text('Deliver features faster'),
    Text('Craft beautiful UIs'),
    Expanded(
      child: FittedBox(
        child: FlutterLogo(),
      ),
    ),
  ],
),
```

### Scaffold
```dart
Scaffold(
  body: Center(child: Text('You have pressed the button $_count times.')),
)
```

### AppBar
```dart
AppBar(
  title: const Text('Sample Code'),
),
```

### Floating Action Button
```dart
FloatingActionButton(
  tooltip: 'Increment Counter',
  child: const Icon(Icons.add),
  onPressed: () => setState(() => _count++),
),
```

### Simple Scaffold
```dart
Scaffold(
  appBar: AppBar(
    title: const Text('Sample Code'),
  ),
  body: Center(child: Text('You have pressed the button $_count times.')),
  floatingActionButton: FloatingActionButton(
    tooltip: 'Increment Counter',
    child: const Icon(Icons.add),
    onPressed: () => setState(() => _count++),
  ),
)
```

### Simple Project
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            Center(
              child: Text(
                '$_counter',
                style: Theme.of(context).textTheme.headlineMedium,
              ),
            ),
            const Image(
              image: NetworkImage('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl.jpg'),
            )
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}
```
