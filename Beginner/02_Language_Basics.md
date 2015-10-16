# Language Basics - Overview

- Nodes classification
- The Catalog
- Variables and parameters
- Resource types
- Classes and defines
- Modules


# Nodes classification

When clients connect, the Puppet Master generates a **catalog** with the list of the resources that clients have to apply locally.

The Puppet Master has to *classify* nodes and define for each of them:

- The **classes** to include
- The **parameters** to pass
- The Puppet **environment** to use

Nodes classification can be done in different ways (more details will follow):

- Using the ```node``` statement in Puppet
- Using and **External Node Classifier** (ENC): a separated tool that provides classification info
- Using the ```hiera_include``` function
- Using a nodeless setup: the classes to include are defined according to variables and facts.


# Variables

In our code we can define our **variables** and use other ones that may come from different sources:

- **facts** generated directly by the client
- **parameters** obtained from node's classification
- Puppet **internal** variables

### Facts

**Facter** runs on clients and collects **facts** that the server can use as variables

    al$ facter

    architecture => x86_64
    fqdn => Macante.example42.com
    hostname => Macante
    ipaddress_eth0 => 10.42.42.98
    macaddress_eth0 => 20:c9:d0:44:61:57
    operatingsystem => Centos
    operatingsystemrelease => 6.3
    osfamily => RedHat
    virtual => physical


### User Variables

We can define custom variables in our Puppet code:

    $role = 'mail'

    $package = $::operatingsystem ? {
      /(?i:Ubuntu|Debian|Mint)/ => 'apache2',
      default                   => 'httpd',
    }



# Resource Types (Types)

Resource Types are single **units of configuration** composed by:

- A **type** (package, service, file, user, mount, exec ...)
- A **title** (how is called and referred)
- Zero or more **arguments**

The syntax is as follows:

    type { 'title':
      argument  => value,
      other_arg => value,
    }

Example for a **file** resource type:

    file { 'motd':
      path    => '/etc/motd',
      content => 'Tomorrow is another day',
    }


# Resource Types reference

Find online the complete [Type Reference](http://docs.puppetlabs.com/references/latest/type.html) for the latest or earlier versions.

From the shell the command line interface:

    puppet describe file

For the full list of available descriptions try:

    puppet describe --list

Give a glance to Puppet code for the list of **native** resource types:

    ls $(facter rubysitedir)/puppet/type

The most common native resources, shipped with Puppet by default are: package, service, file, user, group, cron, exec, mount...

# Simple samples of resources

Installation of OpenSSH package:

    package { 'openssh':
      ensure => present,
    }

Creation of /etc/motd file:

    file { 'motd':
      path => '/etc/motd',
    }

Start of httpd service:

    service { 'httpd':
      ensure => running,
      enable => true,
    }

Creation of oscar user:

    user { 'oscar':
      ensure => present,
      uid    => 1024,
    }

Each of these resources have several other arguments that allows to define every characteristic of the resource.


# More complex examples

Here are some more complex examples with usage of variables, resource references, arrays and relationships.

Management of nginx service with parameters defined in module's variables

    service { 'nginx':
      ensure     => $::nginx::manage_service_ensure,
      name       => $::nginx::service_name,
      enable     => $::nginx::manage_service_enable,
    }

Creation of nginx.conf with content retrieved from different sources (first found is served)

    file { 'nginx.conf':
      ensure  => present,
      path    => '/etc/nginx/nginx.conf',
      source  => [
          "puppet:///modules/site/nginx.conf--${::fqdn}",
          "puppet:///modules/site/nginx.conf"
      ],
    }

Installation of the Apache package triggering a restart of the relevant service:

    package { 'httpd':
      ensure => $ensure,
      name   => $apache_package,
      notify => Class['Apache::Service'],
    }


# Resource Abstraction Layer

Resources are abstracted from the underlying OS, this is achieved via the **Resource Abstraction Layer** (RAL) composed of resource **types** that can have different **providers**.

A type specifies the attributes that a given resource may have, a provider implements the relevant type on the underlying Operating System.

For example the ```package``` type is known for the great number of providers (yum, apt, msi, gem ... ).

    ls $(facter rubysitedir)/puppet/provider/package

With the command ```puppet resource``` we can represent the current status of a system's resources in Puppet language (note this can be done for any resource, even the ones not managed by Puppet):

To show all the exisiting users on a system (or only the root user):

    puppet resource user
    puppet resource user root

To show all the installed packages:

    puppet resource package

To show all the system's services:

    puppet resource service

It's also possible to directly modify them with ```puppet resource``` (note that this is not generally the way Puppet is used to manage the system's resources):

    puppet resource service httpd ensure=running enable=true


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


# The Catalog

The **catalog** is the complete list of resources, and their relationships, that the Puppet Master generates for the client and sends it in Json format.

It's the result of all the puppet code and logic that we define for a given node in our manifests and is applied on the client after it has been received from the master.

The client uses the RAL (Resource Abstraction Layer) to execute the actual system's commands that convert abstract resources like

    package { 'openssh': }

to their actual fulfillment on the system (```apt-get install openssh``` , ```yum install openssh``` ...).

The catalog is saved by the client in ```$libdir/client_data/catalog/$certname.json```


# Practice: Language Basics

On a test machine **install Puppet** if not already installed.

Practice with the **commands**:

    puppet describe
    puppet resource
    facter

Create a **manifest** file and in that file manage the installation of the package and the management of the service of *nginx*.

Use ```puppet apply``` to apply the resources declared in our manifest.
