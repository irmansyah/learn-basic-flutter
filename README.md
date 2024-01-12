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

### Simple Project
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







