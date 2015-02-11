---
layout: post
title: Crear un site con jekyll y github
categories: jekyll
tags: github jekyll
---

Si disponemos de un site en <code>jekyll</code>, github es una solución ideal para alojarla.
Solamente hay que seguir los siguientes pasos:

* Crear un repositorio en github con el nombre del usuario (p.e. <code>jamvius.github.io</code>)
* Si no tenemos todavia nuestro site en git, lo añadimos
{% highlight bash %}
$ git init
{% endhighlight %}
y lo añadimos al repositorio
{% highlight bash %}
$ git add .
$ git commit -m "version inicial del site"
{% endhighlight %}
* Añadir el repositorio remoto al codigo de nuestro site
{% highlight bash %}
$ git remote add origin git@github.com:jamvius/jamvius.github.io.git
{% endhighlight %}
* Subir el codigo a github
{% highlight bash %}
$ git push origin master
{% endhighlight %}

...y listo. Github automaticamente genera el site jekyll en los dominios de usuario (de la forma <code>jamvius.github.io</code>)

Ahora cada vez que querramos actualizar nuestro site, solo tendremos que realizar:
{% highlight bash %}
# => Guardamos la nueva version del site en git
$ git add .
$ git commit -m "nueva vesion del site"
# => La subimos a github
$ git push origin master
{% endhighlight %}