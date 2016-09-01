---
layout: post
title: Recuperar el valor del identificador de usuario de analytics
description: Recuperar el valor del identificador de usuario de analytics utilizando un callback en javascript
categories: javascript
tags: analytics
---

Si queremos recuperar el valor de usuario que ha asignado a un usuario, la libreria de google dispone de una funcion <code>ga(funcion)</code> que define un callback que ejecutará una vez se ha cargado la librería en nuestra página. 

En el siguiente ejemplo, recuperarmos el identificador y lo asignamos a un input oculto, para identificar a los usuarios que utilizan un formulario.

{% highlight javascript %}
<script>
    ga(function(tracker) {
        var clientId = tracker.get('clientId');
        var elem = document.getElementById("userId");
        elem.value = clientId;
    });
</script>
{% endhighlight %}