---
layout: post
title: Configurando jekyll 3.2
categories: jekyll
tags: configuracion jekyll
---

Si vamos a alojar nuestra página creada con <strong>Jekyll</strong> en github, una primer paso es tener instalada su [misma versión de librerias](https://pages.github.com/versions/). La versión actual es la 93, que acaba de incluir la version 3.2 de Jekyll.

{% highlight bash %}
$ gem install github-pages -v 93
{% endhighlight %}

Aprovechando los multiples plugins que dispone jekyll, he dedicido 
utilizar alguno de los disponibles en Github.

* [Jekyll Sitemap](https://github.com/jekyll/jekyll-sitemap): Genera un sitemap con todos nuestros post y páginas.
{% highlight yaml %}
gems:
  - jekyll-sitemap
{% endhighlight %}

* [Jekyll SEO Tag](https://github.com/jekyll/jekyll-seo-tag): añade información SEO a la página. 

Añadir en la sección de gems del archivo<code>_config.yml</code>

{% highlight yaml %}
gems:
  - jekyll-seo-tag
{% endhighlight %}

Y añadir <code>{% raw  %}{% seo %}{% endraw  %}</code> en nuestro código.

* [Jekyll Archives](https://github.com/jekyll/jekyll-archives): Este plugin permite generar distintas paginas agrupando los articulos por tag, categoria, mes o año. 

Por desgracia esta gem no esta soportada por Github, por lo que la tendremos que instalar manualmente y realizar un pequeño "hack" para poder utilizarlo en github. [Otra alternativa](http://mrloh.se/2015/06/automatic-archives-for-jekyll-on-github-pages/)
{% highlight bash %}
$ gem install jekyll-archives
{% endhighlight %}

Al igual que en el anterior, añadir en la sección de gems del archivo <code>_config.yml</code> y su configuración.

{% highlight yaml %}
gems:
  - jekyll-archives

jekyll-archives:
  enabled:
    - categories
    - tags
  layout: 'archive'
  permalinks:
    tag: '/archive/tag/:name/'
    category: '/archive/category/:name/'
{% endhighlight %}

En nuestro caso, activamos solamente páginas por tag y categoria, y definimos el formato del link y layout.

La solución "low-cost" por la que he optado, es justo antes de realizar la subida a Github, es copiar las páginas generadas por el plugin en local, como si fuera contenido propio.

{% highlight bash %}
$ rm -rf archive | cp _site/archive . 
{% endhighlight %}

<div class="note warning">
<p>Con este proceso, ya que tenemos dos fuentes (la carpeta copiada y el plugin archives) que generan en la misma ubicación <code>_sites/archive</code> es necesario borrar la carpeta archive antes de arrancar el servidor en local para evitar conflictos</p>
</div>