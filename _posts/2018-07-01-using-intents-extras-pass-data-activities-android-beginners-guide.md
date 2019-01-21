---
ID: 217
post_title: 'Intent.putextra &#8211; How to use Intents &#038; Extras to pass data between activities?'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/using-intents-extras-pass-data-activities-android-beginners-guide/
published: true
post_date: 2018-07-01 00:02:01
---
Whenever you need data from an activity to be in another activity, you can pass data between then while starting the activities. Intents in android offer this convenient way to pass data between activities using <strong>Extras</strong>. Creating multiple activities to display contents of same properties is not an ideal solution. Instead, passing data from one activity to another and displaying related info is a better way. We can achieve other solutions using the same idea.

We'll start of with the basic concept of starting an activity from a current activity. We use <code>Intent </code>to achieve this. As the name suggests Intents are intentions to perform something. They are basically massage passed between components (Activities, Services, Broadcast receivers etc). To start an activity we'll create an object of the intent and pass it to the <code>startActivity()</code> method.
<pre class="EnlighterJSRAW" data-enlighter-language="java">/*
Creates an Intent object by giving the context
and the class of next activity to be opened
*/ 
Intent intent = new Intent(this, NewActivity.class);

//starting the activity
startActivity(intent);</pre>
&nbsp;
<h2>Using putExtra()</h2>
We can start adding data into the Intent object, we use the method defined in the Intent class <code>putExtra()</code> or <code>putExtras()</code> to store certain data as a key value pair or <strong>Bundle</strong> data object. These key-value pairs are known as Extras in the sense we are talking about Intents.

We'll see an example of storing a string in this Intent object using a key.
<pre class="EnlighterJSRAW" data-enlighter-language="java">//creating and initializing an Intent object
Intent intent = new Intent(this, NextActivity.class);

//attach the key value pair using putExtra to this intent
String user_name = "Jhon Doe";
intent.putExtra("USER_NAME", user_name);

//starting the activity
startActivity(intent);

</pre>
&nbsp;
<blockquote>It is a good practice to use the key as capital letters since the data received at the next activity will be eventually treated as immutable.</blockquote>
We can also use the same <code>putExtra()</code> method to attach Integers, floating point values, bytes, characters and a few other data types as listed on the official <a href="https://developer.android.com/reference/android/content/Intent.html#putExtra(java.lang.String, android.os.Bundle)" rel="noopener" target="_blank">android developers documentation</a>.
<h2>Retrieving data from intent</h2>
Once you start the activity, You'll be able to get the data attached in the next activity [or services, broadcast receivers.. etc] being started. to retrieve the data, we use the method <code>getExtra()</code> on the NextActivity from the intent.

The following example will show you how to use getExtra() on the target activity is started.
<pre class="EnlighterJSRAW" data-enlighter-language="java">//get the current intent
Intent intent = getIntent();

//get the attached extras from the intent
//we should use the same key as we used to attach the data.
String user_name = intent.getStringExtra("USER_NAME");

//if you have used any other type of data, you should use the 
//particular getExtra method to extract the data from Intet
Integer user_id = intent.getIntExtra("USER_ID");
float user_rating = intent.getFloatExtra("USER_RATING");

</pre>
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
<h2>Using Bundle to help it make easier</h2>
You should have noticed, this is a not so cool and easy way to send quite a number of items. This is where we use Bundles. Bundle is a mapping from String keys to various parcelable values. We can store any number of key-value pairs in a Bundle object and simply pass this object through the intent.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
//create a Bundle object
Bundle extras = new Bundle();

//Adding key value pairs to this bundle
//there are quite a lot data types you can store in a bundle
extras.putString("USER_NAME","jhon Doe");
extras.putInt("USER_ID", 21);
extras.putIntArray("USER_SELCTIONS", [1, 2, 3, 4, 5]);
...

//create and initialize an intent
Intent intent = new Intent(this, NextActivity.class);

//attach the bundle to the Intent object
intent.putExtras(extras);

//finally start the activity
startActivity(intent);

</pre>
It's quite the same on retrieving the bundle attached to the intent. We can use the <code>Intent.getExtras()</code> in the target activity/class to get the attached bundle and extract the data stored in it.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
//get the intent in the target activity
Intent intent = getIntent();

//get the attached bundle from the intent
Bundle extras = intent.getExtras();

//Extracting the stored data from the bundle
String user_name = extras.getString("USER_NAME");
Integer user_id = extras.getInt("USER_ID");
...
...
</pre>
<h2>Passing Objects as serializable</h2>
We can also pass Java class objects through bundles, maybe an ArrayList, HashMap, or any type of object, we can serialize in one end get it at the other end.
To put an object to a bundle, we use <code>putSerializabel("KEY", OBJECT)</code>
<pre class="EnlighterJSRAW" data-enlighter-language="java">Bundle bundle = new Bundle;
bundle.putSerializable("KEY", YOUR_OBJECT);
intent.putExtras(bundle);
</pre>
To retrieve this object, in the target activity, we simply get the serializable and assign it to an object of same type by typecasting the return value of <code>getSerializable("KEY", DEFAULT)</code>
<pre class="EnlighterJSRAW" data-enlighter-language="java">Intent intent = this.getIntent();
Bundle bundle = intent.getExtras();

//Type object = (Type) bundle.getSerializable("KEY");
DataClass myData = (DataClass) bundle.getSerializable("MY_DATA");
//we can send ArrayList, HashMaps or any serializable objects
//Use the Type of the object instead of DataClass
//in the ablove example
</pre>
Hope you have understood how to use store and extract data into intents using Extras. For further information you can visit the official android developer website for learning more about <a href="https://developer.android.com/reference/android/content/Intent.html" rel="noopener" target="_blank">Intents</a>, <a href="https://developer.android.com/reference/android/content/Intent.html#putExtra(java.lang.String, android.os.Bundle)" rel="noopener" target="_blank">putExtra</a>, and <a href="https://developer.android.com/reference/android/os/Bundle.html" rel="noopener" target="_blank">Bundles</a>. Comment down below if you ran into any error, we're happy to help.

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