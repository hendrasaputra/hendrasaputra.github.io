---
layout: post
title: JSLint Bundle for TextMate
date: 2011-04-04 13:31:00.000000000 +07:00
---

Developer yang bekerja dengan JavaScript tentu familiar dengan tools <a href="http://jslint.com" title="JSLint">JSLint</a> buatan Douglas Rockford. Masalahnya biasanya penggunaan <a href="http://jslint.com" title="JSLint">JSLint</a> ini adalah dengan mengunjungi <a href="http://jslint.com" title="JSLint">URL</a> lalu melakukan copy-paste code di website tersebut untuk dianalisa. Untuk pengguna TextMate berikut ini adalah cara yang lebih nyaman untuk melakukan jslint terhadap code JavaScript yang kita punya. Caranya adalah dengan membuat bundle dari script JSLint ini di TextMate. Pembuatan bundle ini menggunakan bantuan dari engine <a href="https://github.com/senchalabs/hammerjs" title="HammerJS">HammerJS</a> buatan Ariya Hidayat. Berikut adalah step-by-step pembuatannya

<ol>
<li><p>Install hammerjs</p>

{% highlight bash %}
 git clone http://github.com/senchalabs/hammerjs.git
 cd hammerjs
 cmake ./
 make
{% endhighlight %}
</li>
<li><p>Copy binary <code>hammerjs</code> ke PATH (e.g. /usr/local/bin)</p>
{% highlight bash %}
cp ./hammerjs /usr/local/bin
{% endhighlight %}
</li>
<li><p>Copy <code>lint.js</code> dari folder <code>hammerjs/examples</code> ke PATH</p>
{% highlight bash %}
cp ./examples/lint.js /usr/local/bin
{% endhighlight %}
</li>
<li><p>Buat shell script untuk wrapper jslint dengan isi sebagai berikut</p>
{% highlight bash %}
#!/bin/bash
/usr/local/bin/hammerjs /usr/local/bin/lint.js $1
{% endhighlight %}
</li>
<li><p>Pindah ke directory Bundle TextMate</p>
{% highlight bash %}
cd ~/Library/Application Support/TextMate/Bundles
{% endhighlight %}
</li>
<li><p>Ambil jslint-bundle dari github</p>
{% highlight bash %}
git clone https://github.com/hendrasaputra/jslint-bundle.git
{% endhighlight %}
</li>
<li><p>Reload Bundles on TextMate</p></li>
</ol>
  
