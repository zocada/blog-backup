---
ID: 451
post_title: >
  A brief intro to RxKotlin/RxJava on
  Android
author: Rumaan
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/brief-intro-rxkotlin-rxjava-android/
published: true
post_date: 2018-10-28 13:02:41
---
<h3>RxJava? What is it?</h3>
RxKotlin/RxJava provides an easy and efficient way to handle <em>asynchronous</em> <em>stream</em> of data in programs running on Java Virtual Machine (JVM).

Some examples of asynchronous events can be Network Requests, Touch Input Events etc.

<strong>Rx </strong>in <a href="https://github.com/ReactiveX/RxKotlin">RxKotlin</a> stands for <em>Reactive Extensions. </em>

On Android when it comes to handling operations that must be done off the UI thread there are a lot of options like AsyncTask, Loaders, JobDispatcher etc.
and what makes RxJava stand out is its flexibility and power of Rx Operators.

But for a novice Android Developer the terminologies and concepts used in RxJava world can be intimidating.

&nbsp;
<h4>Setting Up:</h4>
Add this to the build.gradle (app level) module file.

For RxKotlin:

<code class="EnlighterJSRAW" data-enlighter-language="raw">implementation 'io.reactivex.rxjava2:rxkotlin:x.y.z'</code>

For RxJava:

<code class="EnlighterJSRAW" data-enlighter-language="null">implementation "io.reactivex.rxjava2:rxjava:2.x.y"</code>

RxAndroid Bindings:

<code class="EnlighterJSRAW" data-enlighter-language="null">implementation 'io.reactivex.rxjava2:rxandroid:2.1.0'</code>

<hr />

Here are the <em>three</em> important terms that you would come across in <strong><em>Rx</em></strong> World:

1. Observers/Subscribers
2. Observables/Flowables
3. Operators
<h3><em><strong>Observer/Subscriber:</strong></em></h3>
It is someone that observers or requires the data/event from.
It is someone who subscribes to the observable

<center>
<img src="https://cdn.memegenerator.es/imagenes/memes/full/2/16/2162653.jpg" alt="memegenerator.es" border="0" /></center>
<h3><em><strong>Observable/Flowable:</strong></em></h3>
Is someone/something that emits/produces a stream(<em>s</em>) data which can be observed by the Observer/Subscriber who subscribes to it.

<center>
<img class="size-full aligncenter" src="https://i.pinimg.com/236x/8d/76/96/8d7696dcb0d92d078925f6b66c5a147a--fringe-quotes-the-observer.jpg" alt="Observable Person" width="198" height="254" /></center>

[caption id="attachment_576" align="aligncenter" width="1068"]<img class="wp-image-576 size-full" src="https://zocada.com/wp-content/uploads/2018/07/carbon.png" alt="Observables" width="1068" height="426" /> Creating simple Observables[/caption]

Here's how you would make a simple observable that emits/produces <em>3</em> integers:

Here's how you would create a Flowable from a list:
<h3><img class="aligncenter size-full wp-image-584" src="https://zocada.com/wp-content/uploads/2018/07/carbon-2.png" alt="" width="1168" height="510" /></h3>
<h3><strong><em>Operators:</em></strong></h3>
Operations that can be performed on the stream of data or observables themselves.

<img class="aligncenter size-full" src="https://images3.memedroid.com/images/UPLOADED399/5761f07014113.jpeg" width="888" height="499" />

&nbsp;

Some Operators on Observables:

[caption id="attachment_585" align="aligncenter" width="1404"]<img class="wp-image-585 size-full" src="https://zocada.com/wp-content/uploads/2018/07/carbon-1.png" alt="Rx Operators" width="1404" height="888" /> Operators usage and chaining[/caption]

To learn more on Operators, check out Rx Marbles (link below)

&nbsp;

Reference Links:
<ul>
 	<li><a href="https://github.com/ReactiveX/RxKotlin">RxJava (Github)</a></li>
 	<li><a href="https://youtu.be/XLH2v9deew0">Intro to RxJava by Christina Lee</a></li>
 	<li><a href="https://github.com/ReactiveX/RxKotlin">RxKotlin (Github)</a></li>
 	<li><a href="http://rxmarbles.com/">Rx Marbles </a></li>
 	<li><a href="https://proandroiddev.com/exploring-rxjava-in-android-e52ed7ef32e2">Exploring RxJava (my favorite article where I learn RxJava from)</a></li>
</ul>
&nbsp;