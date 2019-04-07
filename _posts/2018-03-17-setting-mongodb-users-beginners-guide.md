---
ID: 208
post_title: 'Getting Started with MongoDB &#8211; Setting up admin and user accounts'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/setting-mongodb-users-beginners-guide/
published: true
post_date: 2018-03-17 13:22:01
---
Setting up the <strong><a href="https://www.mongodb.com/" target="_blank" rel="noopener noreferrer">MongoDB</a> </strong>client we installed on our system is really an easy task. Hope you have a fresh install ready for your system, or please follow our <a href="https://zocada.com/installing-mongo-db-community-edition-ubuntu-linux-server-desktop/" target="_blank" rel="noopener noreferrer">instructions on installing <strong>MongoDB</strong></a>. As we know MongoDB is a powerful NoSQL document-oriented database program. It is designed for high volume data storage and management. So, we'll start off our setup process by starting up the <code>mongod</code> in a separate terminal.

Type in the following command to start the process.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongod</pre>
or
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo service mongod start</pre>
You will be able to see some of the log messages on the screen similar to this. <em>Don't worry if it shows any error, it is because most probably the service will be already running on the same port.</em>

[caption id="attachment_438" align="alignnone" width="783"]<img class="size-full wp-image-438" src="https://zocada.com/wp-content/uploads/2018/01/0_C_zZjIr7vx2jSXR0.png" alt="mongod-shell" width="783" height="434" /> Starting mongod process[/caption]

&nbsp;

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
<h2>Getting started with Mongo Shell</h2>
Once you made sure that MongoDB is running, we can jump into the mongo shell for further configurations and operations. We can start the mongo shell and connect to the running instance if MongoDB in the same system. So, <strong>what is a Mongo shell?</strong>
<blockquote>The mongo shell is an interactive JavaScript interface to MongoDB. You can use the mongo shell to query and update data as well as perform administrative operations. <a href="https://docs.mongodb.com/manual/mongo/" target="_blank" rel="noopener noreferrer">[mks_icon icon="fa-share-square-o" color="#4bd5f4" type="fa"]</a></blockquote>
To start the Mongo Shell, simply type the following command on a new terminal.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongo</pre>
You will see a few messages including the current MongoDB and Mongo Shell version and prompt <code>&gt;</code> waiting for any commands.

[caption id="attachment_439" align="alignnone" width="800"]<img class="size-full wp-image-439" src="https://zocada.com/wp-content/uploads/2018/01/0_IYua7xgQ0w23w2yF.png" alt="mongo-shell" width="800" height="271" /> Mongo Shell[/caption]

Now, we'll start off by creating users and restricting unauthorized access to our database. Since we already started the <code>mongod</code> service without access control [default], we can continue to the next step.
<h2>Creating the user Administrator</h2>
We need to create an admin user in the <code>admin</code> database with <code>userAdminAnyDatabase</code> privilege. To do this we'll first use the <code>admin</code> database. Use the following code in the mongo shell to use the admin database, if the database doesn't exist, MongoDB will create the particular database and use it.
<pre class="EnlighterJSRAW" data-enlighter-language="js">use admin</pre>
<em>make sure you get the message stating <code>Switched to db admin</code></em>

Now, we'll use the <code>createUser()</code> function to create an admin user. Type the following command in the mongo shell to create the admin user.
<pre class="EnlighterJSRAW" data-enlighter-language="js">db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
</pre>
[caption id="attachment_440" align="alignnone" width="634"]<img class="size-full wp-image-440" src="https://zocada.com/wp-content/uploads/2018/01/0_MzYqdfSoLRLZewRz.png" alt="creating-user-admin-mongo" width="634" height="329" /> Creating user admin[/caption]

Once we finish creating the userAdministrator we can start the mongod instance with access control. Now close the shell by typing <code>exit</code>. Then restart the mongod instance using the following command in the terminal after closing the running instance on the other terminal using <code> ctrl + C </code>.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongod --auth --port 27017</pre>
Fire up the mongo shell in another terminal using the following command to authenticate as user administrator.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongod --port 27017 -u "myUserAdmin" -p "abc123" --authenticationDatabase "admin"</pre>
The userAdministrator user has only permission to create and manage the database users. If you try to read or write in the database using userAdministrator user MongoDB will return an error. So, we need to create additional users with roles to read and write on the database.

<ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="6336781322"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
<h2>Creating database users</h2>
We'll start off by creating a test database, using the following code in mongo shell.
<pre class="EnlighterJSRAW" data-enlighter-language="js">use test</pre>
<em>As I said earlier, if we use the above code, MongoDB will create the "test" database if it doesn't exist and switches to that DB.</em>

We can use the <code>db.createUser()</code> function to create an user for this db. Note that, the keyword <code>db</code> referes to the current db we are working on. In this case its the "test" db we switched earlier to.
<pre class="EnlighterJSRAW" data-enlighter-language="js">db.createUser(
  {
    user: "testUser",
    pwd: "xyz123",
    roles: [ { role: "readWrite", db: "test" } ]
  }
)
</pre>
[caption id="attachment_441" align="alignnone" width="765"]<img class="size-full wp-image-441" src="https://zocada.com/wp-content/uploads/2018/01/0_c2-KYWX4321C50ie.png" alt="creating-user-mongo" width="765" height="502" /> Creating user in test DB[/caption] 

We can now log in to the database as the "testUser" with read and write access to the "test" DB. Close the current mongo shell instance by using <code>exit</code> command and type the following command in the terminal.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">mongo --port 27017 -u "testUser" -p "xyz123" --authenticationDatabase "test"
</pre>
To view the current DB you are working in, use the <code>db</code> command in the mongo shell. In this case, we should be able to see "test" printed out.

Or, you can start using the connection string/URI to use this database in applications.
<pre class="EnlighterJSRAW" data-enlighter-language="javascript">
mogodb://testUser:xyz123@localhost:27017/test
</pre>

<ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="5584852720"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>