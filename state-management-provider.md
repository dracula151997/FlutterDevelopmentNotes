To manage state using the Provider package in Flutter, you can follow these steps:

1. Define a model class that extends `ChangeNotifier`. This class will hold the state of your application.
2. Wrap your widget tree with `ChangeNotifierProvider`. This will provide the instance of your model to the widgets that are below it in the widget tree.
3. Use `Provider.of<T>(context)` or `context.watch<T>()` to access the model from your widgets and rebuild them when the model changes.

Here's an example of how you can do it:

First, define your model class. This class will hold your state and notify its listeners when it changes.

```dart
import 'package:flutter/foundation.dart';

class CounterModel extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}
```

Then, provide this model to your widgets using `ChangeNotifierProvider`.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'counter_model.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => CounterModel(),
      child: MaterialApp(
        theme: AppTheme.lightTheme,
        darkTheme: AppTheme.darkTheme,
        themeMode: ThemeMode.system,
        initialRoute: "/root",
        routes: {
          "/root": (context) => const RootBottomNavigation(),
          "/screen_one": (context) => const ScreenOne(),
          "/screen_two": (context) => const ScreenTwo(),
        },
        home: const RootBottomNavigation(),
      ),
    );
  }
}
```

Finally, use `Provider.of<T>(context)` or `context.watch<T>()` to access the model from your widgets and rebuild them when the model changes.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'counter_model.dart';

class ScreenOne extends StatelessWidget {
  const ScreenOne({super.key});

  @override
  Widget build(BuildContext context) {
    var counterModel = Provider.of<CounterModel>(context);
    return Scaffold(
      appBar: AppBar(
        title: const Text("Screen One"),
        backgroundColor: Colors.green,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('You have pushed the button this many times:'),
            Text(
              '${counterModel.count}',
              style: Theme.of(context).textTheme.headline4,
            ),
            TextButton(
              child: const Text("Increment"),
              onPressed: counterModel.increment,
            ),
            TextButton(
              child: const Text("Go back"),
              onPressed: () {
                Navigator.popUntil(context, (route) => route.isFirst);
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, `ScreenOne` will rebuild every time `CounterModel` changes because it's listening to it using `Provider.of<CounterModel>(context)`. When the "Increment" button is pressed, the `increment` method of `CounterModel` is called, which increments the count and notifies its listeners.

### Difference between `Provider.of<T>(context)` and `Consumer<T>`
In Flutter, both `Provider.of<T>(context)` and `Consumer<T>` are used to access data from a provider. However, they are used in slightly different scenarios and have different behaviors.

1. `Provider.of<T>(context)`: This is a direct way to access the data. It will cause the widget to rebuild whenever the provider updates. It's a simpler approach and can be used when the data is needed in the widget's build method.

```dart
final counterModel = Provider.of<CounterModel>(context);
```

2. `Consumer<T>`: This is a widget that rebuilds when the `ChangeNotifier` changes. It's more flexible than `Provider.of<T>` because it allows you to rebuild only a specific part of the widget tree. This can be more efficient if only a small part of the widget tree depends on the provided value.

```dart
Consumer<CounterModel>(
  builder: (context, counterModel, child) {
    return Text('${counterModel.count}');
  },
)
```

In the `Consumer<T>` example, only the `Text` widget will rebuild when `CounterModel` changes. This can be more efficient if the rest of the widget tree is complex and doesn't need to change when `CounterModel` changes.

In summary, use `Provider.of<T>(context)` when you need the data in the widget's build method and don't mind the whole widget rebuilding when the data changes. Use `Consumer<T>` when you want more control over what part of the widget tree rebuilds.
