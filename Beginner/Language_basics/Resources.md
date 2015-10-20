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
