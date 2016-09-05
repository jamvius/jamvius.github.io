---
layout: post
title: Utilizar firefox con Selenium
description: Como configurar Selenium con Firefox.
categories: testing
tags: selenium firefox
---

En las últimas versiones, [Firefox y Selenium estan teniendo problemas de compatibilidad](http://stackoverflow.com/questions/37761668/cant-open-browser-with-selenium-after-firefox-update), por lo que se recomienda utilizar el nuevo driver [Marionette](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette/WebDriver) que utiliza [GeckoDriver](https://github.com/mozilla/geckodriver)

Para ello deberemos utilizar la nueva versión 3.0 de Selenium que esta en beta.
{% highlight bash %}
$ gem install selenium-webdriver -v '3.0.0.beta3.1'
{% endhighlight %}

Y despues configurar la inicialización del driver indicando que use marionette
{% highlight ruby %}
driver = Selenium::WebDriver.for :firefox, marionette: true
{% endhighlight %}
