---
layout: post
status: publish
published: true
title: Setting up Mercurial on CentOS x86_64
wordpress_id: 32
date: '2011-05-11 23:35:54 -0400'
date_gmt: '2011-05-12 03:35:54 -0400'
categories:
- how to
tags:
- centos
- hostgator
- mercurial
comments: []
---
<p><a href="http://mercurial.selenic.com/">Mercurial</a> is a badass distributed version control system. Most likely, you know what mercurial is if you're reading this, so I won't bother explaining it. If you don't know what it is, go to <a href="http://hginit.com" >hginit.com</a>.</p>
<p><strong>Step 1. Get the RPM of Mercurial for Your Version</strong>
I got my package from <a href="http://packages.sw.be/mercurial/">packages.sw.be/mercurial/</a>. Make sure to choose the right version. I chose <a href="http://packages.sw.be/mercurial/mercurial-1.8.2-1.el5.rf.x86_64.rpm">mercurial-1.8.2-1.e15.rf.x86_64.rpm</a>, but there may be more up to date versions or more appropriate versions for you.</p>
<pre>[root@two twohlix.com]# cd /home
[root@two home]# wget http://packages.sw.be/mercurial/mercurial-1.8.2-1.el5.rf.x86_64.rpm
--2011-05-11 22:17:43--  http://packages.sw.be/mercurial/mercurial-1.8.2-1.el5.rf.x86_64.rpm
Resolving packages.sw.be... 85.13.226.40
Connecting to packages.sw.be|85.13.226.40|:80... connected.
...</pre></p>
<p><strong>Step 2. Install the RPM</strong></p>
<pre>[root@two home]# rpm -Uvh mercurial-1.8.2-1.el5.rf.x86_64.rpm
warning: mercurial-1.8.2-1.el5.rf.x86_64.rpm: Header V3 DSA signature: NOKEY, key ID 6b8d79e6
Preparing...                ########################################### [100%]
   1:mercurial              ########################################### [100%]</pre>
I used a few options in the install: '-U' upgrades or installs (whichever it has to) the rpm. '-v' makes it verbose so you can see it do things. '-h' adds the #(h for hash) marks so you can see the progress over time.
If you didn't use your root account for this be sure to use sudo:</p>
<pre>[totally_not_root@two home]# sudo rpm -Uvh mercurial-1.8.2-1.el5.rf.x86_64.rpm</pre></p>
<p><strong>Step 3. Check on Mercurial</strong></p>
<pre>[root@two home]# hg</pre>
that command should result in: </p>
<pre>Mercurial Distributed SCM</p>
<p>basic commands:</p>
<p> add        add the specified files on the next commit
 annotate   show changeset information by line for each file
...</pre>
If that happened, you're all done. You may need to install python if it broke.</p>
