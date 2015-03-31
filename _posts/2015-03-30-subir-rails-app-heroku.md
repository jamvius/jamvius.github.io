---
layout: post
title: Como subir una app rails a heroku
categories: rails sysop
tags: rails deploy heroku
---

## Configurar App

si tenemos un sitio en rails (también da soporte python, nodejs, java, clousure...) 
que queremos subirlo a internet para probarlo [Heroku](http://www.heroku.com) es una gran alternativa.
Para poder usar Heroku debemos crearnos una cuenta y instalarlos sus Toolbelt. 
Un buen punto de partida para hacer todo esto es su [QuickStart](https://devcenter.heroku.com/articles/quickstart).

Para deployar en heroku deberemos hacer unos pequeños cambios en nuestro <code>Gemfile</code>. 
Heroku usa Postgres como base de datos, por lo que deberemos añadir las gemas en entorno de producción.
Tambien deberemos poner la gem sqlite3 solo en los grupos development y test.

{% highlight ruby %}
group :development, :test do
  gem 'sqlite3'
end
group :production do
  gem "pg"
  gem "rails_12factor"
end
{% endhighlight %}

Y ejecutar <code>bundle install --without production</code> para actualizar las dependencias. 
Una vez actualizados debemos realizar un commit para tener la última versión en git.

{% highlight bash %}
# => Si todavia no se tiene el proyecto en git, sera necesario añadirlo con 
# => git init
# => git commit -a -m "version inicial"
$ git commit -a -m "Añadidas dependecias para heroku y actualizado Gemfile.lock"
{% endhighlight %}

## Subir la app

El siguiente paso es crear una nueva app en Heroku. Para ello ejecutamos <code>heroku create</code>
{% highlight bash %}
$ heroku create
Creating radiant-island-4647... done, stack is cedar-14
https://radiant-island-4647.herokuapp.com/ | https://git.heroku.com/radiant-island-4647.git
Git remote heroku added
{% endhighlight %}

Nos creará un nombre aleatorio, que asignará como repositorio remoto y como subdominio en el cual estará alojado nuestra aplicación.

Si queremos definir el nombre de nuestro subdominio, podemos entrar al entorno de administración de Heroku,
crear la app con el nombre que mas nos guste y configurar en nuestra app el repositorio remoto
{% highlight bash %}
cd my-project/
$ git init
$ heroku git:remote -a my-project
{% endhighlight %}

Una vez configurado, lo único que nos falta es hacer un push de la última versión de nuestra app.
Para ello ejecutaremos <code>git push heroku master</code>. Al realizar el push, Heroku adaptará nuestro proyecto 
(BBDD y logs) para su correcto funcionamiento
{% highlight bash %}
$ git push heroku master
Counting objects: 90, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (82/82), done.
Writing objects: 100% (90/90), 21.44 KiB | 0 bytes/s, done.
Total 90 (delta 4), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Ruby app detected
remote: -----> Compiling Ruby/Rails
remote: -----> Using Ruby version: ruby-2.0.0
remote: -----> Installing dependencies using 1.7.12
remote:        Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin -j4 --deployment
remote:        Fetching gem metadata from https://rubygems.org/...........
remote:        Installing rake 10.4.2
[...] Instala todas las gemas [...]
remote:        Installing turbolinks 2.5.3
remote:        Your bundle is complete!
remote:        Gems in the groups development and test were not installed.
remote:        It was installed into ./vendor/bundle
remote:        Post-install message from rdoc:
remote:        Depending on your version of ruby, you may need to install ruby rdoc/ri data:
remote:        <= 1.8.6 : unsupported
remote:        = 1.8.7 : gem install rdoc-data; rdoc-data --install
remote:        = 1.9.1 : gem install rdoc-data; rdoc-data --install
remote:        >= 1.9.2 : nothing to do! Yay!
remote:        Bundle completed (34.42s)
remote:        Cleaning up the bundler cache.
remote: -----> Preparing app for Rails asset pipeline
remote:        Running: rake assets:precompile
remote:        I, [2015-03-25T23:07:25.573293 #1159]  INFO -- : Writing /tmp/build_b8e3435b0d8e41346147ce1d18e9b308/public/assets/application-47fe71a3b34a93e1929c175b1755d405.js
remote:        I, [2015-03-25T23:07:25.661104 #1159]  INFO -- : Writing /tmp/build_b8e3435b0d8e41346147ce1d18e9b308/public/assets/application-3942007d31710307dd44000cb1f768c9.css
remote:        Asset precompilation completed (6.79s)
remote:        Cleaning assets
remote:        Running: rake assets:clean
remote:
remote: ###### WARNING:
remote:        You have not declared a Ruby version in your Gemfile.
remote:        To set your Ruby version add this line to your Gemfile:
remote:        ruby '2.0.0'
remote:        # See https://devcenter.heroku.com/articles/ruby-versions for more information.
remote:
remote: ###### WARNING:
remote:        No Procfile detected, using the default web server (webrick)
remote:        https://devcenter.heroku.com/articles/ruby-default-web-server
remote:
remote: -----> Discovering process types
remote:        Procfile declares types -> (none)
remote:        Default types for Ruby  -> console, rake, web, worker
remote:
remote: -----> Compressing... done, 29.8MB
remote: -----> Launching... done, v6
remote:        https://radiant-island-4647.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/radiant-island-4647.git
 * [new branch]      master -> master
{% endhighlight %}

Ya solo falta crear las tablas de BBDD ejecutando <code>heroku run rake db:migrate</code> y estaremos dispuesto 
para visualizar nuestra app con <code>heroku open</code>

<div class="note info">
  <p>En produccion, si no se define en el <code>router.rb</code>, la raiz del dominio no devuelve nada, 
  al contrario que el entorno de desarrollo</p>
</div>

## Opcional
Posiblemente la primera vez que subamos una app a Heroku nos saldran algunos de los siguientes warnings: 
- Definir version ruby: Esto se soluciona añadiendo al <code>Gemfile</code> la versión de ruby que utiliza nuestro código:
{% highlight ruby %}
ruby '2.2.1'
{% endhighlight %}
- No existe Procfile: Este archivo permite configurar los procesos que utilizan las apps, y como se arrancan. En el caso básico, 
será un proceso web, que arranca el servidor. Heroku recomienda utilizar como servidor [Puma](https://devcenter.heroku.com/articles/deploying-rails-applications-with-the-puma-web-server) en vez de webrick.
Para configurarlo tendremos que poner en el <code>Procfile</code>:

{% highlight ruby %}
web: bundle exec puma -C config/puma.rb
{% endhighlight %}

Añadir a <code>Gemfile</code>:
{% highlight ruby %}
gem 'puma'
{% endhighlight %}

Y crear el archivo <code>./config/puma.rb</code> con:

{% highlight ruby %}
workers Integer(ENV['WEB_CONCURRENCY'] || 2)
threads_count = Integer(ENV['MAX_THREADS'] || 5)
threads threads_count, threads_count

preload_app!

rackup      DefaultRackup
port        ENV['PORT']     || 3000
environment ENV['RACK_ENV'] || 'development'

on_worker_boot do
  # Worker specific setup for Rails 4.1+
  # See: https://devcenter.heroku.com/articles/deploying-rails-applications-with-the-puma-web-server#on-worker-boot
  ActiveRecord::Base.establish_connection
end
{% endhighlight %}

Ahora solo tenemos que actualizar el código en heroku para tener la nueva versión:
{% highlight bash %}
$ git commit -a -m "Corrigiendo warnings de heroku"
$ git push heroku master
{% endhighlight %}
