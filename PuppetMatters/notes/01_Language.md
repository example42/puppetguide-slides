# Resources reference - Overview

### Where to find docs about Puppet resources

### Main resources: package, service, file, user, exec

### Language Style


# Online documentation on types

#### Complete [Type Reference](http://docs.puppetlabs.com/references/latest/type.html)

This is the complete reference for Puppet types based on the latest version.

Check [here](http://docs.puppetlabs.com/references/index.html) for the reference on all the older versions.

Check the Puppet Core [Types Cheatsheet](http://docs.puppetlabs.com/puppet_core_types_cheatsheet.pdf) for an handy PDF with the essential reference.


# Inline documentation on types

#### Types reference documentation

We can check all the types documentation via the command line:

    puppet describe <type>

For a more compact output:

    puppet describe -s <type>

To show all the available resource types:

    puppet describe -l

#### Inspect existing resource types

To interactively inspect and modify our system's resources

    puppet resource <type> [name]

Remember we can use the same command to CHANGE our resources attibutes:

    puppet resource <type> <name> [attribute=value] [attribute2=value2]


# Managing packages

Installation of packages is managed by the **package** type.

The main arguments:

    package { 'apache':
      name      => 'httpd',  # (namevar)
      ensure    => 'present' # Values: 'absent', 'latest', '2.2.1'
      provider  => undef,    # Force an explicit provider
    }

# Managing services

Management of services is via the **service** type.

The main arguments:

    service { 'apache':
      name      => 'httpd',  # (namevar)
      ensure    => 'running' # Values: 'stopped', 'running'
      enable    => true,     # Define if to enable service at boot (true|false)
      hasstatus => true,     # Whether to use the init script' status to check
                             # if the service is running.
      pattern   => 'httpd',  # Name of the process to look for when hasstatus=false
    }

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

# Executing commands

We can run plain commands using Puppet's **exec** type. Since Puppet applies it at every run, either the command can be safely run multiple times or we have to use one of the **creates**, **unless**, **onlyif**, **refreshonly** arguments to manage when to execute it.

    exec { 'get_my_file':
        # (namevar) The command to execute
        command   => "wget http://mysite/myfile.tar.gz -O /tmp/myfile.tar.gz',
        # The search path for the command. Must exist when command is not absolute
        # Often set in Exec resource defaults
        path      => '/sbin:/bin:/usr/sbin:/usr/bin',
        # A file created by the command. It if exists, the command is not executed
        creates   => '/tmp/myfile.tar.gz',
        # A command or an array of commands, if any of them returns an error
        # the command is not executed
        onlyif    => 'ls /tmp/myfile.tar.gz && false',
        # A command or an array of commands, if any of them returns an error
        # the command IS executed
        unless    => 'ls /tmp/myfile.tar.gz',
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

### Referencing a resource

### Managing resources ordering

### Metaparameters

### Conditionals and

### Comparison operators

### Nodes and classes inheritance


# Resource references
In Puppet any resource is uniquely identified by its type and its name.
We can't have 2 resources of the same type with the same name in a catalog.

We have seen that we declare resources with a syntax like:

    type { 'name':
      arguments => values,
    }

When we need to reference to them in our code the syntax is like:

    Type['name']

Some examples:

    file { 'motd': ... }
    apache::virtualhost { 'example42.com': .... }
    exec { 'download_myapp': .... }

are referenced, respectively, with

    File['motd']
    Apache::Virtualhost['example42.com']
    Exec['download_myapp']


# Resource defaults
It's possible to set default argument values for a resource in order to reduce code duplication. The syntax is:

    Type {
      argument => value,
    }

Common examples:

    Exec {
      path => '/sbin:/bin:/usr/sbin:/usr/bin',
    }

    File {
      mode  => 0644,
      owner => 'root',
      group => 'root',
    }

Resource defaults can be overriden when declaring a specific resource of the same type.

Note that the "Area of Effect" of resource defaults might bring unexpected results. The general suggestion is:

Place **global** resource defaults in /etc/pupept/manifests/site.pp outside any node definition.

Place **local** resource defaults at the beginning of a class that uses them (mostly for clarity sake, as they are parse-order independent).

# Nodes inheritance
On the PuppetMaster we can define with the **node** definition the resources to apply to any node.

It is possible to have an inheritance structure for nodes, so that resources defined for a node are automatically included in an inheriting node.

An example:

    node 'general' { ... }

    node 'www01' inherits general { ... }

In Puppet versions prior to 3, it was possible to use nodes inheritance also to set variables and override them at different inheritance levels, and refer to these variables with their "short" name (not fully qualified).
When using this approach it was important to avoid the inclusion on classes in the inheritance tree, since some variables could be evaluated in an unexpected way.

This is no more possible because variables are not more dynamically scoped, and generally speaking nodes inheritance has been deprecated.



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


# Run Stages

In Puppet 2.6 it has been introduced the concept of Run Stages to help users in managing the order of dependencies when applying resources.

Puppet (> 2.6) provides a default **main** stage, we can add any number or further stages with the stage resource type:

    stage { 'pre':
      before => Stage['main'],
    }

Which is equivalent to:

    stage { 'pre': }
    Stage['pre'] -> Stage['main']

We can assign any class to a defined stage with the stage metaparameter:

    class { 'yum':
      stage => 'pre',
    }

Do not abuse of run stages (be vary of dependency cycles)!

[Official documentation on Run Stages](http://docs.puppetlabs.com/puppet/latest/reference/lang_run_stages.html)

# Metaparameters
Metaparameters are parameters available to any resource type, they can be used for different purposes:

 Manage dependencies (**before**, **require**, **subscribe**, **notify**, **stage**)

 Manage resources' application policies (**audit**, **noop**, **schedule**, **loglevel**)

 Add information to a resource (**alias**, **tag**)

[Official documentation on Metaparameters](http://docs.puppetlabs.com/puppet/latest/reference/metaparameter.html)


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

# Exported resources

When we need to provide to an host informations about resources present in another host, we need **exported resources**: resources declared in the catalog of a node (based on its facts and variables) but applied (collected) on another node.

Resources are declared with the special @@ notation which marks them as exported so that they are not applied to the node where they are declared:

    @@host { $::fqdn:
      ip  => $::ipaddress,
    }

    @@concat::fragment { "balance-fe-${::hostname}",
      target  => '/etc/haproxy/haproxy.cfg',
      content => "server ${::hostname} ${::ipaddress} maxconn 5000"
      tag     => "balance-fe",
    }

Once a catalog containing exported resources has been applied on a node and stored by the PuppetMaster (typically on PuppetDB), the exported resources can be collected with the spaceshift syntax (where is possible to specify search queries):

    Host << || >>
    Concat::Fragment <<| tag == "balance-fe" |>>
    Sshkey <<| |>>
    Nagios_service <<||>>

# Exported resources - Configuration

In order to use exported resources we need to enable on the Puppet Master the **storeconfigs** option and specify the backend to use.
We can do this configuring a PuppetMaster to use PuppetDB:

    storeconfigs = true
    storeconfigs_backend = puppetdb

In earlier Puppet versions storeconfigs is based on ActiveRecord, which is considerable slower.
