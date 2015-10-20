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

"Old style" class declaration, without parameters (inside a catalog we can have multiple ```include``` of the same class but that class it's applied only once):

    include mysql

"New style" (from Puppet 2.6) class declaration with explicit parameters (Syntax is the same of normal resources and the same class can be declared, in this way, only once inside the same catalog):

    class { 'mysql':
      root_password => 'my_value',
      port          => '3307',
    }


# Defines

Also called: **Defined resource types** or **defined types**

Similar to parametrized classes but can be used multiple times (with different titles).

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
