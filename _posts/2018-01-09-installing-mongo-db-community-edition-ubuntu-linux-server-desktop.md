---
ID: 196
post_title: 'Installing MongoDB community edition on Ubuntu [desktop/server]'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/installing-mongo-db-community-edition-ubuntu-linux-server-desktop/
published: true
post_date: 2018-01-09 23:23:05
---
MongoDB is a free and open-source NoSQL document-oriented database program designed for high volume data storage and management. It stores data as JSON-like documents as schemas and is one of the fastest database program out there. MongoDB is designed and developed by <a href="https://mongodb.com" target="_blank" rel="noopener">MongoDB Inc</a> in 2009, since then the open-source community crafted it to be one of the fastest leading technology in the data industry and is well known for its faster data access and easier NoSQL support.
<h2>Installing MongoDB 3.6 in Ubuntu</h2>
We'll be installing MongoDB 3.6 community edition in Ubuntu. Follow the instructions carefully step by step to complete the installation.
Get your ubuntu system ready and fire up a terminal by pressing <code>ctrl + alt + T</code>.
<ol style="list-style:none;margin-left: 0; padding-left: 0;">
 	<li>
<h3>1. Importing the public key used by the Ubuntu package management system</h3>
The Ubuntu package management tools ensure package consistency and authenticity by requiring that distributors sign packages with GPG keys. Paste the following command into your terminal to import the MongoDB public GPG Key.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5</pre>
&nbsp;
</li>
<li>
<h3>2. Create a list file for MongoDB</h3>
Create the list file <code>mongodb-org-3.6.list</code> in the directory <code>/etc/apt/sources.list.d/</code> using the following command.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list</pre>
&nbsp;
</li>
<li>
<h3>3. Update the local package database</h3>
The following command will download the package lists from the repositories and "updates" them to get information on the newest versions of packages and their dependencies.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo apt-get update</pre>
&nbsp;
</li>
<li>
<h3>4. Install the MongoDB packages</h3>
Type the following command in the terminal to install the latest stable version of MongoDB in your computer.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo apt-get install -y mongodb-org</pre>
&nbsp;
Once the installation completes. type the following command to ensure MongoDB was successfully installed.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongo --version</pre>
&nbsp;
you should get the latest version number of the installed MongoDB shell as output.
</li>
</ol>
<h2>Running MongoDB</h3>
Type the following command to start the MongoDB server in the default port 27017.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongod</pre>
<strong>OR</strong>
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo service mongod start</pre>

You should be able to see the log data and in there you can see the port it is running on.

<a href="https://zocada.com/wp-content/uploads/2018/01/mongo_terminal.png"><img src="https://zocada.com/wp-content/uploads/2018/01/mongo_terminal.png" alt="" width="783" height="434" class="alignnone size-full wp-image-269" /></a>

PS: Don't worry if the service start process shows any error, it might be probably because the <code>mongod</code> service will be already running in the same port. 

Continue to set up your MongoDB admin and user accounts on our next post.
<a href="https://zocada.com/setting-up-mongodb-users-beginners-guide/" rel="noopener" target="_blank">Getting Started with MongoDB - Setting up admin and user accounts.</a>