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

### Column
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

### Profile Page by Adri Bagas



```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.white),
        useMaterial3: true,
      ),
      debugShowCheckedModeBanner: false,
      home: const SecondDayTestPage(),
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
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Container(
          padding: const EdgeInsets.all(8),
          child: const Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Icon(
                Icons.arrow_back_ios_new,
                size: 24,
                color: Colors.black,
              ),
              Icon(
                Icons.notifications,
                size: 24,
                color: Colors.black,
              ),
            ],
          ),
        ),
      ),
      body: Center(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Container(
              height: 200,
              width: 200,
              decoration: const BoxDecoration(
                color: Colors.white,
                borderRadius: BorderRadius.all(Radius.circular(120)),
              ),
              padding: const EdgeInsets.all(16),
              child: const ClipRRect(
                borderRadius: BorderRadius.all(Radius.circular(120)),
                child: Image(
                  image: NetworkImage(
                    'https://flutter.github.io/assets-for-api-docs/assets/widgets/owl.jpg',
                  ),
                ),
              ),
            ),
            SizedBox(
              height: 100,
              child: Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Container(
                    height: 50,
                    width: 50,
                    decoration: BoxDecoration(
                      color: Colors.blue[900],
                      shape: BoxShape.circle,
                    ),
                    child: const Icon(
                      Icons.facebook,
                      color: Colors.white,
                      size: 24,
                    ),
                  ),
                  const SizedBox(
                    width: 12,
                  ),
                  Container(
                    height: 50,
                    width: 50,
                    decoration: const BoxDecoration(
                      color: Color.fromARGB(255, 208, 52, 4),
                      shape: BoxShape.circle,
                    ),
                    child: const Icon(
                      Icons.g_mobiledata_outlined,
                      color: Colors.white,
                      size: 24,
                    ),
                  ),
                  const SizedBox(
                    width: 12,
                  ),
                  Container(
                    height: 50,
                    width: 50,
                    decoration: BoxDecoration(
                      color: Colors.lightBlue[400],
                      shape: BoxShape.circle,
                    ),
                    child: const Icon(
                      Icons.blender_outlined,
                      color: Colors.white,
                      size: 24,
                    ),
                  ),
                  const SizedBox(
                    width: 12,
                  ),
                  Container(
                    height: 50,
                    width: 50,
                    decoration: BoxDecoration(
                      color: Colors.lightBlue[700],
                      shape: BoxShape.circle,
                    ),
                    child: const Icon(
                      Icons.interests_sharp,
                      color: Colors.white,
                      size: 24,
                    ),
                  ),
                ],
              ),
            ),
            const Text(
              "Adri Bagas",
              style: TextStyle(
                fontWeight: FontWeight.bold,
                fontSize: 32,
              ),
            ),
            Container(
              margin: const EdgeInsets.symmetric(
                horizontal: 48,
              ),
              child: const Text(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam.",
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                  fontSize: 14,
                ),
                textAlign: TextAlign.center,
              ),
            ),
            Expanded(
              child: Column(
                children: [
                  Container(
                    decoration: BoxDecoration(
                      borderRadius: const BorderRadius.all(Radius.circular(90)),
                      color: Colors.grey[200],
                    ),
                    padding: const EdgeInsets.symmetric(
                      horizontal: 20.0,
                      vertical: 16,
                    ),
                    margin: const EdgeInsets.all(8.0),
                    child: const Row(
                      children: [
                        Icon(
                          Icons.privacy_tip_outlined,
                          color: Colors.black,
                          size: 24,
                        ),
                        Spacer(
                          flex: 1,
                        ),
                        Text(
                          "Privacy",
                          style: TextStyle(
                            color: Colors.black,
                            fontSize: 14,
                          ),
                        ),
                        Spacer(
                          flex: 16,
                        ),
                        Icon(
                          Icons.arrow_forward_ios,
                          color: Colors.black,
                          size: 24,
                        ),
                      ],
                    ),
                  ),
                  Container(
                    decoration: BoxDecoration(
                      borderRadius: const BorderRadius.all(Radius.circular(90)),
                      color: Colors.grey[200],
                    ),
                    padding: const EdgeInsets.symmetric(
                      horizontal: 20.0,
                      vertical: 16,
                    ),
                    margin: const EdgeInsets.all(8.0),
                    child: const Row(
                      children: [
                        Icon(
                          Icons.add_chart_outlined,
                          color: Colors.black,
                          size: 24,
                        ),
                        Spacer(
                          flex: 1,
                        ),
                        Text(
                          "Something Menu",
                          style: TextStyle(
                            color: Colors.black,
                            fontSize: 14,
                          ),
                        ),
                        Spacer(
                          flex: 16,
                        ),
                        Icon(
                          Icons.arrow_forward_ios,
                          color: Colors.black,
                          size: 24,
                        ),
                      ],
                    ),
                  ),
                  Container(
                    decoration: BoxDecoration(
                      borderRadius: const BorderRadius.all(Radius.circular(90)),
                      color: Colors.grey[200],
                    ),
                    padding: const EdgeInsets.symmetric(
                      horizontal: 20.0,
                      vertical: 16,
                    ),
                    margin: const EdgeInsets.all(8.0),
                    child: const Row(
                      children: [
                        Icon(
                          Icons.add_circle,
                          color: Colors.black,
                          size: 24,
                        ),
                        Spacer(
                          flex: 1,
                        ),
                        Text(
                          "Add Something",
                          style: TextStyle(
                            color: Colors.black,
                            fontSize: 14,
                          ),
                        ),
                        Spacer(
                          flex: 16,
                        ),
                        Icon(
                          Icons.arrow_forward_ios,
                          color: Colors.black,
                          size: 24,
                        ),
                      ],
                    ),
                  ),
                  Container(
                    decoration: BoxDecoration(
                      borderRadius: const BorderRadius.all(Radius.circular(90)),
                      color: Colors.grey[200],
                    ),
                    padding: const EdgeInsets.symmetric(
                      horizontal: 20.0,
                      vertical: 16,
                    ),
                    margin: const EdgeInsets.all(8.0),
                    child: const Row(
                      children: [
                        Icon(
                          Icons.access_alarm,
                          color: Colors.black,
                          size: 24,
                        ),
                        Spacer(
                          flex: 1,
                        ),
                        Text(
                          "Your Time",
                          style: TextStyle(
                            color: Colors.black,
                            fontSize: 14,
                          ),
                        ),
                        Spacer(
                          flex: 16,
                        ),
                        Icon(
                          Icons.arrow_forward_ios,
                          color: Colors.black,
                          size: 24,
                        ),
                      ],
                    ),
                  ),
                  Container(
                    decoration: BoxDecoration(
                      borderRadius: const BorderRadius.all(Radius.circular(90)),
                      color: Colors.grey[200],
                    ),
                    padding: const EdgeInsets.symmetric(
                      horizontal: 20.0,
                      vertical: 16,
                    ),
                    margin: const EdgeInsets.all(8.0),
                    child: const Row(
                      children: [
                        Icon(
                          Icons.logout,
                          color: Colors.black,
                          size: 24,
                        ),
                        Spacer(
                          flex: 1,
                        ),
                        Text(
                          "Log Out",
                          style: TextStyle(
                            color: Colors.black,
                            fontSize: 14,
                          ),
                        ),
                        Spacer(
                          flex: 16,
                        ),
                        Icon(
                          Icons.arrow_forward_ios,
                          color: Colors.black,
                          size: 24,
                        ),
                      ],
                    ),
                  ),
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
