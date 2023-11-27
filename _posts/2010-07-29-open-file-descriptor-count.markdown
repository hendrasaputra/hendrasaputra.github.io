---
layout: post
title: Open File Descriptor Count
author: hendrasaputra
date: 2010-07-29 09:23:00.000000000 +07:00
categories: [code, awk]
---

Here&rsquo;s an awk function I keep using to find out how many open files a
username open on a unix system. You should replace &lsquo;oracle&rsquo; below with the username you want to check

{% highlight bash %}
lsof | awk '/oracle/ {pidct[$2]++;pidname[$2]=$2;procname[$2]=$1} END {for (i in pidname) {printf (&quot;%s %s %dn&quot;,procname[i],pidname[i],pidct[i]);}}' | tr -s &quot; &quot; | sort -t &quot; &quot; -n -r -k 3,3
{% endhighlight %}
  
