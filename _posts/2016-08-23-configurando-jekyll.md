---
layout: post
title: configurando jekyll
categories: jekyll
tags: configuracion jekyll
---

Aprovechando los multiples plugins que dispone jekyll, he dedicido 
que [github](https://pages.github.com/) también actualizó las versión de Jekyll que soportaba.

* <a href="https://github.com/jekyll/jekyll-seo-tag">Jekyll SEO Tag</a>
Como su nombre indica, añade información SEO a la página. 

Añadir en la sección de gems del archivo<code>_config.yml</code>

{% highlight yaml %}
gems:
  - jekyll-seo-tag
{% endhighlight %}

Y añadir <code>{% raw  %}{% seo %}{% endraw  %}</code> en nuestro código.

* <a href="https://github.com/jekyll/jekyll-archives">Jekyll Archives</a>

Al igual que en el anterior, añadir en la sección de gems del archivo<code>_config.yml</code>

{% highlight yaml %}
gems:
  - jekyll-archives
{% endhighlight %}



<div class="note info">
<p>Se pueden consultar las versiones que soporta github en su <a href="https://pages.github.com/versions/">página de información de plugins</a></p>
</div>


