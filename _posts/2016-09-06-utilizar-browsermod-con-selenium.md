---
layout: post
title: Utilizar Browsermod-proxy con Selenium
description: Utilizar Browsermod-proxy con Selenium para capturar la navegación en un HAR en ruby
categories: ruby
tags: browsermod selenium har ruby
---

[BrowserMob Proxy](http://bmp.lightbody.net/) es un proxy que nos permite captura la navegación que realizamos en archivos HAR para su posterior analisis.
Se integra con java, python, ruby, pero en este ejemplo, he utilizado ruby y su [Ruby client para BrowserMob Proxy](https://github.com/jarib/browsermob-proxy-rb). Una vez instalado el BrowserMod en nuestra máquina, este seria un ejemplo sencillo de su utilización para guardar el HAR en un archivo.

{% highlight ruby %}
require 'selenium/webdriver'
require 'browsermob/proxy'

path = "[PATH_BROWSERMOD_PROXY]"
server = BrowserMob::Proxy::Server.new(path)
server.start

proxy = server.create_proxy

proxy_conf = Selenium::WebDriver::Proxy.new(:http => proxy.selenium_proxy.http)
caps = Selenium::WebDriver::Remote::Capabilities.chrome(:proxy => proxy_conf)
driver = Selenium::WebDriver.for(:chrome, :desired_capabilities => caps)

proxy.new_har("google",{:capture_content => true, :capture_headers => true})
driver.get "http://jamvius.github.io"

har = proxy.har
har.save_to "/tmp/google.har"

proxy.close
driver.quit
{% endhighlight %}