---
ID: 715
post_title: >
  Best image loading libraries for android
  analyzed
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/best-image-loading-libraries-android-analyzed/
published: true
post_date: 2019-01-05 17:43:36
---
<p>Working with images is one of the unavoidable parts of android application development. Maybe it's from the local storage or from the internet, loading images into views need to be efficient so as fewer resources are being used. From retrieving image contents from the web to caching them for delightful user experience, android image loading libraries come in handy to make the job easier. In this post, we'll take a look some of the most common and the best android libraries that can be used to load images faster and efficiently.</p>

<!-- wp:heading -->
<h2>1. Glide</h2>
<!-- /wp:heading -->

<!-- wp:image {"id":752} -->
<figure class="wp-block-image"><img src="https://zocada.com/wp-content/uploads/2019/01/glide_logo.png" alt="" class="wp-image-752"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><a href="https://github.com/bumptech/glide">Glide</a> takes the no. 1 spot among the image loading libraries available today and is the <g class="gr_ gr_3 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del" id="3" data-gr-id="3">goto</g> library when it comes to image caching and other cool features this library provides. <a href="https://bumptech.github.io/glide/">Glide</a> is an open source project developed by BumpTech and is currently at is v4 release. From the GitHub <g class="gr_ gr_110 gr-alert gr_gramm gr_inline_cards gr_run_anim Punctuation only-ins replaceWithoutSep" id="110" data-gr-id="110">page</g> we can see the description as.</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>Glide is a fast and efficient image loading library for Android focused on smooth scrolling. Glide offers an easy to use API, a performant and extensible resource decoding pipeline and automatic resource pooling.</p><cite><a href="https://bumptech.github.io/glide/">bumptech/glide</a></cite></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Glide wins the heart with it's easy to use API and powerful one liners which helps in doing more in a single line of code.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">Glide.with(fragment)
    .load(url)
    .into(imageView)
</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>To use Glide, simply add the following lines of code into the dependencies of your app <g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="4" data-gr-id="4">level </g><code>build.gradle</code><g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="4" data-gr-id="4"> file</g>.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">dependencies {
  implementation ("com.github.bumptech.glide:glide:4.8.0") {
    exclude group: "com.android.support"
  }
  implementation "com.android.support:support-fragment:26.1.0"
}
</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>Glide provides additional features of cropping the image while loading into an ImageView and is one of the few libraries which supports loading GIFs into ImageViews. Here's a quick example on how to use Glide to load an image with the circular crop. You can learn more about Glide and it's all other features from <g class="gr_ gr_14 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling multiReplace" id="14" data-gr-id="14">it's</g> <a href="https://bumptech.github.io/glide">official docs.</a></p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">RequestOptions options = new RequestOptions();
options.centerCrop();

Glide.with(fragment)
    .load(url)
    .apply(options)
    .into(imageView);
</pre>
<!-- /wp:html -->

<!-- wp:html -->
<p><script async="" src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script><br><ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins><br><script><br />
     (adsbygoogle = window.adsbygoogle || []).push({});<br />
</script></p>
<!-- /wp:html -->

<!-- wp:heading -->
<h2>2. Picasso</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><a href="http://square.github.io/picasso/">Picasso</a> is also one of the most popular libraries out there which <g class="gr_ gr_3 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Grammar multiReplace" id="3" data-gr-id="3">is</g> known for the speed and great caching abilities in android. <a href="http://square.github.io/picasso/">Picasso</a> is open source and is developed by Square Inc, a company known for it's awesome contributions to the Android community. Picasso automatically handles image recycling and download cancellation when used with recycler adapters, and makes complex transformations possible with lower memory footprint. One benefit over Glide would be the smaller library size which makes Picasso extremely light weight.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can easily add Picasso into your project by simply adding the following lines into your <code>build.gradle</code> file.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">implementation 'com.squareup.picasso:picasso:2.71828'</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>You can now start using Picasso in your application by a simple syntax to load image into ImageViews.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">Picasso.get()
    .load(url)
    .into(imageView);
</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>Picasso also supports using placeholders for images, while they are loading and when any error occurs during loading of the provided image. You can learn more about Picasso from the <a href="http://square.github.io/picasso/">official docs of Picasso</a> by Square.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">Picasso.get()
    .load(url)
    .placeholder(R.drawable.user_placeholder)
    .error(R.drawable.user_placeholder_error)
    .into(imageView);
</pre>
<!-- /wp:html -->

<!-- wp:html -->
<p><script async="" src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script><br><ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins><br><script><br />
     (adsbygoogle = window.adsbygoogle || []).push({});<br />
</script></p>
<!-- /wp:html -->

<!-- wp:heading -->
<h2>3. Fresco</h2>
<!-- /wp:heading -->

<!-- wp:image {"id":767} -->
<figure class="wp-block-image"><img src="https://zocada.com/wp-content/uploads/2019/01/Screenshot_2019-01-05-Fresco-An-image-management-library--1024x305.png" alt="" class="wp-image-767"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>This powerful library developed by the good folks at <a href="https://facebook.com">Facebook</a> is a full-fledged image loading library with great features. <a href="https://frescolib.org/">Fresco</a> supports out of the box image loading with variable placeholders and it also supports streaming of progressive JPEGs, display of animated GIFs and WebPs, extensive customization of image loading and display and many more. One of the great features of Fresco is that it uses both Main memory and storage memory for caching which increases the performance of the application.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To use Fresco in your project, simply add the following <g class="gr_ gr_3 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="3" data-gr-id="3">dependecy</g> into your app <g class="gr_ gr_5 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="5" data-gr-id="5">level </g><code>build.gradle</code><g class="gr_ gr_5 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="5" data-gr-id="5"> file</g>.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">implementation 'com.facebook.fresco:fresco:1.11.0'</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>Unlike the other libraries mentioned above, Fresco needs to be initialized once from the Application class of your project.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">// MyApplication.java
public class MyApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        Fresco.initialize(this);
    }
}
</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>Since all the features provided by this library comes in a large library size, to leverage the full benefit of the library we need to use the SimpleDraweeView class item in the View of your layout. As the official API docs of the library suggest...</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="xml" >
<com.facebook.drawee.view.SimpleDraweeView
    android:id="@+id/my_image_view"
    android:layout_width="130dp"
    android:layout_height="130dp"
    fresco:placeholderImage="@drawable/my_drawable"
    />
</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>And then in the Java file associated to the layout, we can easily load the image using the following code. </p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<pre class="EnlighterJSRAW" data-enlighter-language="java">Uri uri = Uri.parse(url);
SimpleDraweeView draweeView = (SimpleDraweeView) findViewById(R.id.my_image_view);
draweeView.setImageURI(uri);
</pre>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>For more details on Fresco and how to use all the rich features it offers, visit the <a href="https://frescolib.org/docs/">official docs.</a></p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p><script async="" src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script><br><ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins><br><script><br />
     (adsbygoogle = window.adsbygoogle || []).push({});<br />
</script></p>
<!-- /wp:html -->

<!-- wp:heading -->
<h2>Conclusion<br></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>While Glide and Fresco <g class="gr_ gr_11 gr-alert gr_gramm gr_inline_cards gr_run_anim Grammar multiReplace" id="11" data-gr-id="11">provides</g> really fast image loading compared to Picasso. These libraries are really large in size compared to the tiny size of Picasso. Glide comes packed with all the necessary features and it's easy extend-ability to create custom loaders easily helps it have an upper hand from Fresco. Glide has a fairly simple syntax and API structure while Fresco's API might seem to be of extra work and confusing. All the <g class="gr_ gr_250 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling multiReplace" id="250" data-gr-id="250">above mentioned</g> libraries <g class="gr_ gr_259 gr-alert gr_gramm gr_inline_cards gr_run_anim Grammar multiReplace" id="259" data-gr-id="259">comes</g> with <g class="gr_ gr_283 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="283" data-gr-id="283">built in</g> support for WebP images, <g class="gr_ gr_359 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del" id="359" data-gr-id="359">where as</g> <g class="gr_ gr_445 gr-alert gr_gramm gr_inline_cards gr_run_anim Grammar only-ins replaceWithoutSep" id="445" data-gr-id="445">only</g> Glide seems to have an out of the box performance when working with animated images and GIFs.<br></p>
<!-- /wp:paragraph -->