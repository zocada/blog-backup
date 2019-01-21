---
ID: 521
post_title: >
  Compress, resize and manage images using
  JavaScript directly from the browser
author: Chaman
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/compress-resize-images-javascript-browser/
published: true
post_date: 2018-07-25 05:23:07
---
<!-- wp:html -->
<p>You might be working on a project which has an image upload feature that takes images from the user and uploads it to your storage server. Once you have implemented it then you start thinking of optimizing it, so different factors like the format, quality, resolution, size of the image etc... come into consideration.</p>
<p>Later you decide to compress the images to save your storage space, so you implement an image compression feature in the back-end. Now you have saved your storage space. Don't stop there because you can optimize more, save more resources like bandwidth and CPU cycles. If you have a server with limited resources and has many tasks to run then you are just adding more CPU load.</p>
<p>What if you can save your storage space, bandwidth and reduce server load at the same time. Yes, it is possible, the answer is "Compression at the client side using JavaScript". Now let's implement it.</p>
<p>Take advantage of the HTML5&nbsp; Canvas that is used to draw graphics on a web page. Canvas is just a container for your graphics, JavaScript is used to draw.</p>
<p>
<script src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js" async=""></script>
<br><ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins><br>
<script><br />
     (adsbygoogle = window.adsbygoogle || []).push({});<br />
</script>
</p>
<h3>Steps:</h3>
<ul>
<li>Create an instance of JavaScript FileReader API.<br><code>const reader = new FileReader();</code></li>
</ul>
<ul>
<li>Read the input image using FileReader.<br><code>reader.readAsDataURL(sourceImage);</code></li>
</ul>
<ul>
<li>Create an instance of Image.<br><code>const img = new Image();</code></li>
</ul>
<ul>
<li>Set the result of the FileReader as source for the image.<br><code>img.src = event.target.result;</code></li>
</ul>
<ul>
<li>Create a HTML5 Canvas element<br><code>const elem = document.createElement('canvas');</code></li>
</ul>
<ul>
<li>Set the width and height of the canvas to match the new dimensions of the image.
<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-linenumbers="false">elem.width = width;
elem.height = height;</pre>
</li>
<li>Create an object that is used to draw graphics on the canvas.<br><code>const ctx = elem.getContext('2d')</code></li>
</ul>
<p>The <code>getContext()</code> method returns an object with the properties and methods required for drawing graphics on the canvas. The '<code>2d</code>' parameter limits us for drawing only 2D graphics.</p>
<ul>
<li>Now draw the image on the canvas by specifying the position, width and height of the image.<br><code>ctx.drawImage(img, 0, 0, width, height);</code></li>
<li>Export the canvas as a blob or DataURL by specifying MIME type, image quality.
<pre class="EnlighterJSRAW" data-enlighter-language="js">const data = ctx.canvas.toDataURL(img, mime, quality);</pre>
<p style="text-align: center;">or</p>
<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-linenumbers="false">ctx.canvas.toBlob((blob) =&gt; {
    console.log(blob); //output image as a blob
    const file = new File([blob], fileName, {
        type: mime,
        lastModified: Date.now()
    }); //output image as a file
}, mime, quality);</pre>
<p><code>mime</code> is the "mime type" of the image, like 'image/jpeg', 'image/png' .</p>
<p>Value of <code>quality</code> ranges from 0 to 1. It is the quality of the output image. If you don't specify the <code>mime</code> and <code>quality</code> in the <code>toBlob()</code> method then default quality will be set and the mime type will be 'image/png'.</p>
</li>
</ul>
<blockquote>
<p><ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="6336781322"></ins><br>
<script><br />
     (adsbygoogle = window.adsbygoogle || []).push({});<br />
</script>
</p>
<h4>The final code</h4>
</blockquote>
<p>
<script src="https://gist.github.com/chaman-k/a64fcd49c9e1c0b6a41074fdecf0e5d0.js"></script>
</p>
<h3>Note:</h3>
<p>If you want to maintain the aspect ratio of the output image then you can set either the width or height as constant and calculate the other dimension.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="js">const width = 600;
const scaleFactor = width / img.width;
elem.width = width;
elem.height = img.height * scaleFactor;

ctx.drawImage(img,&nbsp;0,&nbsp;0,&nbsp;width,&nbsp;img.height * scaleFactor);</pre>
<p>Here we kept <code>width</code> as constant and calculated the scaling factor. To find the relative height just multiply the scaling factor to the original height.</p>
<h2 style="text-align: center;">For Angular using RxJS</h2><p><script src="https://gist.github.com/chaman-k/f5b1a4a4779e8ffd20995727f0c9a640.js"></script></p>
<p><ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="5584852720"></ins><br>
<script><br />
     (adsbygoogle = window.adsbygoogle || []).push({});<br />
</script>
</p>
<!-- /wp:html -->