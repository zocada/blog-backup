---
ID: 980
post_title: >
  Drawing Custom Shapes in Flutter using
  CustomPainter
author: Rumaan
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/drawing-custom-shapes-in-flutter-using-custompainter/
published: true
post_date: 2019-01-22 17:10:50
---
<h2>Brief intro about Flutter</h2>
Flutter is a Mobile UI framework by Google which allows developers to create beautiful apps in record time for both iOS and Android with a single codebase. Most talked about feature that Flutter comes with is "Hot Reload" that allows blazing fast reload times (without actually loosing the current state of the app)

<em>This article assumes that you are already familiar with or at least have an understanding of building a basic Flutter App with simple nested widgets.</em>
<h2>Custom Shapes</h2>
Apart from inbuilt or trivial widgets that Flutter Framework provides like a Text Widget, a RaisedButton or a Container for bare bones what if we want to draw a custom button that has a custom shape or you just simply want to bring out that inner artist in you, Flutter makes it a breeze to draw these custom artistic shapes.

&nbsp;

[gallery columns="2" size="medium" ids="988,987"]
<h3>Let's get started with making some simple custom shapes</h3>
<h5>Step 1: Create a new Flutter Project</h5>
Run the following command in your Terminal/Command prompt

<code class="EnlighterJSRAW" data-enlighter-language="null">flutter create custom_shapes</code>

This will create a new flutter project and set up all the dependencies for you. After its done just open the folder in your preferred code editor. I will be using VSCode throughout this article for this project.

You can see the basic material app code that flutter generated for you in the lib/main.dart file. To run the app in emulator or your phone just goto Command Pallet (Command/Control + Shift + P) and type "Flutter: Select Device" and choose the device in which you would like to run the app. Goto Debug -&gt; Start Without Debugging to start compiling and running the app on the chosen device.

[gallery size="large" ids="996,997,1002"]
<h5>Step 2: Creating a Base UI</h5>
Let's remove all the unwanted code from the <em>main.dart</em> file and start from the beginning with a bare minimum app screen that has a simple scaffold with an AppBar having the title.

&nbsp;
<pre class="EnlighterJSRAW" data-enlighter-language="java">import 'package:flutter/material.dart';

void main() =&gt; runApp(HomePage());

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        brightness: Brightness.dark,
        accentColor: Colors.deepOrangeAccent,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Shapes'),
        ),
        body: Padding(
          padding: EdgeInsets.all(8.0),
          child: Container(),
        ),
      ),
    );
  }
}
</pre>
&nbsp;

&nbsp;

[caption id="attachment_1012" align="aligncenter" width="512"]<a href="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-21-at-9.39.55-AM.png"><img class="wp-image-1012 size-full" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-21-at-9.39.55-AM.png" alt="Initial App screen when its run with all the widgets removed and just having a MaterialApp and a Scaffold with Container" width="512" height="905" /></a> Initial Screen[/caption]
<h5>Step 3: Let's draw something</h5>
We will make use <a href="https://docs.flutter.io/flutter/widgets/CustomPaint-class.html">CustomPaint</a> Widget which allow us to draw things on the screen by making use of a CustomPainter object.
<pre class="EnlighterJSRAW" data-enlighter-language="java">CustomPaint(
  painter: MyCustomPainter(),
  child: Widget(),
  ....
)
</pre>
CustomPaint widget requires mainly two things, a <em>painter</em> and a <em>child widget</em>. The Custom paint uses the <em>painter</em> to paint/draw (ex: custom shapes) on the canvas after which it draws the child widget on top of it. Let's add this CustomPaint Widget to our app and start drawing something.
<pre class="EnlighterJSRAW" data-enlighter-language="java">body: Padding(
          padding: EdgeInsets.all(8.0),
          child: CustomPaint(
            painter: ShapesPainter(),
            child: Container(height: 700,),
          ),
       ),</pre>
Here,<em> ShapesPainter()</em> is an instance of a class that extends <em>CustomPainter. </em>The <em>CustomPainter </em>class provides us with 2 methods to override.
<pre class="EnlighterJSRAW" data-enlighter-language="java">class ShapesPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: implement paint
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    // TODO: implement shouldRepaint
    return null;
  }
}</pre>
The <em>shouldRepaint</em> method is used to optimise repaints and basically tell whether the widget needs to be repainted if this properties change. You can read more about that <a href="https://docs.flutter.io/flutter/rendering/CustomPainter/shouldRepaint.html">here</a>.

The <em>paint </em>method is where the real magic happens. This method comes with two parameters. A canvas and the Size of the canvas (or boundaries). We <em><strong>draw</strong> </em>stuffs <strong>on</strong> this <strong><em>Canvas</em></strong> using a <em><strong>Paint </strong></em>object which can be created and customised as required. The <em>paint </em>can have various properties like color, shader, style etc. more about it <a href="https://docs.flutter.io/flutter/dart-ui/Paint-class.html">here</a>.

So to just sum it all up, we use a paint (more like a brush) and draw stuffs on the Canvas that we have been provided with which has some width and height. It's similar to how we draw something on a piece of paper using a pencil. Here the paper would have definite width and height (that would be the Canvas object here) and the pencil that we used to draw might have different levels of darkness and color etc. (that would be our Paint object here).

The <a href="https://docs.flutter.io/flutter/dart-ui/Canvas-class.html">canvas</a> object comes with some helper methods like drawCircle, drawRect etc. to draw a circle and draw a rectangle. All the draw..() methods in the canvas requires a paint object.

Let's create a simple paint object which has a color of Colors.deepOrange and draw a circle on the canvas.
<pre class="EnlighterJSRAW" data-enlighter-language="java">class ShapesPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();
    // set the color property of the paint
    paint.color = Colors.deepOrange;

    // center of the canvas is (x,y) =&gt; (width/2, height/2)
    var center = Offset(size.width / 2, size.height / 2);
    
    // draw the circle on centre of canvas having radius 75.0
    canvas.drawCircle(center, 75.0, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) =&gt; false;
}
</pre>
[caption id="attachment_1032" align="aligncenter" width="512"]<img class="wp-image-1032 size-full" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-22-at-7.37.53-PM.png" alt="A Custom Orange circle drawn on the middle of the canvas" width="512" height="905" /> Custom Drawn Circle at the center of canvas[/caption]

&nbsp;

<em>canvas.drawCircle(...)</em> method takes in three parameters, the centre of the circle, the radius and the paint object to be used. Here, we draw the circle at the centre of the canvas. We find the centre using <em>size.width</em> and <em>size.height</em> from the Size object which returns the width and height of the canvas.

The <em>shouldRepaint</em> method here just returns <em>false </em>since we don't have any fields/values that might change and influence the custom shapes that we draw.

Now let's draw a simple white rectangle which spans to the entire width and height of the canvas. We can use the <em>canvas.drawRect(..)</em> method to do so. The <em>drawRect()</em> method takes <a href="https://docs.flutter.io/flutter/dart-ui/Rect-class.html">Rect</a> object and a <em>paint</em>. We can create an instance of Rect object in various ways. We'll use <em><a href="https://docs.flutter.io/flutter/dart-ui/Rect/Rect.fromLTWH.html">Rect.fromLTWH()</a>, </em>where LTWH stands for Left, Top, Width and Height which means the initial (x,y) point that we start from or the left-topmost point of the rectangle and the width and height of the rectangle that would be added to left and top points which forms the required rectangle.
<pre class="EnlighterJSRAW" data-enlighter-language="java">@override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();

    // set the color property of the paint
    paint.color = Colors.deepOrange;

    // center of the canvas is (x,y) =&gt; (width/2, height/2)
    var center = Offset(size.width / 2, size.height / 2);

    // draw the circle with center having radius 75.0
    canvas.drawCircle(center, 75.0, paint);

    // set the paint color to be white
    paint.color = Colors.white;
    
    // Create a rectangle with size and width same as the canvas
    var rect = Rect.fromLTWH(0, 0, size.width, size.height);

    // draw the rectangle using the paint
    canvas.drawRect(rect, paint);
  }</pre>
[caption id="attachment_1035" align="aligncenter" width="512"]<img class="wp-image-1035 size-full" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-22-at-8.58.13-PM.png" alt="Custom White Rectangle drawn which spans to the canvas width and height but its drawn above the orange circle" width="512" height="905" /> White Rectangle[/caption]

But wait, where is the circle?

Well, the circle hasn't gone anywhere. It's just hidden behind the rectangle. This brings up an important characteristic of drawing using CustomPainter here. The <em>order how you write</em> the draw commands matter. If you look at the code closely, the drawCircle() function is called first and after that the drawRect(). So, the circle will be drawn on the canvas first and then the rectangle. We can easily fix (since we want the circle on the rectangle) that by just moving the drawCircle() function after the drawRect().
<pre class="EnlighterJSRAW" data-enlighter-language="java">@override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();

    // set the paint color to be white
    paint.color = Colors.white;
    
    // Create a rectangle with size and width same as the canvas
    var rect = Rect.fromLTWH(0, 0, size.width, size.height);

    // draw the rectangle using the paint
    canvas.drawRect(rect, paint);

    // set the color property of the paint
    paint.color = Colors.deepOrange;

    // center of the canvas is (x,y) =&gt; (width/2, height/2)
    var center = Offset(size.width / 2, size.height / 2);

    // draw the circle with center having radius 75.0
    canvas.drawCircle(center, 75.0, paint);
  }</pre>
[caption id="attachment_1037" align="aligncenter" width="512"]<img class="wp-image-1037 size-full" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-22-at-9.07.44-PM.png" alt="The Orange circle drawn over the white rectangle after fixing the code." width="512" height="905" /> Orange Circle over the white rectangle[/caption]

&nbsp;

Looks good! Now let's draw a custom path and wrap this up!

To draw a custom path we'll use drawPath() method from the canvas. We'll draw a path from <em>top-left(0,0)</em> to <em>bottom-left(0, size.height)</em> to <em>top-right(size.width, 0) </em>which forms a simple triangle.

To do this we'll have to use a <a href="https://docs.flutter.io/flutter/dart-ui/Path-class.html"><em>Path</em></a> object to represent the path that we draw. The way we draw the path is quite simple. Whenever we initialise a path object i.e path = Path(), the initial point defaults to (0,0) i.e top-left off the screen. The coordinate system of the canvas looks something like this.

[caption id="attachment_1042" align="aligncenter" width="634"]<img class="wp-image-1042 size-full" src="https://zocada.com/wp-content/uploads/2019/01/coordinate-2.png" alt="Coordinate system in the Flutter canvas" width="634" height="497" /> Coordinate system[/caption]

&nbsp;

We can use the lineTo() method to create a line from (x,y) to (x1, y1). Here it would be from (0,0) which is initialised by default, to (0, size.height) which is the bottom-left of the canvas. Finally we use close() to close the path which will forms a triangle.
<pre class="EnlighterJSRAW" data-enlighter-language="java">paint.color = Colors.yellow;

// create a path
var path = Path();
path.lineTo(0, size.height);
path.lineTo(size.width, 0);
// close the path to form a bounded shape
path.close();</pre>
[caption id="attachment_1045" align="aligncenter" width="512"]<img class="wp-image-1045 size-full" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-22-at-10.00.34-PM.png" alt="A yellow path drawn on canvas that makes up a triangle" width="512" height="905" /> Yellow path[/caption]

Let's move the code that draws the circle to the end so that it's layered on top of all the other shapes.

Here's the entire code.
<pre class="EnlighterJSRAW" data-enlighter-language="java">import 'package:flutter/material.dart';

void main() =&gt; runApp(HomePage());

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        brightness: Brightness.dark,
        accentColor: Colors.deepOrangeAccent,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Shapes'),
        ),
        body: Padding(
          padding: EdgeInsets.all(8.0),
          child: CustomPaint(
            painter: ShapesPainter(),
            child: Container(
              height: 700,
            ),
          ),
        ),
      ),
    );
  }
}

class ShapesPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();

    // set the paint color to be white
    paint.color = Colors.white;

    // Create a rectangle with size and width same as the canvas
    var rect = Rect.fromLTWH(0, 0, size.width, size.height);

    // draw the rectangle using the paint
    canvas.drawRect(rect, paint);

    paint.color = Colors.yellow;

    // create a path
    var path = Path();
    path.lineTo(0, size.height);
    path.lineTo(size.width, 0);
    // close the path to form a bounded shape
    path.close();

    canvas.drawPath(path, paint);

    // set the color property of the paint
    paint.color = Colors.deepOrange;

    // center of the canvas is (x,y) =&gt; (width/2, height/2)
    var center = Offset(size.width / 2, size.height / 2);

    // draw the circle with center having radius 75.0
    canvas.drawCircle(center, 75.0, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) =&gt; false;
}
</pre>
[caption id="attachment_1048" align="aligncenter" width="512"]<img class="wp-image-1048 size-full" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-2019-01-22-at-10.03.27-PM.png" alt="Final app with a white rectangular background and yellow triangle path and an orange circle on top all of which drawn on the canvas." width="512" height="905" /> Final App with custom shapes[/caption]

&nbsp;

Play around with the code and try new shapes and colors and what not.

You can find the code <a href="https://github.com/rumaan/custom_shapes_flutter">here</a> in this GitHub repo.

🤤

<hr />

<em>Also published on <a href="https://medium.com/@rumaankalander/drawing-custom-shapes-in-flutter-using-custompainter-47be782b697">Medium</a>.</em>