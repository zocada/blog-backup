---
ID: 128
post_title: Installing Node.js in apple macOS
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/installing-node-js-in-apple-macos/
published: true
post_date: 2018-01-07 00:37:23
---
Node.js can be easily installed by downloading the package from the <a href="https://nodejs.org">official node.js website</a>.

<a href="http://zocada.com/wp-content/uploads/2018/01/node_mac_official_website.png"><img class="alignnone size-large wp-image-130" src="http://zocada.com/wp-content/uploads/2018/01/node_mac_official_website-1024x500.png" alt="" width="770" height="376" /></a>

Open the downloaded package and follow the onscreen instructions by clicking "Continue" and agreeing to the terms of the license.

<h2>Using Package manager</h2>

use any of the following package managers installed on your system to install node.js on the go.
<ul>
<li>
using Homebrew:
<pre class="EnlighterJSRAW" data-enlighter-language="shell"> brew install node</pre>
</li>
<li>
Using Macports:
<pre class="EnlighterJSRAW" data-enlighter-language="shell">port install nodejs&lt;major_version_number&gt;</pre>
</li>
<li>
Using pkgsrc:
<pre class="EnlighterJSRAW" data-enlighter-language="shell">pkgin -y install nodejs</pre>
</li>
</ul>
After installation verify the version installed.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">node -v
</pre>
&nbsp;