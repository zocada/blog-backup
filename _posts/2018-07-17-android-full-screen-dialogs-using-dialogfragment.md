---
ID: 498
post_title: >
  Android full screen dialogs using
  DialogFragment
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/android-full-screen-dialogs-using-dialogfragment/
published: true
post_date: 2018-07-17 16:35:27
---
Dialogs have always been an intuitive way of displaying quick details without having to take users to a different screen. Full-Screen dialogs give a variety of use cases for performing quick UI screens along with the power of fragments without having to fire up a separate activity. From playing videos, viewing full-screen images to even showing complex lists can be implemented with Full-Screen Dialogs for enhancing user experience.

Full-screen dialogs are created by simply extending the <a href="https://developer.android.com/reference/android/support/v4/app/DialogFragment" target="_blank" rel="noopener">DialogFragment </a> class and customizing the theme. So, Let's get started!
<h2>Creating the custom dialog layout</h2>
Let's begin by creating a simple layout to view in the fullscreen dialog (A dialog layout that takes full width and height of the device screen). <code>res/layouts/layout_full_screen_dialog.xml</code>
<script src="https://gist.github.com/haxzie/453a26c02e496fb9a97821c7eee6bde7.js?file=layout_full_screen_dialog.xml"></script>

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


<h2>Creating custom styles for the dialog</h2>
<p>
We need to customize the appearence of the dialog fragment to be viewed as full-screen and to remove the default padding around the dialog. Let's create an entry in the <code>res/values/styles.xml</code> file as follows.
<script src="https://gist.github.com/haxzie/453a26c02e496fb9a97821c7eee6bde7.js?file=styles.xml"></script>
</p>
<h2>Creating the FullScreenDialog class</h2>
<p>
Next we need to create the <code>FullScreenDialog</code> class by extending the android-support-v4 <code>DialogFragment</code>. Let's create a new file called as <code>FullScreenDialog.java</code>.
</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">
public class FullScreenDialog extends DialogFragment {

}
</pre>
<p>In the <code>onCreate()</code> method of the class let's initialize the dialog styles
<pre class="EnlighterJSRAW" data-enlighter-language="java">
@Override
public void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setStyle(DialogFragment.STYLE_NORMAL, R.style.FullScreenDialogStyle);
}
</pre>
Next, on the <code>onCreateView()</code> method, lets inflate the layout we created and initialize the toolbar with a close button to dismiss the dialog.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
     super.onCreateView(inflater, container, savedInstanceState);
     View view = inflater.inflate(R.layout.layout_full_screen_dialog, container, false);

     Toolbar toolbar = view.findViewById(R.id.toolbar);
     toolbar.setNavigationIcon(R.drawable.ic_close_white_24dp);
     toolbar.setNavigationOnClickListener(view1 -> cancelUpload());
     toolbar.setTitle("My Dialog");

     return view;
}
</pre>
Once the dialog is being created, we'll be able to use the <code>getDialog()</code> method and set the window width and height to device screen width and height. Add the followinf lines into the onStart method of the class.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
@Override
public void onStart() {
     super.onStart();
     Dialog dialog = getDialog();
     if (dialog != null) {
         int width = ViewGroup.LayoutParams.MATCH_PARENT;
         int height = ViewGroup.LayoutParams.MATCH_PARENT;
         dialog.getWindow().setLayout(width, height);
     }
}
</pre>


<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="6336781322"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

Once you have done this, Your FullScreenDialog class is ready to roll! Now the file should look like this.
Additionally add a constant String value for tag which will be used while creating the Dialog.
<script src="https://gist.github.com/haxzie/453a26c02e496fb9a97821c7eee6bde7.js?file=FullScreenDialog.java"></script>
</p>
<h2>Launching our Dialog!</h2>
<p>
Once the dialog class, styles and layout has been wired up. We can fire up an instance of our DialogFragment from any activity or fragment. We need to have a fragment trasaction too to get things work. Add the following nuclear lauch codes inside any activity to lauch our dialog.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
FullScreenDialog dialog = new FullScreenDialog();
FragmentTransaction ft = getFragmentManager().beginTransaction();
dialog.show(ft, FullScreenDialog.TAG);
</pre>
</p>
<p>
If we need to send data to the dialog fragment, we can do so as we send arguments to a fragment. While creating the dialog object, create a bundle with all the data we need to send and pass it to the <code>setArgument()</code> method of the FragmentDialog object.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
Bundle b = new Bundle();
b.putString("KEY", "VALUE");
b.putSerializable("KEY", OBJECT);
// or anything else

//initialize the dialog object
dialog.setArguments(b);

//create a fragmentTransaction and
//launch the dialog
</pre>
Now, for recieving the data, inside the <code>onCreate()</code> of the <code>FullScreenDialog</code> use the <code>getArgument()</code> method, which will return the bundle as is.
<pre class="EnlighterJSRAW" data-enlighter-language="java">
Bundle b = getArguments();
String name = b.getString("KEY", "DEFAULT_VALUE");
//and get whatever you have sent
</pre>
</p>

<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="5584852720"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>