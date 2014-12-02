---
layout: post
status: publish
published: true
title: Using HostingScripts by twohlix
wordpress_id: 42
date: '2011-06-07 17:25:31 -0400'
date_gmt: '2011-06-07 21:25:31 -0400'
categories:
- random
tags: []
comments: []
---
<p>The HostingScripts I'm talking about are on github at <a href="http://github.com/twohlix/HostingScripts">http://github.com/twohlix/HostingScripts</a>. Feel free to fork it for your own setup.</p>
<p><strong>Step 1. Download the Code using Git</strong></p>
<pre>
[csmith@two ~]$ cd /wherever/you/want/the/scripts/to/go/
[csmith@two go]$ git clone http://github.com/twohlix/HostingScripts.git
</pre>
Now you should have a bleeding edge version of my HostingScripts under your current directory/HostingScripts/
You can read the README or just keep reading here. </p>
<p><strong>Step 1b. You Might Have to Change Permissions</strong>
Check permissions on the scripts and change them to appropriate permissions.</p>
<pre>
[csmith@two HostingScripts]$ ls -l
total 16
-rwxrwxr-x 1 csmith csmith  281  Jun  3 16:01 disablewww
-rwxrwxr-x 1 csmith csmith 3190  Jun  3 16:01 enablewww
-rwxrwxr-x 1 csmith csmith  945  Jun  3 16:01 listwww
-rwxrwxr-x 1 csmith csmith  843  Jun  3 16:01 README
</pre>
Those permissions will let anyone run your scripts, but I'm guessing thats not what you want. You might want to chmod away some of those permissions or add them if they're missing.</p>
<pre>
[csmith@two HostingScripts]$ chmod go-x *www
</pre>
That will remove any executable permissions for everyone and the group. Change up the chmod accordingly: If you needed to add permissions so you can execute it, or your group wants to execute it</p>
<pre>
[csmith@two HostingScripts]$ chmod ug+x *www
</pre></p>
<p><strong>Step 2. Alter the Scripts for Your Setup</strong>
I'm going to add a configuration file to the project so you only have to change things in one place, but for now you'll have to edit some things (maybe).</p>
<p>This script assumes some things:
1. You're using CentOS's basic setup with <em>httpd</em> for the webserver (not apache2). Particularly <a href="http://secure.hostgator.com/~affiliat/cgi-bin/affiliates/clickthru.cgi?id=twohlix">HostGator's</a> VPS setup. If you're on a HostGator VPS I'm fairly certain you don't need to change anything.
2. You're hosting your own DNS server: <em>named</em>.
3. Your users' home directories are /home/username</p>
<p>These are all changeable, just bust out your favorite text editor and go to town on the scripts (especially <em>enablewww</em>). I'll leave it up to you to figure out what you have to change.</p>
<p><strong>Step 3. Enable a Site</strong>
Enabling a site is easy. For example if I wanted to enable hosting of twohlix.com in my user I would do this:</p>
<pre>
[csmith@two HostingScripts]$ ./enablewww csmith twohlix.com
</pre>
The site should be up and running under <em>~csmith/www/twohlix.com/</em> and the servable files are in htdocs/. I'll often create a symlink named htdocs to whatever directory I want. For example this site uses a symlink from htdocs to my wordpress directory. If i want to put the site in a special maintenance mode I could just recreate the htdocs symlink to some other directory and httpd will serve that up instead.</p>
<pre>
[csmith@two twohlix.com]$ ln -s wordpress htdocs
</pre></p>
<p><strong>Step 4. Disable a Site</strong>
Disabling a site is fairly easy, although you have to alter the <em>named.conf</em> file if you want to stop the DNS. I plan to add in the changes for that, but not this second.</p>
<pre>
[csmith@two HostingScripts]$ ./disablewww csmith twohlix.com
</pre></p>
