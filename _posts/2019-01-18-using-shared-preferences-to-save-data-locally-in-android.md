---
ID: 457
post_title: >
  Using Shared Preferences to save data
  locally in Android
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/using-shared-preferences-to-save-data-locally-in-android/
published: true
post_date: 2019-01-18 06:52:20
---
<p>Persistent storage of data is necessary for almost all android application. From saving tiny bits of data to recognize the user to settings and preferences within the app. Android provides a consistent way of storing simple data in the internal storage privately for each application. In this article, we'll look into how to store and retrieve data in android using <code>SharedPreferences</code>. SharedPrefs are intended to save <b>Key-Value</b> pairs in storage and Android doesn't recommend saving confidential information in shared preferences without proper security. We'll also look into a library which will help us to encrypt the data while saving locally.</p>

<!-- HEADING 2 -->
<h2>Shared Preferences</h2>
<p>SharedPreferences API in Android provides required methods to save and retrieve small key-value paired data in android. The SharedPreferences class gives you an object which points to a local file which will be used to store the data through the API. These files are usually stored inside the App Data subdirectory of your application's installation location. Android leverages the functionalities of XML to save these key-value pairs easily in these files. SharedPreferences files can be either private or shared among other applications.</p>

<!-- HEADING 2 -->
<h2>Writing data into SharedPreferences</h2>
<p>We'll take a quick example of writing a username to SharedPreferences. First, we need to create an object of SharedPreferences with a Unique key which we'll be using to save the data. Let's call this <code>PREFERENCE_FILE_KEY</code></p>

<pre class="EnlighterJSRAW" data-enlighter-language="java">private final String PREFERENCE_FILE_KEY = "myAppPreference";</pre>
<p>It's a good practice to store these key strings in strings.xml of your app and retrieve them using <code>getString(R.string.preference_file_key)</code> since these keys will remain same for accessing the saved data anywhere in your application.</p>

<h3>1. Creating a SharedPreferences file </h3>
<p>We can either create a new SharedPreference file or access an existing shared preferences file using the <code>getSharedPreferences()</code> with any Context in your App.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">Context context = getActivity();
SharedPreferences sharedPref = context.getSharedPreferences(
        PREFERENCE_FILE_KEY, Context.MODE_PRIVATE);</pre>
<p>In Kotlin, it'll look like this</p>
<pre class="EnlighterJSRAW" data-enlighter-language="kotlin">val sharedPref = activity?.getSharedPreferences(
        PREFERENCE_FILE_KEY, Context.MODE_PRIVATE)</pre>

<h3>2. Create a SharedPreferences Editor</h3>
<p>To write data into the shared preferences, we need to use an object of `SharedPreferences.Editor` class.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">Editor editor = sharedPref.edit();</pre>

<h3>3. Write and commit new data</h3>
<p>We need to have a key to any data we enter into shared preferences. It's a good practice to keep all your keys in <code>strings.xm</code> or creating a <code>final</code> variable in a shared static class.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">private static final KEY_USERNAME = "prefUserNameKey"; //anything as u prefer
// ...
editor.putString(KEY_USERNAME, "My UserName");
editor.commit();
</pre>
<p>Alternatively, you can also use <code>editor.apply()</code> where the data is first written into the memory and then written into the storage asynchronously, <code>editor.commit()</code> directly writes to storage synchronously.<br/> If you are using Kotlin, step 2 can be combined with 3 as below.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="kotlin">
with (sharedPref.edit()) {
    putInt(KEY_USERNAME, "My UserName")
    commit()
}
</pre>

<!-- AD -->
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

<h2>Reading Data from SharedPreferences</h2>
<p>We can use the <code>getString()</code> method in the <code>SharedPreferences</code> to read data from the saved preference file.</p>
<h3>1. Open the SharedPreference file</h3>
<p>Using the <code>getSharedPreferences()</code> with a Context, we can open an existing preference file by providing the KEY we used to create. In our case, it is the <code>PREFERENCE_FILE_KEY</code> variabe which holds the key.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">
SharedPreferences sharedPref = getActivity().getSharedPreferences(PREFERENCE_FILE_KEY, Context.MODE_PRIVATE);

</pre>
<p>In Kotlin:</p>
<pre class="EnlighterJSRAW" data-enlighter-language="kotlin">
val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE) ?: return
</pre>

<h3>2. Read the data using SharedPreferences getters</h3>
<p>There are numerous getters defined in SharedPreferences class to get the appropriate data you saved in preferences. We should use the getter which complies to the data type of the data we stored in the prefs. In our case, since the username is a String, we can use <code>getString()</code> method.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">
String username = sharedPref.getString(KEY_USERNAME, defaultValue);
</pre>
<p>Note that, we need to specify a <code>defaultValue</code> into the <code>getters</code> in case the data we are trying to retrieve does not exist, and the defaultValue will be used as a fallBack.</p>

<h2>Encrypting SharedPreference Data using HAWK</h2>
<p>Hawk is a handy library for Android which works similar to SharedPreferences but not quite similar to it. Hawk can encrypt your data before moving into the local storage, thus preventing from others accessing the data. This can be used to store confidential information into local storage by encrypting it. You can visit the <a href="https://github.com/orhanobut/hawk" rel="noopener" target="_blank">official repository of HAWK</a> to learn more about it.</p>
<h3>1. Add Hawk to your app's build.gradle</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="java">
implementation "com.orhanobut:hawk:2.0.1"
</pre>
<h3>2. Initialize Hawk</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="java">
Hawk.init(context).build();
</pre>
<h3>3. Read and Write data using Hawk</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="java">
// To save data
Hawk.put(key, T);

// To read data
T value = Hawk.get(key);

// To delete a stored data
Hawk.delete(key);

// Check if a key exists
Hawk.contains(key);

// Count all the data stored
Hawk.count();

// Delete all the stored data
Hawk.deleteAll();
</pre>

<!-- AD -->
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