---
layout: post
title: Utilizar Selenium Grid en python
description: Como configurar y arrancar selenium grid y utilizarlo desde python
categories: python
tags: selenium grid 
---

[Selenium Grid](https://github.com/SeleniumHQ/selenium/wiki/Grid2) permite definir un conjunto de nodos sobre los que poder realizar pruebas en paralelo.
Para ello debemos [bajarnos](http://selenium-release.storage.googleapis.com/index.html) selenium server y arrancar un hub:
{% highlight bash %}
$ java -jar selenium-server-standalone-2.53.1.jar -role hub
{% endhighlight %}

y tantos nodos como queramos
{% highlight bash %}
$ java -jar selenium-server-standalone-2.53.1.jar -role node -hub http://localhost:4444/grid/register
{% endhighlight %}

Desde código, para utilizar el hub que acabamos de arrancar
{% highlight python %}
from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities

browser = webdriver.Remote(command_executor='http://127.0.0.1:4444/wd/hub', desired_capabilities=DesiredCapabilities.CHROME)

url = "http://jamvius.github.io"
browser.maximize_window()
browser.get(url)

browser.quit()
{% endhighlight %}