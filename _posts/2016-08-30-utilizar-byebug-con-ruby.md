---
layout: post
title: Utilización de byebug y web-console en ruby
description: Recursos para debugar con byebug y web-console en nuestras apps
categories: ruby
tags: byebug web-console debug
---

[Byebug](https://github.com/deivid-rodriguez/byebug) y [Web Console](https://github.com/rails/web-console) son 2 librerias que nos permite debugar el estado de nuestras apps, añadiendo un comando en el punto en el que queremos analizar su estado. La diferencia es que byebug para la app y permite analizarla desde la consola, web-console, crea un terminal virtual en nuestra pagina, que permite realizar comandos ruby. El uso de ambas librerias es muy similar:

Ejemplo **byebug**
{% highlight ruby %}
def index
  byebug
  @articles = Article.find_recent
{% endhighlight %}  

Ejemplo **web console**
{% highlight ruby %}
def index
  console
  @articles = Article.find_recent
{% endhighlight %}  

Enlaces de interes:

* [Articulo sitepoint de Byebug](https://www.sitepoint.com/the-ins-and-outs-of-debugging-ruby-with-byebug/)
* [Documentación de byebug en rails](http://guides.rubyonrails.org/debugging_rails_applications.html#debugging-with-the-byebug-gem)
* [Documentación de web-console en rails](http://guides.rubyonrails.org/debugging_rails_applications.html#debugging-with-the-web-console-gem)