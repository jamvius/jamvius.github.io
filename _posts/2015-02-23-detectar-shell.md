---
layout: post
title: Detectar el shell activo
categories: linux
tags: linux shell
---

* Existen varias maneras de detectar el shell activo
{% highlight bash %}
$ echo $0
/bin/zsh
$ ps -p $$
PID TTY           TIME CMD
5379 ttys001    0:01.46 /bin/zsh
{% endhighlight %}