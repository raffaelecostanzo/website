---
title: Handle taps
description: How to handle tapping and dragging.
js:
  - defer: true
    url: https://dartpad.dev/inject_embed.dart.js
---

{% include docs/yt_shims.liquid %}

<?code-excerpt path-base="cookbook/gestures/handling_taps/"?>

You not only want to display information to users,
you want users to interact with your app.
Use the [`GestureDetector`][] widget to respond
to fundamental actions, such as tapping and dragging.

{{site.alert.note}}
  To learn more, watch this short Widget of the Week video on the GestureDetector widget:

  <iframe class="full-width" src="{{yt-embed}}/WhVXkCFPmK4" title="Learn about the GestureDetector Flutter Widget" {{yt-set}}></iframe>
{{site.alert.end}}

This recipe shows how to make a custom button that shows
a snackbar when tapped with the following steps:

  1. Create the button.
  2. Wrap it in a `GestureDetector` that an `onTap()` callback.

<?code-excerpt "lib/main.dart (GestureDetector)" replace="/return //g;/;$//g"?>
```dart
// The GestureDetector wraps the button.
GestureDetector(
  // When the child is tapped, show a snackbar.
  onTap: () {
    const snackBar = SnackBar(content: Text('Tap'));

    ScaffoldMessenger.of(context).showSnackBar(snackBar);
  },
  // The custom button
  child: Container(
    padding: const EdgeInsets.all(12),
    decoration: BoxDecoration(
      color: Colors.lightBlue,
      borderRadius: BorderRadius.circular(8),
    ),
    child: const Text('My Button'),
  ),
)
```

## Notes

  1. For information on adding the Material ripple effect to your
     button, see the [Add Material touch ripples][] recipe.
  2. Although this example creates a custom button,
     Flutter includes a handful of button implementations, such as:
     [`ElevatedButton`][], [`TextButton`][], and
     [`CupertinoButton`][].

## Interactive example

<?code-excerpt "lib/main.dart"?>
```run-dartpad:theme-light:mode-flutter:run-true:width-100%:height-600px:split-60:ga_id-interactive_example
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    const title = 'Gesture Demo';

    return const MaterialApp(
      title: title,
      home: MyHomePage(title: title),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final String title;

  const MyHomePage({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: const Center(
        child: MyButton(),
      ),
    );
  }
}

class MyButton extends StatelessWidget {
  const MyButton({super.key});

  @override
  Widget build(BuildContext context) {
    // The GestureDetector wraps the button.
    return GestureDetector(
      // When the child is tapped, show a snackbar.
      onTap: () {
        const snackBar = SnackBar(content: Text('Tap'));

        ScaffoldMessenger.of(context).showSnackBar(snackBar);
      },
      // The custom button
      child: Container(
        padding: const EdgeInsets.all(12),
        decoration: BoxDecoration(
          color: Colors.lightBlue,
          borderRadius: BorderRadius.circular(8),
        ),
        child: const Text('My Button'),
      ),
    );
  }
}
```

<noscript>
  <img src="/assets/images/docs/cookbook/handling-taps.gif" alt="Handle taps demo" class="site-mobile-screenshot" />
</noscript>

[Add Material touch ripples]: {{site.url}}/cookbook/gestures/ripples
[`CupertinoButton`]: {{site.api}}/flutter/cupertino/CupertinoButton-class.html
[`TextButton`]: {{site.api}}/flutter/material/TextButton-class.html
[`GestureDetector`]: {{site.api}}/flutter/widgets/GestureDetector-class.html
[`ElevatedButton`]: {{site.api}}/flutter/material/ElevatedButton-class.html
