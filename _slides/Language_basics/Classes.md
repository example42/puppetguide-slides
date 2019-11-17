# Classes

Classes are **containers** of different resources. Since Puppet 2.6 they can have parameters.

Example of a class **definition** (here we describe what the class does and what parameters it has, we don't actually add it and its resources to the catalog):

    class mysql (
      root_password => 'default_value',
      port          => '3306',
    ) {
      package { 'mysql-server': ensure => present }
      service { 'mysql': ensure => running }
      [...]
    }

When we have to use a class previously defined, we **declare** it. Class declaration can be done in 2 different ways:

Class declaration without parameters (inside a catalog we can have multiple ```include``` of the same class but that class it's applied only once):

    include mysql

This is similar to:

    require mysql # Include and require the class
    contain mysql # Include the class and be sure that all classes contained there are handled together 

Class declaration with explicit parameters, available from Puppet 2.6. Syntax is the same of normal resources and the same class can be declared, in this way, only once inside the same catalog:

    class { 'mysql':
      root_password => 'my_value',
      port          => '3307',
    }

# Defines

Also called: **Defined resource types** or **defined types**

Defined resource types are written in Puppet DSL and can make use of existing resource types or of other defined resource types.

They are similar to parametrized classes but can be used multiple times (with different titles), they are used as normal native types like package, service etc.

**Definition** of a define:

    define apache::virtualhost (
      $ensure   = present,
      $template = 'apache/virtualhost.conf.erb' ,
      [...] ) {

      file { "ApacheVirtualHost_${name}":
        ensure  => $ensure,
        content => template("${template}"),
      }
    }

**Declaration** of a define:

    apache::virtualhost { 'www.example42.com':
      template => 'site/apache/www.example42.com-erb'
    }

# Class and define parameters

Classes and defines can have parameters, according to the values given to these parameters user can customized their behaviour and generated results. Parameters are variables usable inside the same class or define (or in templates used there).

Starting from Puppet 4 parameters can be validated using the (very flexible and powerful) Puppet Data type system.

Class definition in older Puppet versions: 

    class motd (
      $content => 'This is the motd',
    ) {
      file { '/etc/motd':
        content => $content,
      }
    }
  
Same class with parameters validation from Puppet 4:

    class motd (
      String $content => 'This is the motd',
    ) {
      file { '/etc/motd':
        content => $content,
      }
    }

A variable defined in a class can be used another class by using its fully qualified name ($<class_name>::<variable_name>). For example we can refer in a class different than `motd` its `$content` variable with: `$::motd::content`. The only condition is that the class where the variable is set must be parsed (classified, in this case) before the class that uses it.
