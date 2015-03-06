---
layout: post
title: Calcular el espacio de los directorios
categories: linux
tags: linux shell
---

* Una manera sencilla de calcular el espacio de los directorios es usando el comando <code>du</code>
{% highlight bash %}
$ du -cksh *
1.7G	Documents
1.6G	Downloads
1.4G	Google Drive
2.2G	Library
 27M	Music
421M	Pictures
 26G	VirtualBox VMs
7.0G	apps
1.1G	biblioteca
208M	eclipse
 91M	sources
# [...]
 44G	total
{% endhighlight %}
