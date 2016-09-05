---
layout: post
title: Empezando con django (I)
description: Resumen del tutorial oficial del django (I)
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

Para crear una vista, hay que añadir al <code>polls/views.py</code>

{% highlight python %}
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
{% endhighlight %}

y crear <code>polls/urls.py</code>

{% highlight python %}
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]
{% endhighlight %}

y añadir al archivo <code>mysite/urls.py</code> 

{% highlight python %}
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', admin.site.urls),
]
{% endhighlight %}