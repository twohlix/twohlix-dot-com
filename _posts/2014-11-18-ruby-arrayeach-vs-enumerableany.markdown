---
layout: post
status: publish
published: true
title: Ruby Array#each vs Enumerable#any?
wordpress_id: 91
date: '2014-11-18 11:20:48 -0500'
date_gmt: '2014-11-18 15:20:48 -0500'
categories:
- random
- ruby
tags: []
comments: []
---
So I had a little snippet of code that a coworker of mine mentioned I could replace:
<pre>collection_thingy.each do |val|
  return if val.prop == :particular_thing
end</pre>
with:
<pre>return if collection_thingy.any? { |val| val.prop == :particular_thing }</pre>
And that got me thinking about which was faster. So I did some quick benchmarking. Results and code are embedded below.
<p><script src="https://gist.github.com/twohlix/e103633365933380a105.js"></script></p>
<p>Clearly Array#each is faster than using the equivalent Enumerable#any?, and by 13-28% depending on the array size. That seems like a lot. I'm not enitrely sure why it's that much faster but it's interesting. Still, for most cases there is a negligble difference (especially in a Rails app), just be aware of the difference if you're traversing giant arrays (on 1Billion elements its as much as 14 second difference in my environment).</p>
<p>Here are some graphs showing the speedup more visually (<a href="http://imgur.com/a/dwY4b">imgur album of graphs</a>):
<img src="http://i.imgur.com/apNCqSU.png" alt="1M Elements" width="60%" />
<img src="http://i.imgur.com/8ZHb1yc.png" alt="10M Elements" width="60%" />
<img src="http://i.imgur.com/vBsdvzt.png" alt="100M Elements" width="60%" />
<img src="http://i.imgur.com/ItKf9Lx.png" alt="1B Elements" width="60%" /></p>
<p>All that being said, if performance isn't an issue in the particular codeblock Enumerable#any? is more readable. Feel free to post your own results as actual runtimes will vary from environment to environment.</p>
