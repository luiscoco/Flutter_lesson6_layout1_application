# Flutter: common architectural templates

Learning Flutter involves understanding not only the UI framework but also the architectural patterns that can help manage your app's complexity as it grows

Here are some common architectural templates you can consider when starting with Flutter:

## 1. Simple App (No Architecture)

For very simple applications, you might start with no specific architecture, just a single main file (**main.dart**)

**main.dart**

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Simple App'),
        ),
        body: Center(
          child: Text('Hello, world!'),
        ),
      ),
    );
  }
}
```

## 2. 


## 3. 
