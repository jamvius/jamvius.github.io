---
layout: post
title: Empezando con django (II)
description: Resumen del tutorial oficial del django (II)
categories: python
tags: django tutorial
---

Resumen del segundo capítulo [tutorial oficial de django](https://docs.djangoproject.com/es/1.10/intro/tutorial02/)

Ejecutamos la migración para las clases por defecto
{% highlight bash %}
$ python manage.py migrate
{% endhighlight %}

Despues de añadir nuestros modelos
{% highlight bash %}
$ python manage.py makemigrations polls
$ python manage.py sqlmigrate polls 0001
$ python manage.py migrate
# Arrancamos el shell con nuestra app cargada
$ python manage.py shell
{% endhighlight %}

{% highlight bash %}
from polls.models import Question, Choice
>>> Question.objects.all()
<QuerySet []>
>>> q = Question(question_text="What's new?", pub_date=timezone.now())
>>> q.save()
>>> q.id
>>> q = Question.objects.get(pk=1)
{% endhighlight %}

Para activar el admin, debemos crear el usuario admin.
{% highlight bash %}
$ python manage.py createsuperuser
$ python manage.py runserver
{% endhighlight %}

Despues de configurarlo podemos acceder por [admin](http://127.0.0.1:8000/admin/)

Añadiendo al polls/admin.py 
{% highlight python %}
from django.contrib import admin

from .models import Question

admin.site.register(Question)
{% endhighlight %}

Añadimos podemos gestionar los objetos Question desde el admin