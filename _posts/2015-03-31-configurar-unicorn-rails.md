---
layout: post
title: Como configurar unicorn como servidor en rails
categories: rails 
tags: rails 
---

Para configurarlo tendremos que poner en el <code>Procfile</code>:

{% highlight ruby %}
web: bundle exec unicorn -p $PORT -c ./config/unicorn.rb
{% endhighlight %}

Añadir a <code>Gemfile</code>:
{% highlight ruby %}
gem 'unicorn'
{% endhighlight %}

Y crear el archivo <code>./config/unicorn.rb</code> con:

{% highlight ruby %}
worker_processes Integer(ENV["WEB_CONCURRENCY"] || 3)
timeout 15
preload_app true

before_fork do |server, worker|
  Signal.trap 'TERM' do
    puts 'Unicorn master intercepting TERM and sending myself QUIT instead'
    Process.kill 'QUIT', Process.pid
  end

  defined?(ActiveRecord::Base) and
    ActiveRecord::Base.connection.disconnect!
end

after_fork do |server, worker|
  Signal.trap 'TERM' do
    puts 'Unicorn worker intercepting TERM and doing nothing. Wait for master to send QUIT'
  end

  defined?(ActiveRecord::Base) and
    ActiveRecord::Base.establish_connection
end
{% endhighlight %}
