### How to navigate to another screen in Flutter?
In Flutter, you can navigate to another screen using the `Navigator` class. Here's a step-by-step guide:

1. First, you need to define the new screen. You've already done this with `ScreenOne` in `lib/presentation/navigation_example/screen_one.dart`.

2. Next, you need to trigger the navigation. This is typically done in response to a user action, such as pressing a button.

3. To navigate to the new screen, you use the `Navigator.push` method, which pushes a `Route` onto the navigation stack. In this case, the `Route` is a `MaterialPageRoute`, which transitions to the new screen using a platform-specific animation.

Here's an example of how you can navigate to `ScreenOne` when the `CustomButton` in `lib/presentation/widget_examples/widget_examples_screen.dart` is pressed:

```dart
CustomButton(
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => const ScreenOne()),
    );
  },
  icon: Icons.home,
  color: Colors.red,
  iconColor: Colors.white,
  shape: BoxShape.circle,
),
```

In this code, when the `CustomButton` is pressed, the `onPressed` callback is called, which pushes `ScreenOne` onto the navigation stack. This causes Flutter to build the `ScreenOne` widget and animate it onto the screen.

In addition to the `Navigator.push` method, you can also use named routes for navigation in Flutter. Named routes can make it easier to understand the navigation flow of your app, especially when you have many screens.

Here's how you can define and use named routes:

1. Define the routes in your main app widget. Each route is associated with a string (the route's name) and a builder function that returns the widget to display when the route is navigated to.

```dart
MaterialApp(
  // Start the app with the "/" named route. In this case, the app starts
  // on the FirstScreen widget.
  initialRoute: '/',
  routes: {
    // When navigating to the "/" route, build the FirstScreen widget.
    '/': (context) => const WidgetExamplesScreen(),
    // When navigating to the "/second" route, build the SecondScreen widget.
    '/second': (context) => const ScreenOne(),
  },
)
```

2. Navigate to the second screen using `Navigator.pushNamed`.

```dart
CustomButton(
  onPressed: () {
    Navigator.pushNamed(context, '/second');
  },
  icon: Icons.home,
  color: Colors.red,
  iconColor: Colors.white,
  shape: BoxShape.circle,
),
```

In this code, when the `CustomButton` is pressed, the `onPressed` callback is called, which navigates to the route named '/second'. This causes Flutter to build the `ScreenOne` widget and animate it onto the screen.

### `Navigator.push` vs `Navigator.pushReplacement`
In Flutter, `Navigator.push` and `Navigator.pushReplacement` are two methods used for navigation between screens, but they behave differently.

1. `Navigator.push`: This method is used to navigate to a new screen, adding it on top of the navigation stack. This means the current screen is still in the memory and when you pop from the new screen, you will return to the original screen. Here's an example:

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const ScreenTwo()),
);
```

2. `Navigator.pushReplacement`: This method is used to navigate to a new screen, replacing the current screen in the navigation stack. This means the current screen is removed from memory and when you pop from the new screen, you will not return to the original screen, but to the screen that was active before the original screen. Here's an example:

```dart
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => const ScreenTwo()),
);
```

In summary, use `Navigator.push` when you want to keep the current screen in the navigation stack and return to it later. Use `Navigator.pushReplacement` when you want to completely replace the current screen with a new one and not return to it.

### Named Routes
In Flutter, named routes are a way to define the routes for your application in one place and refer to them by name. This can make your code more maintainable and easier to understand.

Here's how you can define and use named routes:

1. Define the routes in your main app widget. Each route is associated with a string (the route's name) and a builder function that returns the widget to display when the route is navigated to.

```dart
MaterialApp(
  // Start the app with the "/" named route. In this case, the app starts
  // on the FirstScreen widget.
  initialRoute: '/',
  routes: {
    // When navigating to the "/" route, build the FirstScreen widget.
    '/': (context) => const WidgetExamplesScreen(),
    // When navigating to the "/second" route, build the SecondScreen widget.
    '/second': (context) => const ScreenOne(),
  },
)
```

2. Navigate to the second screen using `Navigator.pushNamed`.

```dart
CustomButton(
  onPressed: () {
    Navigator.pushNamed(context, '/second');
  },
  icon: Icons.home,
  color: Colors.red,
  iconColor: Colors.white,
  shape: BoxShape.circle,
),
```

In this code, when the `CustomButton` is pressed, the `onPressed` callback is called, which navigates to the route named '/second'. This causes Flutter to build the `ScreenOne` widget and animate it onto the screen.

### `Navigator.pop` vs `Navigator.popUntil`
In Flutter, `Navigator.pop` and `Navigator.popUntil` are two methods used for navigation, but they behave differently.

1. `Navigator.pop`: This method is used to remove the current screen from the navigation stack and navigate back to the previous screen. If the current screen was pushed onto the stack by a `Navigator.push` operation, `Navigator.pop` will return to the original screen. Here's an example:

```dart
Navigator.pop(context);
```

2. `Navigator.popUntil`: This method is used to repeatedly pop the navigation stack until a particular condition is met. The condition is provided as a callback that accepts a `Route` object and returns a boolean. If the callback returns true for a given route, that route and all routes above it are popped. Here's an example:

```dart
Navigator.popUntil(context, (route) => route.isFirst);
```

In this code, `route.isFirst` is a boolean that is true if the route is the first route in the navigation stack (i.e., the home route). So, this line of code pops all routes off the navigation stack until it reaches the first route.

In summary, use `Navigator.pop` when you want to navigate back to the previous screen. Use `Navigator.popUntil` when you want to pop multiple screens off the navigation stack until a certain condition is met.
