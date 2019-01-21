---
ID: 111
post_title: >
  Installing Node.js in Ubuntu and other
  Linux distros.
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/installing-node-js-in-ubuntu-and-other-linux-distros/
published: true
post_date: 2018-01-06 20:23:46
---
Node.js is available for Linux distributions and the package comes built-in with the Node Package Manager a.k.a NPM. npm is the package manager for JavaScript. It's also the world's largest software registry. There are over 600,000 packages of JavaScript code available to download, with approximately 3 billion downloads per week. npm makes it easy for JavaScript developers to reuse code other developers have shared. Adapt it to new applications, or incorporate it as is. When someone revises their code, you can easily update your application to incorporate the newly improved code.
<h2>Debian and Ubuntu based distributions</h2>
<em>Including Linux Mint, Linux Mint Debian Edition (LMDE), elementary OS, bash on Windows and others.</em>

Node.js is available from the NodeSource Debian and Ubuntu binary distributions repository (formerly Chris Lea's Launchpad PPA). Support for this repository, along with its scripts, can be found on GitHub at nodesource/distributions.
<h3>Using Package Manager</h3>
This is the most basic installation you need.
Fire up a terminal and copy the commands to install Node.js and npm.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo apt-get update
sudo apt-get install nodejs</pre>
&nbsp;

<h3>Downloading and Installing from NodeSource</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="shell">curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs</pre>
For installing Node.js 9.x
<pre class="EnlighterJSRAW" data-enlighter-language="shell">curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt-get install -y nodejs</pre>
&nbsp;

<h2>Arch Linux</h2>
Node.js and npm packages are available in the Community Repository.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">pacman -S nodejs npm</pre>

<h2>Enterprise Linux and Fedora</h2>
Including Red Hat® Enterprise Linux® / RHEL, CentOS and Fedora.

Node.js is available from the NodeSource Enterprise Linux and Fedora binary distributions repository. Support for this repository, along with its scripts, can be found on GitHub at nodesource/distributions.

Note that the Node.js packages for EL 5 (RHEL5 and CentOS 5) depend on the EPEL repository being available. The setup script will check and provide instructions if it is not installed.

On RHEL, CentOS or Fedora, for Node.js v8 LTS:
<pre class="EnlighterJSRAW" data-enlighter-language="shell">curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -</pre>

OR For installing Node.js 9.x
<pre class="EnlighterJSRAW" data-enlighter-language="shell">curl --silent --location https://rpm.nodesource.com/setup_9.x | sudo bash -</pre>

and then install
<pre class="EnlighterJSRAW" data-enlighter-language="shell">sudo yum -y install nodejs</pre>

For more information on installing on Linux visit <a href="https://nodejs.org/en/download/package-manager/" rel="noopener" target="_blank">the Node.js official website</a>