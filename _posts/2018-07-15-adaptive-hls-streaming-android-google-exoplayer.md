---
ID: 463
post_title: 'Adaptive HLS streaming on android with Google&#8217;s ExoPlayer'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/adaptive-hls-streaming-android-google-exoplayer/
published: true
post_date: 2018-07-15 07:09:34
---
Streaming video and audio using the default media player API of Android can be a pain when it comes to adaptive streaming and customization. Google's ExoPlayer is an application level media player which provides consistent API and easy customization for playing videos both locally and over the internet. ExoPlayer supports features not currently supported by Android’s MediaPlayer API, including DASH, HLS and SmoothStreaming adaptive playbacks.

Here we'll look into integrating ExoPlayer into an android application for streaming video using HLS protocol. HLS stands for <strong>HTTP Live Streaming</strong> which resembles MPEG-DASH in that it works by breaking the overall stream into a sequence of small HTTP-based file downloads, each download loading one short chunk of an overall potentially unbounded transport stream. HLS protocol is widely used by Vimeo, Apple and other companies which provides live streaming of videos.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>


<h2>Let's get started</h2>
<p>Create a new android studio project and add make sure you have JCenter and Google repositories included in the project level <code>build.gradle</code> file.</p>
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=project%20level%20build.gradle "></script>
<p>Add these dependencies into your app level <code>build.gradle</code> file to include ExoPlayer libraries for HLS streaming.</p> 
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=app%20level%20build.gradle "></script>
<p>
Additionally if you want to use DASH or Smooth Streaming instead of HLS use the following dash module instead of hls
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=additionals%20on%20build.gradle "></script>
</p>

<h2>Customizing layout for ExoPlayer</h2>
Whether you are using an Activity, Fragment or Dialog. Insert this into the layout file of the component. Here I'll be demonstrating on an Activity's layout file.
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=layout_main_activity.xml"></script>
<p>
Additionally, I've added a progress indicator to display during initial load and buffering. In the line #14 I have included a custom layout for Exo controller. You can avoid this line if you don't want custom control customization. We need to define a layout file for customizing and give ids to the element as specified in the original Exo layout. (Hopefully, the android studio Intellisense will help you in that).
</p>
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=player_custom_controls.xml"></script>
<p>
You can specify additional TextViews in the layout for displaying current position and end time of the video with ids <code>exo_position</code> and <code>exo_duration</code>
</p>


<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="6336781322"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>


<h2>Initializing and Playing the Video</h2>
In the Activity declare the PlayerView we added in the layout as <code>private PlayerView playerView</code> and initialize it inside the onCreate method with the id of the view.
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=init%20PlayerView"></script>
Additionaly we need a few variables initialized to be used to save the player state on orientation changes and activity pause.
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=additional%20variables%20MainActivity.java"></script>

we need to initialize the ExoPlayer with the streaming URL and configurations in the <code>onStart</code> method of the activity.
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=activity%20onStart%20MainActivity.java"></script>

<h2>Cleaning Up!</h2>
We need to release the player when the activity goes to the background or is paused. Create the following method and call it inside the onStop() and onPause() method of your activity.
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=releasePlayer%20MainActivity.java"></script>
<script src="https://gist.github.com/haxzie/760f435a11cfd6015c03c81a00cd257c.js?file=onStop%20MainActivity.java"></script>

[caption id="attachment_491" align="aligncenter" width="1920"]<img src="https://zocada.com/wp-content/uploads/2018/07/Screenshot_20180715-151415.png" alt="exo_player_hls_streaming" width="1920" height="1080" class="size-full wp-image-491" /> A customized ExoPlayer with auto rotate and close buttons on toolbar.[/caption]
That's it! Your video will be playing now! For additional information on playing DASH videos visit the Google <a href="https://codelabs.developers.google.com/codelabs/exoplayer-intro/" rel="noopener" target="_blank">CodeLabs</a>, or for the documentation of the ExoPlayer visit the <a href="https://github.com/google/ExoPlayer" rel="noopener" target="_blank">GitHub</a> repository. Feel free to ask any queries in the comment section below.


<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="5584852720"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>