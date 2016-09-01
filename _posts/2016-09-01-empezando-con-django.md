---
layout: post
title: Empezando con django
description: Resumen del tutorial oficial del django
categories: python
tags: django tutorial
---

Resumen del [tutorial oficial de django](https://docs.djangoproject.com/es/1.10/intro/tutorial01/)

Para crear un nuevo proyecto
{% highlight bash %}
$ django-admin startproject mysite
{% endhighlight %}

Diferentes maneras de arrancar el servidor
{% highlight bash %}
$ python manage.py runserver
$ python manage.py runserver 8080
$ python manage.py runserver 0.0.0.0:8000
{% endhighlight %}

En django, un proyecto puede estar compuesto de varias apps, y las apps puedes estar a su vez en varios proyectos. Para crear dentro de la app.
{% highlight bash %}
$ cd mysite
$ python manage.py startapp polls
{% endhighlight %}

