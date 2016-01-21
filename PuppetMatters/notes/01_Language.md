# Resources reference - Overview

### Where to find docs about Puppet resources

### Main resources: package, service, file, user, exec

### Language Style



# Managing files

Files are the most configured resources on a system, we manage them with the **file** type:

    file { 'httpd.conf':
        # (namevar) The file path
        path      => '/etc/httpd/conf/httpd.conf',  
        # Define the file type and if it should exist:
        # 'present','absent','directory','link'
        ensure    => 'present',
        # Url from where to retrieve the file content
        source    => 'puppet://[puppetfileserver]/<share>/path',
        # Actual content of the file, alternative to source
        # Typically it contains a reference to the template function
        content   => 'My content',
        # Typical file's attributes
        owner     => 'root',
        group     => 'root',
        mode      => '0644',
        # The sylink target, when ensure => link
        target    => '/etc/httpd/httpd.conf',
        # Whether to recursively manage a directory (when ensure => directory)
        recurse   => true,
    }


# Managing users

Puppet has native types to manage users and groups, allowing easy addition, modification and removal. Here are the main arguments of the **user** type:

    user { 'joe':
        # (namevar) The user name
        name      => 'joe',  
        # The user's status: 'present','absent','role'
        ensure    => 'present',
        # The user's  id
        uid       => '1001',
        # The user's primary group id
        gid       => '1001',
        # Eventual user's secondary groups (use array for many)
        groups    => [ 'admins' , 'developers' ],
        # The user's password. As it appears in /etc/shadow
        # Use single quotes to avoid unanted evaluation of $* as variables
        password  => '$6$ZFS5JFFRZc$FFDSvPZSSFGVdXDlHe…',
        # Typical users' attributes
        shell     => '/bin/bash',
        home      => '/home/joe',
        mode      => '0644',
    }

# Puppet language style

Puppet language as an official [Style Guide](http://docs.puppetlabs.com/guides/style_guide.html) which defines recommended rules on how to write the code.

The standard de facto tool to check the code style is [puppet-lint](http://puppet-lint.com/).

Badly formatted example:

     file {
     "/etc/issue":
         content => "Welcome to $fqdn",
         ensure => present,
          mode => 644,
         group => "root",
         path => "${issue_file_path}",
         }

Corrected style:

    file { '/etc/issue':
      ensure  => present,
      content => "Welcome to ${fqdn}",
      mode    => 0644,
      group   => 'root',
      path    => $issue_file_path,
    }

# Resources reference - Practice

Create a manifest that contains all the explored resources: package, service, file, exec, user.

Use Pupppet Lint to verify its style.
# Language reference - Overview



# Class inheritance
In Puppet classes are just containers of resources and have nothing to do with OOP classes. Therefore the meaning of class inheritance is somehow limited to few specific cases.

When using class inheritance, the main class ('puppet' in the sample below) is always evaluated first and all the variables and resource defaults it sets are available in the scope of the child class ('puppet::server').

Moreover the child class can override the arguments of a resource defined in the main class. Note the syntax used when referring to the existing resource File['/etc/puppet/puppet.conf']:

    class puppet {
      file { '/etc/puppet/puppet.conf':
        content => template('puppet/client/puppet.conf'),
      }
    }

    class puppet::server inherits puppet {
      File['/etc/puppet/puppet.conf'] {
        content => template('puppet/server/puppet.conf'),
      }
    }



# Managing dependencies
Puppet language is declarative and not procedural: it defines states, the order in which resources are written in manifests does not affect the order in which they are applied to the desired state.

To manage resources ordering, there are 3 different methods, which can cohexist:

  1 - Use the metaparameters **before**, **require**, **notify**, **subscribe**

  2 - Use the **Chaining arrows** (compared to the above metaparamers: **->** , **<-** , **<~** , **~>**)

  3 - Use run stages

# Managing dependencies - before | notify

In a typical Package/Service/Configuration file example we want the package to be installed first, configure it and then start the service, eventually managing its restart if the config file changes.

This can be expressed with metaparameters:

    package { 'exim':
      before => File['exim.conf'],  
    }

    file { 'exim.conf':
      notify => Service['exim'],
    }

    service { 'exim':
    }

which is equivalent to

    Package['exim'] -> File['exim.conf'] ~> Service['exim']


# Managing dependencies - require | subscribe

The previous example can be expressed using the alternative reverse metaparameters:

    package { 'exim':
    }

    file { 'exim.conf':
      require => Package['exim'],
    }

    service { 'exim':
      subscribe => File['exim.conf'],
    }

which can also be expressed like:

    Service['exim'] <~ File['exim.conf'] <- Package['exim']


# Conditionals
Puppet provides different constructs to manage conditionals inside manifests:

**Selectors** allows to set the value of a variable or an argument inside a resource declaration according to the value of another variable.
Selectors therefore just returns values and are not used to manage conditionally entire blocks of code.

**case statements** are used to execute different blocks of code according to the values of a variable. It's possible to have a default block for unmatched entries.
Case statements are NOT used inside resource declarations.

**if elsif else** conditionals, like case, are used to execute different blocks of code and can't be used inside resources declarations.
We can can use any of Puppet's comparison expressions and we can combine more than one for complex patterns matching.

**unless** is somehow the opposite of **if**. It evaluates a boolean condition and if it's *false* it executes a block of code. It doesn't have elsif / else clauses.

# Sample: Assign a variable value

#### Selector for variable's assignement

     $package_name = $osfamily ? {
       'RedHat' => 'httpd',
       'Debian' => 'apache2',
       default  => undef,
     }

#### case

     case $::osfamily {
       'Debian': { $package_name = 'apache2' }
       'RedHat': { $package_name = 'httpd' }
       default: { notify { "Operating system $::operatingsystem not supported" } }
     }

#### if elsif else

     if $::osfamily == 'Debian' {       $package_name = 'apache2'
     } elsif $::osfamily == 'RedHat' {       $package_name = 'httpd'
     } else {       notify { "Operating system $::operatingsystem not supported" }     }

# Comparing strings: operators

Puppet supports some common comparison operators: ```==  !=   <  >  <=  >=  =~  !~``` and the somehow less common ```in```

     if $::osfamily == 'Debian' { [ ... ] }

     if $::kernel != 'Linux' { [ ... ] }

     if $::uptime_days > 365 { [ ... ] }

     if $::operatingsystemrelease <= 6 { [ ... ] }


# Comparing strings: in operator and combinations

## in operator
The in operator checks if a string present in another string, an array or in the keys of an hash

     if '64' in $::architecture

     if $monitor_tool in [ 'nagios' , 'icinga' , 'sensu' ]

## Expressions combinations
It's possible to combine multiple comparisons with **and** and **or**

    if ($::osfamily == 'RedHat')
    and ($::operatingsystemrelease == '5') {
       [ ... ]
    }

    if ($::osfamily == 'Debian') or ($::osfamily == 'RedHat') {
       [ ...]
    }
