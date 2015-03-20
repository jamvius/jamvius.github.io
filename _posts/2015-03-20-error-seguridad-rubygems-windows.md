---
layout: post
title: Corregir el error de certificados al instalar gems en Windows
categories: ruby 
tags: ruby gem windows
---

Si al intentar instalar una gem en windows nos da un error del estilo:
{% highlight bash %}
SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed
{% endhighlight %}

hay que actualizar los certificados siguiendo esta [guia](https://gist.github.com/luislavena/f064211759ee0f806c88)

## Resumen

* [Descargar](https://github.com/rubygems/rubygems/releases/download/v2.2.3/rubygems-update-2.2.3.gem) e instalar manualmente el update_rubygems correspondiente a nuestra versión de rubygems.
{% highlight bash %}
C:\>gem install --local C:\rubygems-update-2.2.3.gem
{% endhighlight %}
* Actualizar rubygems.
{% highlight bash %}
C:\>update_rubygems --no-ri --no-rdoc
{% endhighlight %}
* Localizar la ubicacion de gem.
{% highlight bash %}
C:\>gem which rubygems
C:/Ruby21/lib/ruby/2.1.0/rubygems.rb
# => la carpeta sera C:/Ruby21/lib/ruby/2.1.0/ssl_certs
{% endhighlight %}
* [Descargar](https://raw.githubusercontent.com/rubygems/rubygems/master/lib/rubygems/ssl_certs/AddTrustExternalCARoot-2048.pem) y copiar el nuevo certificado en la carpeta indicada en el pto anterior. 
