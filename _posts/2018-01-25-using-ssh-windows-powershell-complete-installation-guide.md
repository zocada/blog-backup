---
ID: 287
post_title: 'Using SSH in Windows PowerShell &#8211; Complete Installation Guide'
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/using-ssh-windows-powershell-complete-installation-guide/
published: true
post_date: 2018-01-25 14:31:26
---
Connecting to a remote server was always been a hassle for windows users. For several years we've been depending on <a href="https://www.putty.org/" target="_blank" rel="noopener">PuTTY</a> for the same purpose and it's a pain setting up and using it. PuTTY is an SSH and TelNet client originally designed to give the functionalities that are built in on Linux terminals. Since the day Microsoft introduced <a href="https://docs.microsoft.com/en-us/powershell/" target="_blank" rel="noopener">PowerShell</a> on latest updates in Windows 10, the game started changing slowly.

We'll learn how to install <a href="https://www.openssh.com/" target="_blank" rel="noopener">OpenSSH</a> client on our Windows 10 machine with PowerShell using <a href="https://chocolatey.org/" target="_blank" rel="noopener">Chocolatey</a>, a Package Manager for Windows.
<h3>Requirements</h3>
Make sure you have latest version of Windows 10 [or Windows 7 / Windows Server 2003+] installed and PowerShell 2.0+ is available to fire up.

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

<h2>Installing Chocolatey on Windows</h2>
Open up your Windows PowerShell as Administrator by searching it on the <strong>start menu</strong>, right click and <strong>Run as Administrator</strong>.

<a href="https://zocada.com/wp-content/uploads/2018/01/powershell_run_as_administrator.jpg"><img class="alignnone size-full wp-image-293" src="https://zocada.com/wp-content/uploads/2018/01/powershell_run_as_administrator.jpg" alt="" width="852" height="656" /></a>

Now, Paste the following command into PowerShell Window to start downloading Chocolatey. It will take a while to download the file and install it.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))</pre>
Once the download is finished, Restart the environment to update the newly added environment variable. Paste the following command.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">refreshenv</pre>
&nbsp;
<h2>Installing OpenSSH in Windows</h2>
We'll be installing the freely available and ready to download version of OpenSSH through the PowerShell using choco-tools. Make sure you are running the PowerShell with administrative previleages.
<blockquote>OpenSSH is the premier connectivity tool for remote login with the SSH protocol. It encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. In addition, OpenSSH provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.</blockquote>
Copy paste the following choco command to start downloading and installing OpenSSH.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">choco install openssh</pre>
Once the installation completes, Close the PowerShell and open it again. Type the <code>ssh</code> command to verify that the installation was successfull.

<a href="https://zocada.com/wp-content/uploads/2018/01/powershell_ssh.jpg"><img class="alignnone size-full wp-image-299" src="https://zocada.com/wp-content/uploads/2018/01/powershell_ssh.jpg" alt="" width="805" height="359" /></a>

Now you can connect to your server using the standard ssh commands. If you get Host Key Verification failed error then use the following command to connect to the server only for the first time. This will add your host into the known hosts for future uses.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">ssh -o StrictHostKeyChecking=no username@yourserver</pre>
<a href="https://zocada.com/wp-content/uploads/2018/01/adding_to_known_hosts.jpg"><img class="alignnone size-full wp-image-300" src="https://zocada.com/wp-content/uploads/2018/01/adding_to_known_hosts.jpg" alt="" width="615" height="304" /></a>

For any further queries, visit the official website of <a href="https://www.openssh.com/" target="_blank" rel="noopener">OpenSSH</a> and <a href="https://chocolatey.org" target="_blank" rel="noopener">Chocolatey</a>. Leave a comment if you need any help or if you ran into an error.

<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="6336781322"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>