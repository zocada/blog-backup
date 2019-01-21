---
ID: 528
post_title: 'Android &#8211; Integrating Fingerprint authentication in your apps'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/android-integrating-fingerprint-authentication-apps/
published: true
post_date: 2018-07-23 17:40:08
---
Fingerprint authentication has been a huge leap towards a better user experience in smartphones. Having this golden feature in your user's phone and trying to integrate this feature in your applications to increase security and the bonus of better user experience is worth a shot. Let's see how we can quickly integrate a simple FingerPrint authentication into an android app.

While integrating Fingerprint auth in our applications, we need to take care of quite a lot of things concerning the hardware of the device our users are using. We know that only devices running android Marshmallow and above have support for Fingerprint scanners. Additionally to use the Android's built-in Fingerprint features the user needs to have enabled fingerprint security in the device and have at least one fingerprint registered in the device. Let's keep these points in mind and we need to check these things before dispatching a listener for fingerprint authentication.
<strong>So, Let's get started!</strong>
<h2>Permission for Fingerprint use</h2>
We need our application's manifest file to describe that our application needs permission to use <strong>Fingerprint</strong>. Let's add the following line inside the <code>manifest</code> tag inside the AndroidManifest.xml file.
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;uses-permission android:name="android.permission.USE_FINGERPRINT" /&gt;</pre>

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

<h2>Checking Fingerprint availability</h2>
As I mentioned above, we need to verify that the user runs appropriate Android version, the device has the necessary hardware for the Fingerprint scanner and the user has at least one fingerprint already registered in the device.
Write down the following method in your activity's class or create a separate java file and drop this method in there.
<script src="https://gist.github.com/haxzie/7c5578616f87d7763b82f56aa9a0c3a3.js"></script>
<h2>Creating a Fingerprint Helper class</h2>
Next, we need to create a helper class by extending the <code>FingerprintManager.AuthenticationCallback</code> and we'll create an interface inside this class for the authentication listner.
<pre class="EnlighterJSRAW" data-enlighter-language="java">@RequiresApi(api = Build.VERSION_CODES.M)
public class FingerprintHelper extends AuthenticationCallback{

    private FingerprintHelperListener listener;

    public FingerprintHelper(FingerprintHelperListener listener) {
        this.listener = listener;
    }

    //interface for the listner
    interface FingerprintHelperListener {
        void authenticationFailed(String error);
        void authenticationSuccess(FingerprintManager.AuthenticationResult result);
    }

}
</pre>
Additionally, we need to create methods to start authentication, cancel the listner and implement the methods in the <code>AuthenticationCallback</code> to interact with our listner. Now our <code>FilgerprintHelper</code> will look like this.
<script src="https://gist.github.com/haxzie/84d53762518777e0cab4124891d2266c.js"></script>
<h2>Implementing the listener in Activity</h2>
Once we have created the <code>FingerprintHelper.java</code> and the <code>FingerprintHelperListener</code> inside it, we can implement the listner in our Activity.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class LoginActivity extends AppCompatActivity implements FingerprintHelper.FingerprintHelperListener {

   //Your onCreate and other pieces of code goes here
   ...
   ...
   //You class should implement the listener and override the below two methods
    @Override
    public void authenticationFailed(String error) {
        //Authentication failed. ie user tried an invalid fingerprint
        Toast.makeText(this, "Invalid Fingeprint", Toast.LENGTH_LONG).show();
    }

    @Override
    public void authenticationSuccess(FingerprintManager.AuthenticationResult result) {
        //Yaay! we have authenticated the user using Fingerprint.
        ...
        //add your logic to continue here.
    }
}</pre>
We need to create variables of <code>FingerprintManager</code> and <code>FingeprintHelper</code> in our activity.
<pre class="EnlighterJSRAW" data-enlighter-language="java">private FingerprintHelper fingerprintHelper;
private FingerprintManager fingerprintManager;
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

Next, we'll check for the Fingerprint settings using the function <code>checkFingerprintSettings</code> we discussed above in this post and start listneing when the Activity starts and cancel the listening when the activity is paused ie. app went to background. So add the following line of code inside your activity by overriding the <code>onResume()</code> and the <code>onPause()</code> method.
<pre class="EnlighterJSRAW" data-enlighter-language="java">@RequiresApi(api = Build.VERSION_CODES.M)
@Override
protected void onResume() {
    super.onResume();
     //Check for the fingerprint permission and listen for fingerprint
     //add additional checks along with this condition based on your logic
    if (checkFingerPrintSettings(this)) {
        //Fingerprint is available, update the UI to ask user for Fingerprint auth
        //start listening for Fingerprint
        fingerprintHelper = new FingerprintHelper(this);
        fingerprintManager = (FingerprintManager) getSystemService(FINGERPRINT_SERVICE);
        fingerprintHelper.startAuth(fingerprintManager, null);
     } else {
        Log.d(TAG, "Finger print disabled due to No Login credentials or no Fingerprint");
     }
}

@RequiresApi(api = Build.VERSION_CODES.M)
@Override
protected void onPause() {
   super.onPause();
   if (fingerprintHelper != null)
       fingerprintHelper.cancel();
}</pre>
That's it! You're ready to roll with the new feature on your app. Now your Activity class should look something like this.
<script src="https://gist.github.com/haxzie/44c354c7bd89864e57bc8cd271d8f77a.js"></script>

<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="5584852720"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>