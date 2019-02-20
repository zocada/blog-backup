---
ID: 1075
post_title: 'Deploying Node.js application to DigitalOcean &#8211; Setting up the server'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/deploying-node-js-application-to-digitalocean-setting-up-the-server/
published: true
post_date: 2019-02-20 06:09:49
---
Node.js is one of the fastest growing technology this decade have ever seen. Emerging from the language which ruled the front-end of the web, Node.js has become quite the popular and the favorite JavaScript run-time environment which brought tremendous change in how the web looks today. From server-side scripting to creating some of the fastest web servers, Node.js got it all. During the growth of Node.js and the super awesome community around it, <a href="https://expressjs.com/" target="_blank" rel="noopener">Express.js</a> has always been the de-facto when it comes to building robust web servers in no time.

In this post, I'll try to cover the following things in brief.
<ul>
 	<li>Getting familiar with Digital Ocean and creating your first droplet</li>
 	<li>Setting up SSH and connecting to your server from your local machine</li>
 	<li>Setting up a simple Express.js web-server in local machine</li>
 	<li>Using Git to deploy your code to server</li>
 	<li>Installing Node.js and PM2 on the server</li>
 	<li>Assigning a domain name for the server</li>
</ul>
<h2>Step 1. Creating a <a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener">DigitalOcean</a> account with free credits</h2>
[caption id="attachment_1086" align="aligncenter" width="1354"]<a href="https://m.do.co/c/28bb5c20041a"><img class="size-full wp-image-1086" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Cloud-Computing-Simplicity-at-Scale.png" alt="DigitalOcean" width="1354" height="767" /></a> DigitalOcean[/caption]

<a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener">DigitalOcean</a> with no doubt have made cloud easier and much accessible to people with any skill level. The simple interface and outstanding customer support makes <a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener">DigitalOcean</a> favorite for hobbyist developers and large enterprises. <a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener">Digitalocean</a> provides a welcome credit of $100 for every signups with this <a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener"><strong>unique link.</strong></a> Follow the link and click on Sign Up, You should be able to see a message mentioning your welcome credit of $100.

[caption id="attachment_1089" align="aligncenter" width="659"]<a href="https://m.do.co/c/28bb5c20041a"><img class="size-full wp-image-1089" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean.png" alt="DigitalOcean" width="659" height="344" /></a> DigitalOcean[/caption]

You might need to add your credit card information to continue the sign-up procedure and get the $100 reward. Don't worry, <a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener">DigitalOcean</a> won't deduct any money from your account without prior notice and a $100 is good enough to run a free server for almost a year.

[caption id="attachment_1091" align="aligncenter" width="813"]<a href="https://m.do.co/c/28bb5c20041a"><img class="size-full wp-image-1091" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Welcome.png" alt="DigitalOcean SignUp" width="813" height="381" /></a> DigitalOcean SignUp[/caption]

Once your sign up process is complete, and your credit card details has been successfully added, your account will have $100 credit to use in <a href="https://m.do.co/c/28bb5c20041a" target="_blank" rel="noopener">DigitalOcean</a>. You'll be able to see your credits in the billing section of your account, you can find the "billing" menu under the "account" section in the left navigation ar in your dashboard. Now, Let's head on to creating a new server!

<a href="https://m.do.co/c/28bb5c20041a"><img class="aligncenter size-full wp-image-1093" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Account1.png" alt="" width="1354" height="668" /></a>

<!-- SECTION 2 -->
<h2>Step 2. Creating a new Droplet</h2>
Droplets are individual computing units in <a href="https://m.do.co/c/28bb5c20041a">DigitalOcean</a>, You can imagine them as individual servers or computers (after all cloud is actually someone else's computer). We need to host our server in one of the droplets we create. Click on the "Create" button and choose droplet to proceed to create a new droplet.

<a href="https://m.do.co/c/28bb5c20041a"><img class="aligncenter size-full wp-image-1097" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Account2.png" alt="" width="616" height="184" /></a>

Next, in the choose an image option, you can choose "ubuntu", which will be selected by default. This is the image of the operating system that DigitalOcean will install in our server.

<a href="https://m.do.co/c/28bb5c20041a"><img class="aligncenter size-full wp-image-1099" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Create-Droplets.png" alt="" width="1040" height="443" /></a>

Next, on the choose a size option, you can choose a server configuration that fits your needs. Here, I'll be choosing a $40 per month configuration which has quite a good configuration, to begin with. You may choose a $5 server if all you need is a 1gb ram server.

<a href="https://m.do.co/c/28bb5c20041a"><img class="aligncenter size-full wp-image-1100" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Create-Droplets1.png" alt="" width="1142" height="532" /></a>

You can leave the <strong>Add backup option</strong> to "No" and <strong>Add block storage</strong> option as is for now. Next, on the <strong>Choose a data center</strong> option you need to choose a data center location that is closer to the location of your target audience. The larger the audience from a Data Center near to them, the faster your site will be accessible to them. Since I am from India, the Bangalore data center is closer to me, and since most of my reader are from India, this is the best choice. If you are living elsewhere feel free to chose the one nearest to you.

<a href="https://m.do.co/c/28bb5c20041a"><img class="aligncenter size-full wp-image-1102" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-13-DigitalOcean-Create-Droplets2.png" alt="" width="1142" height="411" /></a>

Next, we need to set up SSH keys for secure access to our server. Click on the add SSH Key button, a popup will open requesting you to paste the public key and name.

<a href="https://m.do.co/c/28bb5c20041a"><img class="aligncenter size-full wp-image-1105" src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-16-DigitalOcean-Create-Droplets1-1.png" alt="" width="976" height="560" /></a>

To create a new SSH key pair, if you are in a Linux machine use the following command in your terminal. (without the $)
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ ssh-keygen</pre>
&nbsp;
You can specify the name of the key and provide a passphrase while generating the RSA keys. For example, if you have given the name as "mydroplet", your private key and public key will be saved to the current working directory with the names <strong>mydroplet</strong> and <strong>mydroplet.pub</strong>. Once the keys have been generated, move the files named as you specified and name.pub to your <code>.ssh</code> directory in the home folder. Once you are done with this you can copy the contents of the public key, ie. <strong>mydroplet.pub</strong> and paste it in the above-mentioned field in DigitalOcean. If you have NPM installed in your system, u can simply use the <code>cli-cp</code> library to copy the contents of the file directly. To install this package, simply execute the command <code>npm i -g cli-cp</code>, this is completely optional, and you can do it manually too. We'll walk you through the process in the below screencast so you can follow the steps easily.
<center>
<script id="asciicast-5e5uM1HWQwOmgXUoWAKylsfC8" src="https://asciinema.org/a/5e5uM1HWQwOmgXUoWAKylsfC8.js" async></script>
</center>
In the end, paste the contents into the text field in DigitalOcean to add the SSH key with a name and choose the name to select the keys to be used.
Next, click on the big green button saying <strong>create</strong> to create your droplet.

<img src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-20-DigitalOcean-Create-Droplets.png" alt="" width="1148" height="450" class="aligncenter size-full wp-image-1113" />


<!-- Step 3 -->
<h2>Step 3. Assigning a floating IP to your droplet</h2>
A floating IP is a static IP address that points to one of your Droplets. It allows you
to redirect network traffic to any of your Droplets in the same datacenter. So that you can have a backup server and you can change the current floating IP to point to the backup server in case the main server goes down (or u need to shut down for maintenance, or want to point the domain to a different droplet in later time). To create a new floating IP head on to the <strong>Networking</strong> menu in the side navigation and choose the tab <strong>Floating IPs</strong>. Click on the Search for droplet field and choose the droplet you just created and click on <strong>Assign Floating IP</strong>.

<img src="https://zocada.com/wp-content/uploads/2019/02/Screenshot_2019-02-20-DigitalOcean-Floating-IPs1.png" alt="" width="1353" height="667" class="aligncenter size-full wp-image-1115" />

<!-- Step 4 -->
<h2>Step 4. Logging into the Server/droplet using SSH</h2>
Once you have assigned the floating IP, you can now log in to the server from your local machine using SSH. Copy the floating IP of your droplet and execute the following command in your Terminal. Windows users can either use Windows Subsystem for Linux or manually <a href="https://zocada.com/using-ssh-windows-powershell-complete-installation-guide/" >install OpenSSH client in your PowerShell to use SSH.</a>
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ ssh root@YOUR-FLOATING-IP</pre>
&nbsp;
If it gives a warning, type yes on the prompt to add your server to known host. You'll be logged into your server and will be able to execute commands in your droplet now.

<img src="https://zocada.com/wp-content/uploads/2019/02/Screenshot-from-2019-02-20-10-27-31.png" alt="" width="802" height="568" class="aligncenter size-full wp-image-1118" />

<!-- step 5 -->
<h2>Step 5. Installing Node.js in your server</h2>
Make sure you are logged in to your server using SSH, We'll use the <a href="https://github.com/creationix/nvm" rel="noopener" target="_blank">Node Version Manager (NVM)</a> to install Node.js and NPM in our server. Execute the following shell script provided in the nvm documentation to get started with the installation.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash</pre>
&nbsp;
Once the Shell Script is successfully run, you need load nvm. Execute the following command to make the changes made by the shell script take effect in the current terminal.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ source .bashrc</pre>
&nbsp;
Once it's done, you can check whether nvm is installed, by simply executing the command <code>nvm</code>. To install the latest version of Node.js and NPM execute the following command.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ nvm install node</pre>
&nbsp;

<img src="https://zocada.com/wp-content/uploads/2019/02/installing-node.gif" alt="" width="926" height="555" class="aligncenter size-full wp-image-1121" />

In order for some npm packages to work (those that require compiling code from source, for example), you will need to install the build-essential package:
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ sudo apt install build-essential</pre>
&nbsp;

<!-- step 6 -->
<h2>Step 6. Testing everything with a simple Node.js app</h2>
Once we are done setting up all the necessary things we need to run a simple Node.js application, let's put it into the test. Let's use a simple Node HelloWorld application. We have already created a simple node app for this, and we'll use git to clone this project and run it. Make sure you have git installed in the server, you can use the command <code>git --version</code> to check the version of git in the server. Git will be installed by default in the server, if not, you can install git by simply executing <code>sudo apt install git</code>.
Execute the following command to clone the repository from GitHub to your server. This will be the common workflow we'll be using to bring our code into the server later.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ git clone https://github.com/zocada/node-hello-world.git</pre>
&nbsp;
Let's run the app
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ cd node-hello-world.git
$ node index.js</pre>
&nbsp;

Now you should be able to check the output of the node web app we ran from a browser by navigating to: <strong>http://YOUR-SERVER'S-FLOATING-IP:3000</strong>, example <strong>http://192.168.1.1:3000</strong> and you will be able to see the HelloWorld message.

<h2>Wrapping up</h2>
In the upcoming post, we'll discuss how to attach a domain to your server, setup Nginx for reverse proxy and PM2 for running the node applications in production.