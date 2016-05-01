---
layout: post
title: Actualizar jekyll a la version 3
categories: jekyll
tags: upgrade jekyll
---

Después de un año con el blog parado, he decidido volver a activarlo actualizando a la version 3, aprovechando
que [github](https://pages.github.com/) también actualizó las versión de Jekyll que soportaba.

<div class="note info">
<p>Se pueden consultar las versiones que soporta github en su <a href="https://pages.github.com/versions/">página de información de plugins</a></p>
</div>

Los cambios principales en esta nueva versión ha sido la reducción de gems que utiliza por defecto, por lo que si queremos
ciertas funcionalidades, como la paginación, es necesario añadir la gem en el archivo de configuración <code>_config.yml</code>

{% highlight yaml %}
# ahora markdown es el procesador por defecto
markdown:         kramdown
# y el syntax highlighting por defecto es rouge, que esta implementado en ruby
highlighter:      rouge
# es necesario poner el jekyll-paginate para tener implementada la paginación
gems: ['jekyll-paginate']
{% endhighlight %}