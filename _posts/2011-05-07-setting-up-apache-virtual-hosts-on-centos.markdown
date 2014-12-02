---
layout: post
status: publish
published: true
title: Setting up Apache Virtual Hosts on CentOS
wordpress_id: 13
date: '2011-05-07 03:12:48 -0400'
date_gmt: '2011-05-07 07:12:48 -0400'
categories:
- how to
tags:
- apache
- httpd
- centos
- hostgator
comments:
- id: 32616
  author: Prayoga Teguh
  author_email: ogalolypop@gmail.com
  author_url: http://wallpapermoo.com
  date: '2014-04-18 17:57:34 -0400'
  date_gmt: '2014-04-18 21:57:34 -0400'
  content: Thanks, its work for me. Now I can create more than one website on my CentOS
    server. Thanks again. :D
- id: 41078
  author: Gilson
  author_email: ur1sg6d118@hotmail.com
  author_url: http://www.facebook.com/profile.php?id=100003458362673
  date: '2014-08-12 14:29:50 -0400'
  date_gmt: '2014-08-12 18:29:50 -0400'
  content: Thank u David, I've been solved the pblorem. I have to use the Windows
    Installer for PHP 5.2.0, I just leave the Apache 2.2.3 and reinstall PHP. But
    I don't understand, 'cause I had (previously) Apache 1.5.x or 2.2.0 (i can't remember
    well!) and PHP 5.2.0 and I don't use the Windows Installer for PHP, just extract
    the files of PHP and configure my Apache and it's done, but now not, anyway, thank
    u so much for the help, and I sorry (dumb, I don't check it the Windows Installer,
    anyway!!)
- id: 42887
  author: How can I set up Virtual Hosts in Centos7? | Question and Answer
  author_email: ''
  author_url: http://qandasys.info/how-can-i-set-up-virtual-hosts-in-centos7/
  date: '2014-09-11 08:24:13 -0400'
  date_gmt: '2014-09-11 12:24:13 -0400'
  content: '[...] http://twohlix.com/2011/05/setting-up-apache-virtual-hosts-on-centos/
    [...]'
---
<p>So you've got a new VPS host from <a href="http://secure.hostgator.com/~affiliat/cgi-bin/affiliates/clickthru.cgi?id=twohlix">HostGator</a>. You want to host yours and your 5,000 closest friends' sites too: but in order to do that you have to setup your apache server's virtual hosts.</p>
<p><strong>Step 1. Make a Directory to contain your Virtual Host files</strong></p>
<pre>[root@two twohlix.com]#
[root@two twohlix.com]# cd /etc/httpd/
[root@two httpd]# mkdir sites-available
[root@two httpd]# mkdir sites-enabled</pre>
Now that you've created 'sites-enabled' and 'sites-available', we're going to make Apache check any of the conf files you have in 'sites-enabled'.</p>
<p><strong>Step 2. Tell Apache to Look for your Conf Files</strong></p>
<pre>[root@two httpd]# vim conf/httpd.conf</pre>
Add these lines to the end of your 'httpd.conf' file:</p>
<pre>NameVirtualHost *:80
Include /etc/httpd/sites-enabled/</pre>
<strong>Step 3. Create Some Configuration Files for your Sites</strong></p>
<pre>[root@two httpd]# cd sites-available/
[root@two sites-available]# cat > twohlix.com.vhost.conf
#
# &nbsp; twohlix.com (/etc/httpd/sites-available/twohlix.com)
#
<VirtualHost *:80>
&nbsp;&nbsp; &nbsp; &nbsp;  ServerAdmin admin@twohlix.com
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;ServerName &nbsp;twohlix.com
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;ServerAlias www.twohlix.com *.twohlix.com</p>
<p>        #Indexes + Directory Root
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;DocumentRoot /home/csmith/www/twohlix.com/htdocs/
        <Directory "/home/csmith/www/twohlix.com/htdocs">
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Options Indexes FollowSymLinks MultiViews
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;AllowOverride All
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Order allow,deny
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Allow from all
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;</Directory></p>
<p>        #LOG FILES
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;ErrorLog &nbsp;/home/csmith/www/twohlix.com/logs/error.log
&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;CustomLog /home/csmith/www/twohlix.com/logs/access.log combined
</VirtualHost>
</pre>
Change the DocumentRoot to wherever you want to host your website for example '/opt/development/username/www.yoursite.com/html/' and make sure that directory exists (user mkdir).
Make sure your log's directory exists also.</p>
<p><strong>Step 4. Symlink the Conf Files To 'sites-enabled'</strong></p>
<pre>[root@two sites-available]# ln -s /etc/httpd/sites-available/twohlix.com.vhost.conf /etc/httpd/sites-enabled/twohlix.com.vhost.conf</pre>
I symlink my sites into 'sites-enabled' because that way its easy to turn on and off sites (for development) without having to make/remake VHost files. Just 'rm' the file from sites-enabled if you want apache to stop serving it.</p>
<p><strong>Step 5. Restart Apache</strong></p>
<pre>[root@two sites-available]# /etc/init.d/httpd restart</pre>
OR</p>
<pre>[root@two sites-available]# /etc/init.d/httpd graceful</pre>
That should work. Just place all your servable documents (or symlink things) into the DocumentRoot you specified. Voila...i hope.
I'll throw a script to make this easy up on <a href="https://github.com/twohlix">Github</a>.</p>
