---
layout: post
title: Utilizar Browsermod-proxy con Selenium en python
description: Utilizar Browsermod-proxy con Selenium para capturar la navegación en un HAR en python
categories: python
tags: browsermod selenium har 
---

Despues de probar BrowserMob en **ruby**, me he encontrado con algunos problemas, debido a que la conector hace un par de años que no se actualiza, por lo que he optado por probar la [versión python](https://browsermob-proxy-py.readthedocs.io). Este seria un ejemplo para utilizar **browsermod-proxy** desde **selenium**

{% highlight python %}
from browsermobproxy import Server
from selenium import webdriver

server = Server([path_browsermob])
server.start()
proxy = server.create_proxy()
proxy.new_har("google", {'captureHeaders': True, 'captureContent': True})

chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument("--proxy-server={0}".format(proxy.proxy))

browser = webdriver.Chrome(chrome_options = chrome_options)
browser.get("http://jamvius.github.io/")

har = proxy.har

server.stop()
browser.quit()
{% endhighlight %}