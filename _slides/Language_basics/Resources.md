# Resource Types (Types)

Resources (also called Resource Types and Types) are single **units of configuration** that potentially can manage any "object" in an Operating System or more widely in an IT infrastructure.

A resources is composed by:

- A **type** (package, service, file, user, mount, exec, interface, ec2_instance ...)
- A **title** (how the resource is called and referred in Puppet code)
- Zero or more **arguments**

The syntax is always as follows:

    @@@ puppet
    type { 'title':
      argument  => value,
      other_arg => value,
    }

Example for a **file** resource type:

    @@@ puppet
    file { 'motd':
      ensure  => file,
      path    => '/etc/motd',
      content => 'Tomorrow is another day',
    }


# Resource Types documentation

Information about resource types and their documentation can be found in different places:

  - Online is published the complete [Type Reference](http://docs.puppetlabs.com/references/latest/type.html) for the latest or earlier versions of Puppet.

  - The `puppet describe` command:

        @@@ shell
        puppet describe <resource_type>
      
    for example, to find from the command line information about the file resource:

        @@@ shell
        puppet describe file

    To list the description of ll the available types, run:
    
        @@@ shell
        puppet describe --list

  - Give a glance to Puppet code for the list of **native** resource types (the ones written in Ruby language, based on the types and providers pattern):

        @@@ shell
        ls $(facter rubysitedir)/puppet/type

# Simple samples of resources

The most common native resources, shipped with Puppet by default are: package, service, file, user, group, cron, exec, mount. Here are some simple examples.

Installation of OpenSSH package:

    @@@ puppet
    package { 'openssh':
      ensure => present,
    }

Creation of /etc/motd file:

    @@@ puppet
    file { 'motd':
      ensure => file,
      path   => '/etc/motd',
    }

Start of httpd service:

    @@@ puppet
    service { 'httpd':
      ensure => running,
      enable => true,
    }

Creation of oscar user:

    @@@ puppet
    user { 'oscar':
      ensure => present,
      uid    => 1024,
    }

Each of these resources have several other arguments that allows to define every characteristic of the resource.


# More complex examples

Here are some more complex examples with usage of variables, resource references, arrays and relationships.

Management of nginx service with parameters defined in module's variables

    @@@ puppet
    service { 'nginx':
      ensure     => $::nginx::manage_service_ensure,
      name       => $::nginx::service_name,
      enable     => $::nginx::manage_service_enable,
    }

Creation of nginx.conf with content retrieved from different sources (first found is served)

    @@@ puppet
    file { 'nginx.conf':
      ensure  => file,
      path    => '/etc/nginx/nginx.conf',
      source  => [
          "puppet:///modules/site/nginx.conf--${::fqdn}",
          "puppet:///modules/site/nginx.conf"
      ],
    }

Installation of the Apache package triggering a restart of the relevant service:

    @@@ puppet
    package { 'httpd':
      ensure => $ensure,
      name   => $apache_package,
      notify => Class['Apache::Service'],
    }


# Resource Abstraction Layer (RAL)

Resources are abstracted from the underlying OS, this is achieved via the **Resource Abstraction Layer** (RAL) composed of resource **types** that can have different **providers**.

A type specifies the attributes that a given resource may have, a provider implements the relevant type on the underlying Operating System.

For example the ```package``` type is known for the great number of providers (yum, apt, msi, gem ... ).

    @@@ shell
    ls $(facter rubysitedir)/puppet/provider/package

With the command ```puppet resource``` we can represent the current status of a system's resources in Puppet language (note this can be done for any resource, even the ones not managed by Puppet):

To show all the existing users on a system (or only the root user):

    @@@ shell
    puppet resource user
    puppet resource user root

To show all the installed packages:

    @@@ shell
    puppet resource package

To show all the system's services:

    @@@ shell
    puppet resource service

It's also possible to directly modify them with ```puppet resource``` (note that this is not generally the way Puppet is used to manage the system's resources):

    @@@ shell
    puppet resource service httpd ensure=running enable=true
