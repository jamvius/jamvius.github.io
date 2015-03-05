---
layout: post
title: Probando SSHKit
categories: ruby
tags: ruby ssh
---

[SSHKit](https://github.com/capistrano/sshkit) es una gema que permite realizar acciones automatizadas ssh
en diversos servidores de manera sencilla.
Un Ejemplo sencillo que permite conectarse a varios servidores y hacer un tail seria:

{% highlight ruby %}
require 'sshkit'
require 'sshkit/dsl'

SSHKit::Backend::Netssh.configure do |ssh|
  ssh.ssh_options = {
      user: '<username>',
  	  password: '<password>'
  }
end

SSHKit.config.output_verbosity = :debug
SSHKit.config.format = :pretty

servers_list = %w{<server1> <server2>}
site_dir = '<directorio>'

on servers_list do |host|
  within site_dir do
    execute(:tail, '-20', 'server.log')
  end
end
{% endhighlight %}

