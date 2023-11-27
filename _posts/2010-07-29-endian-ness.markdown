---
layout: post
title: Endian-ness
author: hendrasaputra
date: 2010-07-29 10:10:00.000000000 +07:00
categories: [blog, code]
tags: [featured]
---

Getting `short int` and `long int` from a byte character on C can make
you shoot your feet sometimes. Especially if you&rsquo;re coding it in
Little Endian machine and processing them on Big Endian machine.
Suddenly you get a different result. For example take a look at this code

{% highlight c %}
get_int32(unsigned int *dest, char *src)
{
    unsigned char dummy[4];
    memcpy(&amp;dummy[0],&amp;src[0],1);
    memcpy(&amp;dummy[1],&amp;src[1],1);
    memcpy(&amp;dummy[2],&amp;src[2],1);
    memcpy(&amp;dummy[3],&amp;src[3],1);
    memcpy(dest,&amp;dummy,4);
}

get_int16(unsigned int *dest, char *src)
{
    unsigned char dummy[2];
    bzero(dummy,2);
    memcpy(&amp;dummy[0],&amp;src[0],1);
    memcpy(&amp;dummy[1],&amp;src[1],1);
    memcpy(dest,&amp;dummy,2);
}
{% endhighlight %}


This code when processed in Big Endian machine can correctly translate
a byte character to <strong>Long</strong> and <strong>Short</strong>. What it did is it assume that
the <strong>Most Significant Bit</strong> is stored on the lowest address.
but if we run this code on the Little Endian machine (such as your
ordinary Intel machine) it will produce a different result because on
Little Endian the <strong>Least Significant Bit</strong> is stored in the lowest
address, and that can cause a bug in you application.
To fix things lets change the code to the following

{% highlight c %}
unsigned long int get_int32(char *src)
{
    unsigned char dummy[4];
    bzero(dummy,4);
    dummy[0]=*src;
    dummy[1]=*(src+1);
    dummy[2]=*(src+2);
    dummy[3]=*(src+3);
    return (dummy[0]&lt;&lt;24) | (dummy[1]&lt;&lt;16) | (dummy[2]&lt;&lt;8) | dummy[3];
}

unsigned short int get_int16(char *src)
{
    unsigned char dummy[2];
    bzero(dummy,2);
    dummy[0]=*src;
    dummy[1]=*(src+1);
    return (dummy[0] &lt;&lt; 8) | dummy[1];
}

{% endhighlight %}


This code is better because it doesn&rsquo;t assume that MSB is stored in
the lowest address, it just bit shifting and &lsquo;OR'ing memory address
value.
  
