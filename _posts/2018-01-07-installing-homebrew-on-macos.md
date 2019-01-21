---
ID: 145
post_title: Installing Homebrew on macOS
author: Arjun Suvarna S
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/installing-homebrew-on-macos/
published: true
post_date: 2018-01-07 15:16:28
---
Homebrew is open-source package management system that simplifies installing packages on macOS. Self-termed as the missing package manager for macOS is now one of the largest community-supported open-source project developed through Github’s open-source community. HomeBrew is originally written by MaxHowell and it gained huge popularity among the Ruby developer’s community.

&nbsp;

To install Homebrew open up terminal and type in the following
<pre class="EnlighterJSRAW" data-enlighter-language="shell">/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
</pre>
you will be prompted to allow installation press return to go through with installation

To install a package us the 'brew install command', for example:
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$ brew install wget</pre>
you can use the list command to see the list of installed packages
<pre class="EnlighterJSRAW" data-enlighter-language="shell">$brew list</pre>
to find details about available packages head on over to http://brewformulas.org/

&nbsp;