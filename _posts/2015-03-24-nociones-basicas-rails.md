---
layout: post
title: Nociones básicas de rails
categories: rails 
tags: rails 
---

## Generar app

Crear una app en un directorio
{% highlight bash %}
$ # => rails new <app_name>
$ rails new Blog
{% endhighlight %}

### Opciones
* **--skip-bundle**: Desactiva la ejecucion del <code>bundle install</code> despues de descargar las dependencias
* **-d postgresql**: Selecciona la BBDD (defecto sqlite3)
* **--skip-active-record**: Si no queremos que nos cree la configuración de ActiveRecord (p.e. si no usamos BB.DD no relacionales como mongodb)
* **--skip-test-unit**: Para no generar el codigo de test

Si tenemos varias versiones de rails instaladas y queremos utilizar una versión que no sea la ultima
(la por defecto) hay que indicar la versión entre underlines

{% highlight bash %}
$ rails _4.1.8_ new Blog
{% endhighlight %}

Crear en el directorio actual
{% highlight bash %}
$ rails new . 
{% endhighlight %}

Ahora para arrancarlo solo tenemos que ejecutar
{% highlight bash %}
# => rails s|server
$ rails server 
=> Booting WEBrick
=> Rails 4.2.1 application starting in development on http://localhost:3000
=> Run `rails server -h` for more startup options
=> Ctrl-C to shutdown server
[2015-03-24 23:27:58] INFO  WEBrick 1.3.1
[2015-03-24 23:27:58] INFO  ruby 2.2.1 (2015-02-26) [x86_64-darwin14]
[2015-03-24 23:27:58] INFO  WEBrick::HTTPServer#start: pid=1589 port=3000
{% endhighlight %}

## Generar codigo
Si queremos generar codigo, podemos usar la opción <code>generate (g)</code> de rails
{% highlight bash %}
# => rails g scaffold <modelo> <campo1>:(string|integer|boolean|references) campo2 ... campoN [opciones]
$ rails g scaffold Post title description year:integer
     invoke  active_record
      create    db/migrate/20150324224320_create_posts.rb
      create    app/models/post.rb
      invoke    test_unit
      create      test/models/post_test.rb
      create      test/fixtures/posts.yml
      invoke  resource_route
       route    resources :posts
      invoke  scaffold_controller
      create    app/controllers/posts_controller.rb
      invoke    erb
      create      app/views/posts
      create      app/views/posts/index.html.erb
      create      app/views/posts/edit.html.erb
      create      app/views/posts/show.html.erb
      create      app/views/posts/new.html.erb
      create      app/views/posts/_form.html.erb
      invoke    test_unit
      create      test/controllers/posts_controller_test.rb
      invoke    helper
      create      app/helpers/posts_helper.rb
      invoke      test_unit
      invoke    jbuilder
      create      app/views/posts/index.json.jbuilder
      create      app/views/posts/show.json.jbuilder
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/posts.coffee
      invoke    scss
      create      app/assets/stylesheets/posts.scss
      invoke  scss
      create    app/assets/stylesheets/scaffolds.scss
{% endhighlight %}

### Opciones
* **-t=spec**: Define la libreria que queremos usar para generar los tests
* **--skip-assets**: Si no queremos generar los asset para esta entidad

Si queremos recrear las BB.DD.
{% highlight bash %}
$ rake db:create
{% endhighlight %}

Para ejecutar los scripts de migracion que recrean los models
{% highlight bash %}
$ rake db:migrate
{% endhighlight %}

Si queremos inicializar la app con datos, podemos introducirlos en el <code>seed.rb</code> y se ejecutaran con:
{% highlight bash %}
$ rake db:seed
{% endhighlight %}

el <code>db:setup</code> ejecuta en schema.rb y el seed.rb, pero si se cambia los archivos de migrate no se actualiza el schema.rb
automaticamente (no se cuando)

Para borrar lo generado con un scaffold p.e.
{% highlight bash %}
$ rails d scaffold Post
{% endhighlight %}

