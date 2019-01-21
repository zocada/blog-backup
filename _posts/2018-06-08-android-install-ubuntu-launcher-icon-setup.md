---
ID: 99
post_title: 'Android studio on Ubuntu &#8211; Complete installation guide'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/android-install-ubuntu-launcher-icon-setup/
published: true
post_date: 2018-06-08 17:28:40
---
Android studio is one of the best known IDE around since <a href="https://ww.jetbrains.com" target="_blank" rel="noopener">JetBrains</a> came into the game. The IDE is powered by JetBrain's IntelliJ development environment. Ever since the development phase of android shifted from traditional eclipse based environment there have been several improvements. Android Studio has been a blessing for the developers by its vast features and ease of use for the entire development cycle of your application. Fusing it in with a Linux system brings the full power of a developer as a superuser too. we'll explain step by step guide for installing and setting up Android studio on <strong>Ubuntu</strong> one of the popular <strong>Linux</strong> distro out there.

<h3>Update:</h3>
<p>
With the latest version of ubuntu which comes with snap package manager, You can install Android Studio using a single command.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">
sudo snap install android-studio --channel 
</pre>
Visit <a href="https://snapcraft.io/store" rel="noopener" target="_blank">snapcraft.io</a> for more awesome apps for your Ubuntu desktop.

</p>

<h3>Old Method</h3>
<h3>Step 1: Downloading Android Studio [zip]</h3>
The official android developers website provides the latest stable version of android studio to download. Goto <a href="https://developer.android.com/studio/index.html" target="_blank" rel="noopener">developer.android.com</a>, accept the terms and conditions and download the zip file.

<h3>Step 2: Extracting the files</h3>
Once the download is completed, open the ZIP file and extract the <code>android-studio</code> folder to a local directory.

When the files are successfully extracted, open a terminal and <code>cd</code> into the folder or open the folder <code>android-studio</code> and right-click -&gt; Open in terminal. now type the following command to open Android studio.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">cd bin
./studio.sh</pre>
&nbsp;
wait a few seconds, and you'll see the android studio loading screen. For ease of use you can create a launcher application on to your navigation pane. Follow the instruction below to do that.

<h3>step 3: Creating a launcher for Android Studio</h3>

Fire up a terminal and <code>cd</code> into the android studio folder or open the extracted <code>android-studio</code> folder using file manager and right-click -> open in terminal in an empty space.

now we need to create a launcher file with required details about android studio. Make sure your terminals current directory is in <code>android-studio/bin/</code> folder, then type the following command to open <code>GEdit</code>.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">gedit androidstudio.desktop</pre>
&nbsp;
this will open GEdit with blank file ready to edit, copy paste the following lines in to the file and save it.

<script src="https://gist.github.com/haxzie/21126332898492f5316a86ff1d7d04e5.js"></script>
&nbsp;
Make sure to add the complete directory path of your <code>android-studio</code> folder instead of <...> and save and close GEdit.
your androidstudio.desktop file should look something like this after adding the directory path.


Once its done, open the <code>android-studio</code> folder using file manager and open the <code>bin</code> folder and you'll see the following contents in it. Now you can double-click on the <strong>Android Studio</strong> application icon to launch android studio, Or simple click and drag the icon to your Navigation/Launcher pane for quick access.


That's it. You have done Installing Android studio. If anything goes wrong feel free to comment down below and we'll get back to you soon.