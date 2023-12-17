### What is the difference between SizedBox and Container widget?

In Flutter, both `SizedBox` and `Container` are widgets used to control the layout and size of their child widgets, but they have some differences:

1. `SizedBox`: This widget forces its child to have a specific width and/or height. If either the width or height is null, this widget will size itself to match the child's size in that dimension. If the child widget is null, it will adjust itself to the given width and height. It doesn't have any styling properties. Here's an example:

```dart
SizedBox(
  width: 100,
  height: 100,
  child: Text('Hello World'),
)
```

In this example, the `SizedBox` forces its child `Text` widget to be exactly 100 logical pixels wide and 100 logical pixels high.

2. `Container`: This widget is a convenience widget that combines common painting, positioning, and sizing widgets. It can take a child widget and apply padding, margins, borders, background color, or other decorations to it. If the `Container` has no child, it will automatically expand to fill the available space. If it has a child, it will size itself to the child's size. Here's an example:

```dart
Container(width: 100,
  height: 100,
  padding: const EdgeInsets.all(8.0),
  margin: const EdgeInsets.all(4.0),
  decoration: BoxDecoration(
    color: Colors.blue,
    border: Border.all(color: Colors.black),
  ),
  child: Text('Hello World'),
)
```

In this example, the `Container` forces its child `Text` widget to be exactly 100 logical pixels wide and 100 logical pixels high. It also applies a padding of 8 logical pixels to all sides of the child, a margin of 4 logical pixels to all sides of the `Container`, and a blue background color with a black border.

In summary, `SizedBox` is a simpler widget for controlling the size of a single child, while `Container` provides more comprehensive styling and layout options.


### What types of decoration in Container widget flutter?
In Flutter, the `Container` widget can have a `decoration` property which is of type `BoxDecoration`. The `BoxDecoration` class provides a variety of ways to draw a box. Here are some of the properties you can use:

1. `color`: This property is used to set the color of the box. It takes a `Color` object.

2. `image`: This property is used to set the background image of the box. It takes a `DecorationImage` object.

3. `border`: This property is used to create a border around the box. It takes a `Border` object.

4. `borderRadius`: This property is used to create a rounded rectangle border around the box. It takes a `BorderRadius` object.

5. `boxShadow`: This property is used to cast a shadow behind the box. It takes a list of `BoxShadow` objects.

6. `gradient`: This property is used to set a gradient effect on the box. It takes a `Gradient` object.

7. `shape`: This property is used to shape the box. It takes a `BoxShape` enum which can be either `BoxShape.rectangle` or `BoxShape.circle`.

Here's an example of a `Container` with a `BoxDecoration`:

```dart
Container(
  height: 200,
  width: 200,
  decoration: BoxDecoration(
    color: Colors.amber,
    image: DecorationImage(
      image: NetworkImage('https://example.com/image.jpg'),
      fit: BoxFit.cover,
    ),
    border: Border.all(
      color: Colors.black,
      width: 3,
    ),
    borderRadius: BorderRadius.circular(10),
    boxShadow: [
      BoxShadow(
        color: Colors.grey.withOpacity(0.5),
        spreadRadius: 5,
        blurRadius: 7,
        offset: Offset(0, 3),
      ),
    ],
    gradient: LinearGradient(
      begin: Alignment.topLeft,
      end: Alignment.bottomRight,
      colors: [Colors.red, Colors.blue],
    ),
    shape: BoxShape.rectangle,
  ),
)
```

In this example, the `Container` has a height and width of 200. The `BoxDecoration` has a color of amber, a background image, a black border with a width of 3, a border radius of 10, a box shadow, a linear gradient from red to blue, and a rectangular shape.

### MainAxisAlignment and CrossAxisAlignment in Flutter?
In Flutter, `MainAxisAlignment` and `CrossAxisAlignment` are enums used in widgets like `Row`, `Column`, and `Flex` to align their children along the main axis and cross axis respectively.

1. `MainAxisAlignment`: This enum is used to align children along the main axis. Here are its values:

    - `MainAxisAlignment.start`: Place the children as close to the start of the main axis as possible.
    - `MainAxisAlignment.end`: Place the children as close to the end of the main axis as possible.
    - `MainAxisAlignment.center`: Place the children in the middle of the main axis.
    - `MainAxisAlignment.spaceBetween`: Place the free space evenly between the children.
    - `MainAxisAlignment.spaceAround`: Place the free space evenly between the children as well as half of that space before and after the first and last child.
    - `MainAxisAlignment.spaceEvenly`: Distribute the children and the free space evenly along the main axis.

2. `CrossAxisAlignment`: This enum is used to align children along the cross axis. Here are its values:

    - `CrossAxisAlignment.start`: Place the children as close to the start of the cross axis as possible.
    - `CrossAxisAlignment.end`: Place the children as close to the end of the cross axis as possible.
    - `CrossAxisAlignment.center`: Place the children in the middle of the cross axis.
    - `CrossAxisAlignment.stretch`: Stretch the children along the cross axis to fill the cross space.
    - `CrossAxisAlignment.baseline`: Align the children along their baseline. This requires that the `textBaseline` property is set.

Here's an example of how to use `MainAxisAlignment` and `CrossAxisAlignment` in a `Column`:

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: <Widget>[
    Text('Hello'),
    Text('World'),
  ],
)
```

In this example, the `Column` widget has two `Text` children. The `mainAxisAlignment` property is set to `MainAxisAlignment.spaceEvenly`, which means the children and the free space are distributed evenly along the main axis. The `crossAxisAlignment` property is set to `CrossAxisAlignment.center`, which means the children are placed in the middle of the cross axis.

### What is the difference between Expanded and Flexible widget?
In Flutter, both `Flexible` and `Expanded` widgets are used to control how a widget flexes within a `Flex` widget (like `Row` or `Column`). However, they have a key difference:

1. `Flexible`: This widget controls how a child of a `Row`, `Column`, or `Flex` flexes. The `Flexible` widget does not require the child to fill the available space. If the `fit` property is `FlexFit.tight` (the default), the child is forced to fill the available space. If the `fit` property is `FlexFit.loose`, the child can be at most as large as the available space. Here's an example:

```dart
Flexible(
  flex: 2,
  fit: FlexFit.loose,
  child: Container(color: Colors.amber),
)
```

> If you use multiple `Flexible` widgets in a row, you must set the `flex`
> property on all of them.

In this example, the `Container` can be at most as large as the available space, but it's not forced to fill it.

2. `Expanded`: This widget is a shorthand for `Flexible` with `fit: FlexFit.tight`. It forces the child to fill the available space along the main axis. Here's an example:

```dart
Expanded(
  flex: 2,
  child: Container(color: Colors.amber),
)
```
In this example, the `Container` is forced to fill the available space.

> `Expanded` uses the **available** space given by `flex` property.

In summary, `Flexible` gives you the option to fill the available space or not, while `Expanded` always fills the available space.

### FlexFit enum in Flexible widget?
In Flutter, `FlexFit` is an enum used with the `Flexible` widget to control how a child of a `Row`, `Column`, or `Flex` flexes. It has two values:

1. `FlexFit.tight`: This forces the child to fill the available space along the main axis. If multiple children are marked as `FlexFit.tight`, the available space is divided according to the `flex` factor.

2. `FlexFit.loose`: This allows the child to be smaller than the available space. The child can be at most as large as the available space but is not forced to fill it. If multiple children are marked as `FlexFit.loose`, they are allocated space before the remaining space is divided among the children marked as `FlexFit.tight`.

Here's an example of how to use `FlexFit` in a `Row`:

```dart
Row(
  children: <Widget>[
    Flexible(
      flex: 2,
      fit: FlexFit.tight,
      child: Container(color: Colors.amber),
    ),
    Flexible(
      flex: 1,
      fit: FlexFit.loose,
      child: Container(color: Colors.blue),
    ),
  ],
)
```

In this example, the `Row` widget has two children. The first child is a `Container` with `FlexFit.tight`, which means it is forced to fill the available space. The second child is a `Container` with `FlexFit.loose`, which means it can be at most as large as the available space but is not forced to fill it.

### Difference between Image and CircleAvatar widget?
In Flutter, `Image` and `CircleAvatar` are both widgets used to display images, but they have different purposes and features:

1. `Image`: This widget displays an image. It can display images from different sources such as network, assets, or files. It also provides various properties to control how the image is displayed, such as `fit` (how to inscribe the image into the space allocated during layout), `alignment`, `repeat`, etc. Here's an example:

```dart
Image.network(
  'https://example.com/image.jpg',
  fit: BoxFit.cover,
)
```

In this example, the `Image` widget displays an image from a URL and scales the image to fill its layout box while maintaining the image's aspect ratio.

2. `CircleAvatar`: This widget displays a circular avatar image. It's typically used for profile images. It takes a `backgroundImage` property for the image to display and automatically shapes it as a circle. It also has a `backgroundColor` property to set the color of the circle. Here's an example:

```dart
CircleAvatar(
  backgroundImage: NetworkImage('https://example.com/image.jpg'),
  backgroundColor: Colors.blue,
)
```

In this example, the `CircleAvatar` widget displays a circular image from a URL with a blue background.

In summary, use `Image` when you need to display an image with various configurations, and use `CircleAvatar` when you need to display a circular image, typically for avatars.

### `Positioned` widget in Flutter?
The `Positioned` widget in Flutter is a widget that controls where a child of a `Stack` is positioned. It can be used to specify the position of a child widget in the `Stack` along the horizontal and vertical axes.

The `Positioned` widget has the following properties:

- `top`: The distance from the top edge of the `Stack` to the top edge of the child widget.
- `right`: The distance from the right edge of the `Stack` to the right edge of the child widget.
- `bottom`: The distance from the bottom edge of the `Stack` to the bottom edge of the child widget.
- `left`: The distance from the left edge of the `Stack` to the left edge of the child widget.
- `width`: The width of the child widget.
- `height`: The height of the child widget.

Here's an example of how to use the `Positioned` widget:

```dart
Stack(
  children: <Widget>[
    Container(color: Colors.yellow),
    Positioned(
      top: 50,
      left: 50,
      child: Container(color: Colors.red, width: 100, height: 100),
    ),
  ],
)
```

In this example, the `Positioned` widget is used to position a red `Container` 50 pixels from the top and left edges of the yellow `Container`. The red `Container` has a width and height of 100 pixels.

### Types of ScrollView widget in Flutter
In Flutter, there are several types of ScrollView widgets that you can use to create scrollable layouts. Here are some of them:

1. `ScrollView`: This is an abstract class that scrolls a single child. It's not typically used directly. Instead, consider using the `ListView` or `CustomScrollView`.

2. `ListView`: This is probably the most commonly used. It's a scrollable list of widgets arranged linearly.

3. `GridView`: This is a scrollable, 2D array of widgets. You can control the aspect ratio of its items, and it can automatically arrange its children in a grid format.

4. `CustomScrollView`: A `ScrollView` that creates custom scroll effects using slivers. A `CustomScrollView` lets you supply slivers directly to create various scrolling effects, such as lists, grids, and expanding headers.

5. `SingleChildScrollView`: A box in which a single widget can be scrolled. This is useful when you need to make a single child scrollable.

6. `PageView`: A scrollable list that works page by page. Each child of a `PageView` is forced to be the same size as the viewport.

7. `NestedScrollView`: A scrolling view inside of which can be nested other scrolling views, with their scroll positions being intrinsically linked.

8. `Scrollable`: A widget that scrolls. `Scrollable` implements the interaction model for a scrollable widget, including gesture recognition, but does not have an opinion about how the viewport, which actually displays the children, is constructed.

Remember, each of these ScrollView widgets has its own use cases and properties, and you should choose the one that best fits your needs.

### `physics` property in ScrollView widget?
The `physics` property in the `SingleChildScrollView` widget in Flutter is used to determine how the widget should respond to user input, for example, how the widget should behave when the user reaches the maximum scroll extent.

By default, `SingleChildScrollView` uses `ScrollPhysics`, which allows for the bouncing effect on iOS and a clamping effect on Android when the scroll extent is reached. However, you can change this behavior by providing a different `ScrollPhysics` subclass.

Here are a few examples of `ScrollPhysics` subclasses:

- `BouncingScrollPhysics`: This creates a bouncing effect when the scroll extent is reached. This is the default behavior on iOS.
- `ClampingScrollPhysics`: This creates a clamping effect when the scroll extent is reached. This is the default behavior on Android.
- `NeverScrollableScrollPhysics`: This disables scrolling altogether.
- `AlwaysScrollableScrollPhysics`: This enables scrolling even if the content does not exceed the viewport.

Here's an example of how to use the `physics` property in a `SingleChildScrollView`:

```dart
SingleChildScrollView(
  physics: BouncingScrollPhysics(), // Change this to the ScrollPhysics subclass you want to use
  child: Column(
    children: [
      // Your widgets here
    ],
  ),
)
```

In your code, you're already using `BouncingScrollPhysics`:

```dart
SingleChildScrollView(
  physics: const BouncingScrollPhysics(),
  // ...
)
```

This means that your `SingleChildScrollView` will have a bouncing effect when the user scrolls beyond the content.

### MediaQuery
`MediaQuery` is a widget in Flutter that provides access to the media query data from the current `BuildContext`. The `MediaQueryData` includes information about the user's device such as screen size, orientation, and brightness.

You can use `MediaQuery` to make your app responsive to different screen sizes and orientations. For example, you can use it to set the width of a widget to half the width of the screen like this:

```dart
double screenWidth = MediaQuery.of(context).size.width;
double halfScreenWidth = screenWidth / 2;

Container(
  width: halfScreenWidth,
  // other properties...
)
```

In this example, `MediaQuery.of(context).size.width` gets the width of the screen from the `MediaQueryData`. The width of the `Container` is then set to half the width of the screen.

You can also use `MediaQuery` to check the orientation of the device and adjust your layout accordingly. For example:

```dart
bool isLandscape = MediaQuery.of(context).orientation == Orientation.landscape;

if (isLandscape) {
  // build a landscape layout
} else {
  // build a portrait layout
}
```

In this example, `MediaQuery.of(context).orientation` gets the orientation of the device from the `MediaQueryData`. If the orientation is landscape, a landscape layout is built. Otherwise, a portrait layout is built.

### LayoutBuilder widget in Flutter
The `LayoutBuilder` widget in Flutter is a widget that builds itself based on its parent widget's size. It takes a `BuildContext` and `BoxConstraints` as input and returns a widget. The `BoxConstraints` contains the minimum and maximum width and height of the parent widget.

Here's an example of how to use the `LayoutBuilder` widget:

```dart
LayoutBuilder(
  builder: (BuildContext context, BoxConstraints constraints) {
    if (constraints.maxWidth > 600) {
      return WideLayoutWidget();
    } else {
      return NarrowLayoutWidget();
    }
  },
)
```

In this example, the `LayoutBuilder` widget checks the maximum width of its parent widget. If the maximum width is greater than 600, it returns the `WideLayoutWidget`. Otherwise, it returns the `NarrowLayoutWidget`. This can be useful for creating responsive layouts that adapt to different screen sizes.

### LayoutBuilder useful properties and methods
The `BoxConstraints` class in Flutter represents a set of constraints that are used to determine the size of widgets. It has several useful properties and methods:

Properties:

1. `minWidth`: The smallest allowable width of the box. This value must be non-negative and less than or equal to `maxWidth`.

2. `maxWidth`: The largest allowable width of the box. This value must be non-negative and greater than or equal to `minWidth`.

3. `minHeight`: The smallest allowable height of the box. This value must be non-negative and less than or equal to `maxHeight`.

4. `maxHeight`: The largest allowable height of the box. This value must be non-negative and greater than or equal to `minHeight`.

Methods:

1. `BoxConstraints.tight(Size size)`: Creates box constraints that require the given size.

2. `BoxConstraints.expand({double? width, double? height})`: Creates box constraints that expand to fill another box constraints. If width or height is given, the constraints require exactly this width or height.

3. `BoxConstraints.tightFor({double? width, double? height})`: Creates box constraints that require the given width or height.

4. `BoxConstraints.tightForFinite({double width = double.infinity, double height = double.infinity})`: Creates box constraints that require the given width or height, treating null as zero.

5. `BoxConstraints.loose(Size size)`: Creates box constraints that is respected only for their maximum value: they can be any size, so long as they are not larger than the given size.

6. `BoxConstraints.lerp(BoxConstraints a, BoxConstraints b, double t)`: Linearly interpolate between two BoxConstraints.

7. `hasTightWidth`, `hasTightHeight`: These are getter methods that return true if the constraints have a tight width/height.

8. `hasBoundedWidth`, `hasBoundedHeight`: These are getter methods that return true if the constraints have a bounded width/height.

9. `isTight`: This is a getter method that returns true if the constraints have both a tight width and height.

10. `isNormalized`: This is a getter method that returns true if the constraints are normalized; that is, the minimums are less than or equal to the maximums and the values are all non-negative.

11. `biggest`: This is a getter method that returns the size that both has the largest width and height that satisfy these constraints.

12. `smallest`: This is a getter method that returns the size that both has the smallest width and height that satisfy these constraints.

13. `constrain(Size size)`: Returns the size that this box should be given its constraints.

14. `constrainDimensions(double width, double height)`: Returns the size that this box should be given the provided dimensions.

15. `constrainWidth([double width = double.infinity])`: Returns the width that this box should be given the provided width.

16. `constrainHeight([double height = double.infinity])`: Returns the height that this box should be given the provided height.

17. `enforce(BoxConstraints constraints)`: Returns a new box constraints that is the intersection of the current box constraints and the given box constraints.

18. `deflate(EdgeInsets edges)`: Returns a new box constraints that is smaller by the given edge dimensions in each direction.

19. `inflate(EdgeInsets edges)`: Returns a new box constraints that is bigger by the given edge dimensions in each direction.

20. `flipped`: Returns a new box constraints with the width and height constraints swapped.

Here is an example of how to use `BoxConstraints`:

```dart
Container(
  constraints: BoxConstraints.expand(height: 50.0),
  color: Colors.blue,
  child: Text('Hello World'),
)
```

In this example, the `Container` widget has a `BoxConstraints` that expands to fill the height, with a specified height of 50.0 logical pixels.

### Types of Buttons widget in Flutter
In Flutter, there are several types of buttons that you can use. Here are some examples:

1. `ElevatedButton`: This is a Material Design raised button. It contains ink splashes for a pressed state.

```dart
ElevatedButton(
  onPressed: () {
    print("Elevated Button Pressed");
  },
  child: Text("Elevated Button"),
)
```

2. `TextButton`: This is a Material Design text button. Text buttons are typically used for less-pronounced actions, including those located in dialogs and cards.

```dart
TextButton(
  onPressed: () {
    print("Text Button Pressed");
  },
  child: Text("Text Button"),
)
```

3. `OutlinedButton`: This is a Material Design outlined button. Outlined buttons are medium-emphasis buttons. They contain actions that are important, but they aren’t the primary action in an app.

```dart
OutlinedButton(
  onPressed: () {
    print("Outlined Button Pressed");
  },
  child: Text("Outlined Button"),
)
```

4. `IconButton`: This is a Material Design icon button. It's an icon that reacts to touch by filling with color (ink).

```dart
IconButton(
  icon: Icon(Icons.volume_up),
  onPressed: () {
    print("Icon Button Pressed");
  },
)
```

5. `FloatingActionButton`: This is a Material Design floating action button. It is used for a promoted action. It contains an ink splash on press and release.

```dart
FloatingActionButton(
  onPressed: () {
    print("Floating Action Button Pressed");
  },
  child: Icon(Icons.navigation),
  backgroundColor: Colors.green,
)
```

6. `DropdownButton`: This is a Material Design dropdown button. It displays a menu that contains a list of options.

```dart
DropdownButton<String>(
  value: dropdownValue,
  icon: Icon(Icons.arrow_downward),
  onChanged: (String? newValue) {
    setState(() {
      dropdownValue = newValue!;
    });
  },
  items: <String>['One', 'Two', 'Three', 'Four']
    .map<DropdownMenuItem<String>>((String value) {
      return DropdownMenuItem<String>(
        value: value,
        child: Text(value),
      );
    }).toList(),
)
```

Remember to replace `setState` and `dropdownValue` with your own state management solution.

### What is the MaterialStateColor.resolveWith
`MaterialStateColor.resolveWith((states) => Colors.blue)` is a method in Flutter that returns a color that responds to changes in the Material widget's state.

The `resolveWith` method takes a callback function that provides a set of `MaterialState`s, and returns a color that corresponds to that state. In this case, regardless of the state, it always returns `Colors.blue`.

Here's a simple example of how it can be used:

```dart
ElevatedButton(
  onPressed: () {},
  child: Text('Button'),
  style: ButtonStyle(
    backgroundColor: MaterialStateColor.resolveWith((states) => Colors.blue),
  ),
)
```

In this example, the background color of the `ElevatedButton` will always be blue, regardless of its state (pressed, hovered, focused, etc.).

### Ink and InkWell widget in Flutter
`Ink` and `InkWell` are both widgets in Flutter that are used to handle touch events and provide visual feedback. However, they have different purposes and uses.

`InkWell` is a widget that responds to touch events. It provides a splash effect on the screen when tapped. This is commonly used for buttons and list items to provide feedback to the user that the item has been pressed. It has several callbacks such as `onTap`, `onDoubleTap`, `onLongPress` etc. to handle different types of user interactions.

`Ink` is a widget that paints upon material widgets. It's often used to give a custom shape and appearance to a material widget. The `Ink` widget can display an image, a color, or a gradient. The splash effect of the `InkWell` is rendered in the `Ink` widget.

Here's an example of how they can be used together:

```dart
Material(
  child: Ink(
    decoration: BoxDecoration(
      color: Colors.blue,
      shape: BoxShape.circle,
    ),
    child: InkWell(
      onTap: () {
        print('InkWell tapped');
      },
      child: SizedBox(
        width: 100,
        height: 100,
      ),
    ),
  ),
)
```

In this example, the `Ink` widget is used to give a circular shape and blue color to the `InkWell`. When the `InkWell` is tapped, it displays a splash effect within the circular area defined by the `Ink` widget.

### GestureDetector widget in Flutter
The `GestureDetector` widget in Flutter is a non-visual widget primarily used for detecting the user's gesture. It provides a number of callbacks to handle different types of user interactions. Here are some of the gestures that `GestureDetector` can recognize:

- `onTap`: Triggered when the user taps the screen.
- `onDoubleTap`: Triggered when the user quickly taps the screen twice.
- `onLongPress`: Triggered when the user presses and holds the screen for a long duration.
- `onPanStart`, `onPanUpdate`, `onPanEnd`: These are triggered when the user starts dragging, is dragging, and finishes dragging respectively.
- `onScaleStart`, `onScaleUpdate`, `onScaleEnd`: These are triggered when the user starts a pinch-to-zoom gesture, is in the process of pinch-to-zoom, and finishes the pinch-to-zoom gesture respectively.

Here's an example of how to use the `GestureDetector` widget:

```dart
GestureDetector(
  onTap: () {
    print('Widget has been tapped');
  },
  onDoubleTap: () {
    print('Widget has been double-tapped');
  },
  onLongPress: () {
    print('Widget has been long-pressed');
  },
  child: Container(
    width: 200.0,
    height: 200.0,
    color: Colors.blue,
  ),
)
```

In this example, the `GestureDetector` wraps a `Container`. When the `Container` is tapped, double-tapped, or long-pressed, the corresponding message is printed to the console.

### Difference between GestureDetector and InkWell
`InkWell` and `GestureDetector` are both widgets in Flutter used for detecting user interaction and executing a function when the user interacts with them. However, they have some differences:

1. `InkWell`: This widget is a Material Design concept. It responds to touch events by filling the area with a splash of color (ink). It's commonly used for buttons and list items to provide feedback to the user that the item has been pressed. It has several callbacks such as `onTap`, `onDoubleTap`, `onLongPress` etc. to handle different types of user interactions. The splash effect is rendered within the ink splash area defined by the widget's bounds and `clipBehavior`.

2. `GestureDetector`: This is a non-visual widget that provides gesture recognition. It's more flexible than `InkWell` as it supports a wide range of gestures such as tap, double tap, long press, drag, and scale. However, unlike `InkWell`, it doesn't provide any visual feedback.

In summary, if you need visual feedback such as a splash on touch, use `InkWell`. If you need to support a wide range of gestures and don't need the visual feedback, use `GestureDetector`.

### IndexedStack widget in Flutter
The `IndexedStack` widget in Flutter is a Stack that shows a single child from a list of children. The child that is displayed is determined by the `index` property.

In the context of your code, the `IndexedStack` widget is used to switch between different pages in your application. The `index` property is tied to `_currentIndex`, which is updated when a new tab is selected in the `BottomNavigationBar`.

Here's a simplified example of how `IndexedStack` works:

```dart
IndexedStack(
  index: _currentIndex,
  children: [
    Text("First Page"),
    Text("Second Page"),
  ],
)
```

In this example, if `_currentIndex` is `0`, "First Page" will be displayed. If `_currentIndex` is `1`, "Second Page" will be displayed.

### `SafeArea` widget in Flutter?
`SafeArea` is a widget in Flutter that insets its child by sufficient padding to avoid intrusions by the operating system. For example, this padding includes areas to avoid: the status bar at the top of the screen, the notch on iOS devices, the navigation bar at the bottom, and more.

The primary purpose of `SafeArea` is to make your UI adaptable to various screen sizes and orientations without getting hidden by the system UI.

Here's an example of how to use `SafeArea`:

```dart
SafeArea(
  child: Text('Hello, World!'),
)
```

In this example, the `Text` widget will be displayed in an area that avoids any system intrusions. This means it won't be hidden by the status bar, notch, navigation bar, etc.

You can also customize the behavior of `SafeArea` by setting its properties:

- `top`: If true, the padding includes enough padding to avoid the status bar at the top of the screen. Defaults to true.
- `bottom`: If true, the padding includes enough padding to avoid the system nav bar at the bottom of the screen. Defaults to true.
- `left`: If true, the padding includes enough padding to avoid intrusions on the left. Defaults to true.
- `right`: If true, the padding includes enough padding to avoid intrusions on the right. Defaults to true.

Here's an example of how to use these properties:

```dart
SafeArea(
  top: true,
  bottom: false,
  left: true,
  right: true,
  child: Text('Hello, World!'),
)
```

In this example, the `Text` widget will avoid intrusions from the top, left, and right, but not from the bottom.
