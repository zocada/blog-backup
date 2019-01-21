---
ID: 140
post_title: 'Getting started with Android Development [Java] &#8211; Make your first Android App'
author: Rumaan
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/getting-started-with-android-development-java/
published: true
post_date: 2018-01-14 12:20:37
---
<p style="text-align: left;">Have an excellent idea that you want to turn up into an app or you're just a beginner who wants to get started with Android development. <a href="https://zocada.com/wp-content/uploads/2018/01/2000px-Android_dance.svg_.png"><img class="size-medium wp-image-148 aligncenter" src="https://zocada.com/wp-content/uploads/2018/01/2000px-Android_dance.svg_-211x300.png" alt="" width="211" height="300" /></a>Here are a few steps to hop right in:</p>

First things first is you will need an IDE(Integrated Development Environment)

Back in the days people used to use Eclipse for developing Android Apps but Google has its own IDE now called <a href="https://developer.android.com/studio/index.html">Android Studio</a>

and it's available for multiple platforms like Windows, macOS, Linux.

You can download and install it from <a href="https://developer.android.com/studio/index.html">here</a>.

&nbsp;

After you've done installing and setting up Android Studio.

1.Open Android Studio and at this page select 'Start a new Android Studio Project'

<a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.18.57-PM.png"><img class="wp-image-223 size-full" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.18.57-PM.png" alt="" width="778" height="484" /></a>

<img class="alignnone size-full wp-image-423" src="https://zocada.com/wp-content/uploads/2018/01/StartScreen.png" alt="" width="777" height="482" />

<p style="text-align: left;">2. Choose your Application name - [This is the name of the app and it's going to show up in the App launcher]</p>

Set the company domain - [Leave it as is]

<img class="alignnone size-full wp-image-428" src="https://zocada.com/wp-content/uploads/2018/01/create_app_1.png" alt="" width="900" height="672" />

Choose the project location - [Where the project and its files must be saved]

Leave the other options as is. [For now 😜]

<a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.21.44-PM.png"><img class="alignnone size-full wp-image-224" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.21.44-PM.png" alt="" width="898" height="668" /></a>

<ol>
<li>Select Phone and Tablet and choose the API level [for now leave this as is] and hit next.</li>
</ol>

<img class="alignnone size-full wp-image-429" src="https://zocada.com/wp-content/uploads/2018/01/create_app_2.png" alt="" width="900" height="672" /><a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.28.19-PM.png"><img class="alignnone size-full wp-image-225" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.28.19-PM.png" alt="" width="897" height="666" /></a>

<ol>
<li>Choose Basic Activity or Empty Activity and hit next. This is actually the template for the App [More on this coming soon😇]<a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.30.12-PM.png"><img class="alignnone size-full wp-image-226" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.30.12-PM.png" alt="" width="894" height="667" /></a></li>
</ol>

<img class="alignnone size-full wp-image-426" src="https://zocada.com/wp-content/uploads/2018/01/choose_activity.png" alt="" width="900" height="672" />

<ol>
<li>Leave the options as is [again, for time being 😉] and hit next!<a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.31.04-PM.png"><img class="alignnone size-full wp-image-227" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.31.04-PM.png" alt="" width="898" height="664" /></a></li>
</ol>

&nbsp;

<ol>
<li>Let Android Studio build the project and set everything up for you [Based of your system configuration it should take about a minute or two]. Be patient and let Android Studio do its <em>"thing"</em>. After its done, look to the top right and you should see this.</li>
</ol>

<a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.32.19-PM.png"><img class="alignnone size-full wp-image-228" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.32.19-PM.png" alt="" width="524" height="53" /><img class="alignnone size-full wp-image-431" src="https://zocada.com/wp-content/uploads/2018/01/run_app.png" alt="" width="531" height="57" /></a>

Hit the <em><strong>Green Play</strong></em> button.

<ol>
<li>When this window pops up, plug in your Phone [or if you're using an Emulator, start it] and select the phone the list and hit <strong>OK</strong></li>
</ol>

<img class="alignnone size-full wp-image-427" src="https://zocada.com/wp-content/uploads/2018/01/choose_phone.png" alt="" width="624" height="478" />

<a href="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.36.12-PM.png"><img class="alignnone size-full wp-image-229" src="https://zocada.com/wp-content/uploads/2018/01/Screen-Shot-2018-01-13-at-8.36.12-PM.png" alt="" width="621" height="476" /></a>

If your device doesn't show up make sure,

<ol>
    <li>Your USB cable is working fine</li>
    <li>USB debugging is enabled in the Developer Options [Read further to know how?]</li>
    <li>Install drivers for your phone [Just Google '**Your phone**drivers']</li>
</ol>

To enable USB debugging [on Stock/Vanilla Android], open 'Settings App' and goto 'About Phone', and find 'Build Number' and tap on it several times until you see something like, 'You're <strong>x</strong> steps away from becoming a Developer'. Keep tapping it until you see the message 'You're a developer now' or something like that. Head back into settings and you'll see that a new section called 'Developer Options' is available now. Tap on it and scroll down a little and find 'Android Debugging' and enable it. If any warning messages pop up just ignore and hit OK. Now your phone should show up on the Android Studio Deployment Target screen.

When you select your phone and Hit OK, Android Studio should start building/compiling your app. Meanwhile if there's a pop up on your screen saying 'this PC wants to use this device for USB debugging' or something similar, just choose always allow and hit allow.

After Build/Compile is done you should see your App running on your device!

<img class="alignnone size-full wp-image-425" src="https://zocada.com/wp-content/uploads/2018/01/app_screen.png" alt="" width="503" height="813" />

Congrats! You've just build your first Android App.

&nbsp;