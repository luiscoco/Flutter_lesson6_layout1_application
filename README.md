# Flutter: basic layout sample

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

## 2. Buiding a layout

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
      debugShowCheckedModeBanner: false,
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Flutter layout demo'),
      ),
      body: ListView(
        children: [
          Image.network(
            'https://media.myswitzerland.com/image/fetch/w_760,h_760,c_fill,g_auto,f_auto,q_auto,e_trim/https%3A%2F%2Fwww.myswitzerland.com%2F-%2Fmedia%2Fst%2Fgadmin%2Fimages%2Flandscapes%2Fsummer%2Flandscapes%2Fstn4738_52157.jpg', // Replace with a valid image URL
            height: 240,
            fit: BoxFit.cover,
          ),
          Padding(
            padding: const EdgeInsets.all(16.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Row(
                  children: [
                    Expanded(
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            'Oeschinen Lake Campground',
                            style: TextStyle(
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          SizedBox(height: 8.0),
                          Text(
                            'Kandersteg, Switzerland',
                            style: TextStyle(
                              color: Colors.grey[500],
                            ),
                          ),
                        ],
                      ),
                    ),
                    Icon(
                      Icons.star,
                      color: Colors.red[500],
                    ),
                    Text('41'),
                  ],
                ),
                SizedBox(height: 16.0),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    _buildButtonColumn(context, Icons.call, 'CALL'),
                    _buildButtonColumn(context, Icons.near_me, 'ROUTE'),
                    _buildButtonColumn(context, Icons.share, 'SHARE'),
                  ],
                ),
                SizedBox(height: 16.0),
                Text(
                  'Lake Oeschinen lies at the foot of the Blüemlisalp in the Bernese Alps. Situated 1,578 meters above sea level, it is one of the larger Alpine Lakes. A gondola ride from Kandersteg, followed by a half-hour walk through pastures and pine forest, leads you to the lake, which warms to 20 degrees Celsius in the summer. Activities enjoyed here include rowing, and riding the summer toboggan run.',
                  softWrap: true,
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Column _buildButtonColumn(BuildContext context, IconData icon, String label) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        IconButton(
          icon: Icon(icon, color: Colors.blue[500]),
          onPressed: () {
            if (label == 'CALL') {
              _showDialog(context);
            }
          },
        ),
        Container(
          margin: const EdgeInsets.only(top: 8.0),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12.0,
              fontWeight: FontWeight.w400,
              color: Colors.blue[500],
            ),
          ),
        ),
      ],
    );
  }

  void _showDialog(BuildContext context) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Call Button Pressed'),
          content: Text('You have pressed on the Call button'),
          actions: [
            TextButton(
              child: Text('OK'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }
}
```

## 3. How to Navigate between Pages

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Flutter layout demo'),
      ),
      body: ListView(
        children: [
          Image.network(
            'https://media.myswitzerland.com/image/fetch/w_1760,h_520,c_limit,f_auto,q_auto,e_sharpen:50/https%3A%2F%2Fwww.myswitzerland.com%2F-%2Fmedia%2Fdam%2Fresources%2Fexperience%2Fs%2Ft%2Fstockhorn%20and%20striking%20horn%2Fimages%20summer%2F51483_32001800.jpeg', // Replace with a valid image URL
            height: 240,
            fit: BoxFit.cover,
          ),
          Padding(
            padding: const EdgeInsets.all(16.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Row(
                  children: [
                    Expanded(
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            'Oeschinen Lake Campground',
                            style: TextStyle(
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          SizedBox(height: 8.0),
                          Text(
                            'Kandersteg, Switzerland',
                            style: TextStyle(
                              color: Colors.grey[500],
                            ),
                          ),
                        ],
                      ),
                    ),
                    Icon(
                      Icons.star,
                      color: Colors.red[500],
                    ),
                    Text('41'),
                  ],
                ),
                SizedBox(height: 16.0),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    _buildButtonColumn(context, Icons.call, 'CALL'),
                    _buildButtonColumn(context, Icons.near_me, 'ROUTE'),
                    _buildButtonColumn(context, Icons.share, 'SHARE'),
                  ],
                ),
                SizedBox(height: 16.0),
                Text(
                  'Lake Oeschinen lies at the foot of the Blüemlisalp in the Bernese Alps. Situated 1,578 meters above sea level, it is one of the larger Alpine Lakes. A gondola ride from Kandersteg, followed by a half-hour walk through pastures and pine forest, leads you to the lake, which warms to 20 degrees Celsius in the summer. Activities enjoyed here include rowing, and riding the summer toboggan run.',
                  softWrap: true,
                ),
                SizedBox(height: 16.0),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    ElevatedButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute(builder: (context) => PageOne()),
                        );
                      },
                      child: Text('Page 1'),
                    ),
                    ElevatedButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute(builder: (context) => PageTwo()),
                        );
                      },
                      child: Text('Page 2'),
                    ),
                  ],
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Column _buildButtonColumn(BuildContext context, IconData icon, String label) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        IconButton(
          icon: Icon(icon, color: Colors.blue[500]),
          onPressed: () {
            if (label == 'CALL') {
              _showDialog(context);
            }
          },
        ),
        Container(
          margin: const EdgeInsets.only(top: 8.0),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12.0,
              fontWeight: FontWeight.w400,
              color: Colors.blue[500],
            ),
          ),
        ),
      ],
    );
  }

  void _showDialog(BuildContext context) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Call Button Pressed'),
          content: Text('You have pressed on the Call button'),
          actions: [
            TextButton(
              child: Text('OK'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }
}

class PageOne extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Page One'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('This is Page One'),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
              },
              child: Text('Back to Home'),
            ),
          ],
        ),
      ),
    );
  }
}

class PageTwo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Page Two'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('This is Page Two'),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
              },
              child: Text('Back to Home'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## 4. We added three Cards in Page 2

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Flutter layout demo'),
      ),
      body: ListView(
        children: [
          Image.network(
            'https://media.myswitzerland.com/image/fetch/w_1760,h_520,c_limit,f_auto,q_auto,e_sharpen:50/https%3A%2F%2Fwww.myswitzerland.com%2F-%2Fmedia%2Fdam%2Fresources%2Fexperience%2Fs%2Ft%2Fstockhorn%20and%20striking%20horn%2Fimages%20summer%2F53876_32001800.jpeg', // Replace with a valid image URL
            height: 240,
            fit: BoxFit.cover,
          ),
          Padding(
            padding: const EdgeInsets.all(16.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Row(
                  children: [
                    Expanded(
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            'Oeschinen Lake Campground',
                            style: TextStyle(
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          SizedBox(height: 8.0),
                          Text(
                            'Kandersteg, Switzerland',
                            style: TextStyle(
                              color: Colors.grey[500],
                            ),
                          ),
                        ],
                      ),
                    ),
                    Icon(
                      Icons.star,
                      color: Colors.red[500],
                    ),
                    Text('41'),
                  ],
                ),
                SizedBox(height: 16.0),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    _buildButtonColumn(context, Icons.call, 'CALL'),
                    _buildButtonColumn(context, Icons.near_me, 'ROUTE'),
                    _buildButtonColumn(context, Icons.share, 'SHARE'),
                  ],
                ),
                SizedBox(height: 16.0),
                Text(
                  'Lake Oeschinen lies at the foot of the Blüemlisalp in the Bernese Alps. Situated 1,578 meters above sea level, it is one of the larger Alpine Lakes. A gondola ride from Kandersteg, followed by a half-hour walk through pastures and pine forest, leads you to the lake, which warms to 20 degrees Celsius in the summer. Activities enjoyed here include rowing, and riding the summer toboggan run.',
                  softWrap: true,
                ),
                SizedBox(height: 16.0),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    ElevatedButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute(builder: (context) => PageOne()),
                        );
                      },
                      child: Text('Page 1'),
                    ),
                    ElevatedButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute(builder: (context) => PageTwo()),
                        );
                      },
                      child: Text('Page 2'),
                    ),
                  ],
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Column _buildButtonColumn(BuildContext context, IconData icon, String label) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        IconButton(
          icon: Icon(icon, color: Colors.blue[500]),
          onPressed: () {
            if (label == 'CALL') {
              _showDialog(context, 'You have pressed on the Call button');
            }
          },
        ),
        Container(
          margin: const EdgeInsets.only(top: 8.0),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12.0,
              fontWeight: FontWeight.w400,
              color: Colors.blue[500],
            ),
          ),
        ),
      ],
    );
  }

  void _showDialog(BuildContext context, String message) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Button Pressed'),
          content: Text(message),
          actions: [
            TextButton(
              child: Text('OK'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }
}

class PageOne extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Page One'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('This is Page One'),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
              },
              child: Text('Back to Home'),
            ),
          ],
        ),
      ),
    );
  }
}

class PageTwo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Page Two'),
      ),
      body: ListView(
        padding: const EdgeInsets.all(8.0),
        children: [
          _buildCard(
            context,
            'Card Title 0',
            'Card Subtitle 0',
            'https://media.myswitzerland.com/image/fetch/w_1760,h_520,c_limit,f_auto,q_auto,e_sharpen:50/https%3A%2F%2Fwww.myswitzerland.com%2F-%2Fmedia%2Fdam%2Fresources%2Fexperience%2Fs%2Ft%2Fstockhorn%20and%20striking%20horn%2Fimages%20summer%2F53870_32001800.jpeg',
            0,
          ),
          _buildCard(
            context,
            'Card Title 1',
            'Card Subtitle 1',
            'https://media.myswitzerland.com/image/fetch/w_1760,h_520,c_limit,f_auto,q_auto,e_sharpen:50/https%3A%2F%2Fwww.myswitzerland.com%2F-%2Fmedia%2Fdam%2Fresources%2Fexperience%2Fs%2Ft%2Fstockhorn%20and%20striking%20horn%2Fimages%20summer%2F53874_32001800.jpeg',
            1,
          ),
          _buildCard(
            context,
            'Card Title 2',
            'Card Subtitle 2',
            'https://media.myswitzerland.com/image/fetch/w_1760,h_520,c_limit,f_auto,q_auto,e_sharpen:50/https%3A%2F%2Fwww.myswitzerland.com%2F-%2Fmedia%2Fdam%2Fresources%2Fexperience%2Fs%2Ft%2Fstockhorn%20and%20striking%20horn%2Fimages%20winter%2F49435_32001800_2.jpeg',
            2,
          ),
        ],
      ),
    );
  }

  Widget _buildCard(BuildContext context, String title, String subtitle, String imageUrl, int index) {
    return Card(
      child: Column(
        mainAxisSize: MainAxisSize.min,
        children: <Widget>[
          ListTile(
            leading: Image.network(
              imageUrl,
              width: 50,
              height: 50,
              fit: BoxFit.cover,
            ),
            title: Text(title),
            subtitle: Text(subtitle),
          ),
          ButtonBar(
            children: <Widget>[
              TextButton(
                child: Text('BUTTON 1'),
                onPressed: () {
                  _showDialog(context, 'You pressed Button 1 on card $index');
                },
              ),
              TextButton(
                child: Text('BUTTON 2'),
                onPressed: () {
                  _showDialog(context, 'You pressed Button 2 on card $index');
                },
              ),
            ],
          ),
        ],
      ),
    );
  }

  void _showDialog(BuildContext context, String message) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Button Pressed'),
          content: Text(message),
          actions: [
            TextButton(
              child: Text('OK'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }
}
```
