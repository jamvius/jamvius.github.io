---
layout: post
title: Comandos remotos de git
categories: git
tags: git remote
---

* Añadir repositorio remoto
{% highlight bash %}
# => git remote add <repository_name> <repository_url>
$ git remote add origin https://github.com/jamvius/jamvius.github.io.git
$ git remote add origin git@github.com:jamvius/jamvius.github.io.git
{% endhighlight %}

<div class="note info">
  <p>Si queremos hacer push sin necesidad de poner user/password es necesario configurar la url en el formato ssh (2º).</p>
</div>

* Mostrar repositorios remotos configurados en el repositorio actual
{% highlight bash %}
$ git remote -v
{% endhighlight %}

* Subir el estado de repositorio local al repositorio remoto
{% highlight bash %}
$ git push origin master
{% endhighlight %}

* Borra un repositorio remoto de un proyecto
{% highlight bash %}
# => git remote (remove|rm) <repositoriy_name>
$ git remote remove origin
$ git remote rm origin
{% endhighlight %}

* Actualiza la url del repositorio
{% highlight bash %}
# =>  git remote set-url <repository_name> <repository_url>
$ git remote set-url origin git@github.com:jamvius/jamvius.github.io.git
{% endhighlight %}