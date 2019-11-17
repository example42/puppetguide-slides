# Modules

Modules are Self Contained and Distributable *recipes* contained in a directory with a predefined structure.

They are used to manage an application, system's resources, a local site or more complex structures.

Common places where to find public modules are the [Puppet Forge](http://forge.puppet.com) and [GitHub](https://github.com/search?q=puppet).

Modules must be placed in the Puppet Master's modulepath, which is a double colon separated list of directories where Puppet looks for modules.

To see what's the local modulepath:

    puppet config print modulepath

Default module path, for root user, has changed over time. On Puppet pre 4 it is:

    /etc/puppet/modules:/usr/share/puppet/modules

Starting fromm Puppet 4, modulepath changes (as may other Puppet related directories):

    /etc/puppetlabs/code/environments/production/modules:/etc/puppetlabs/code/modules:/opt/puppetlabs/puppet/modules


# The puppet module subcommand

Puppet has a module module tool to interface with Puppet Modules Forge

    puppet help module
    [...]
    ACTIONS:
      build        Build a module release package.
      changes      Show modified files of an installed module.
      generate     Generate boilerplate for a new module.
      install      Install a module from the Puppet Forge or an archive.
      list         List installed modules
      search       Search the Puppet Forge for a module.
      uninstall    Uninstall a puppet module.
      upgrade      Upgrade a puppet module.

To search a module on the Forge:

    puppet module search elasticsearch

To install / uninstall / upgrade a module the module's author must be specified:

    puppet module install elastic/elasticsearch
    puppet module uninstall elastic/elasticsearch
    puppet module upgrade elastic/elasticsearch


# Paths of a module

  Modules have a standard structure:

    mysql/              # Main module directory

    mysql/manifests/    # Manifests directory. Puppet code here in .pp files
    mysql/lib/          # Plugins directory. Ruby code that extends Puppet here.
    mysql/templates/    # ERB and EPP Templates directory
    mysql/files/        # Static files directory
    mysql/spec/         # Puppet tests directory
    mysql/examples/     # Tests / Usage examples directory
    mysql/tasks         # Tasks (in any language) directory (from Puppet )
    mysql/plans         # Plans directory
    mysql/type          # Data types directory 

    mysql/Modulefile    # Module's metadata descriptor (old, deprecated)
    mysql/metadata.json # Module's metadata descriptor

This layout enables useful conventions over configurations.

# Modules paths conventions

Classes and defines can be autoloaded, that is found automatically by Puppet as long as the relevant module is in the $modulepath and defined in the correct manifests, as follows:

    include mysql
    # Main mysql class is placed in: $modulepath/mysql/manifests/init.pp

    include mysql::server
    # This class is defined in: $modulepath/mysql/manifests/server.pp

    mysql::conf { ...}
    # This define is defined in: $modulepath/mysql/manifests/conf.pp

    include mysql::server::ha
    # This class is defined in: $modulepath/mysql/manifests/server/ha.pp

Templates (`.erb` or `.epp`) are used in the relevant functions (`template()` or `epp()`) as follows

    content => template('mysql/my.cnf.erb'),
    # Erb template is in: $modulepath/mysql/templates/my.cnf.erb

    content => epp('mysql/my.cnf.epp'),
    # Epp template is in: $modulepath/mysql/templates/my.cnf.epp

Statically sourced files (files copied as is from master to clients) are referred as follows (note: `source` and `content` parameters in the file type are mutually exclusive):

    source => 'puppet:///modules/mysql/my.cnf'
    # Static file is in: $modulepath/mysql/files/my.cnf


# ERB templates

They are files with `.erb` extension typically passed to the `template()` function and used as content for ```file``` resources.

Inside these files ruby code can be interpolated inside the  ```<%``` and ```%>``` tags.

Example of an erb template:

    # Show facts values
    hostname = <%= @::fqdn %>

    # Show values of variables outside local scope, two methods:
    ntp_server = <%= scope.lookupvar('::ntp::server') %>
    ntp_server = <%= scope['::ntp::server'] %>

    # Iteration over an array
    <% @::dns_servers.each do |ns| %>
    nameserver <%= ns %>
    <% end %>

    # Conditional blocks of texts
    <% if scope.lookupvar('puppet::db') == "puppetdb" -%>
    storeconfigs_backend = puppetdb
    <% end -%>

Note the ending ```-%>```: when dash is present, no new line is introduced on the generated file.


# EPP templates

They are files with `.epp` extension typically passed to the `epp()` function and used as content for ```file``` resources. As second argument the epp function expects an hash of variables usable in the template.

Inside these files Puppet code can be interpolated inside the  ```<%``` and ```%>``` tags, the variables passed can be validated.

Example of an epp template, as used, for example, in `epp('template.epp',{dns_servers = ['1.1.1.1','8.8.8.8']})`:

    # Show facts values and top scope variables using the fully qualified path ($:: ...)
    hostname = <%= $::fqdn %>

    # Show values of variables outside local scope using the fully qualified path:
    ntp_server = <%= $::ntp::server') %>

    # Iteration over an array (here the local scope dns_servers must be passed as argument of the epp function)
    <% $dns_servers.each |$ns| { %>
    nameserver <%= $ns %>
    <% } %>

    # Conditional blocks of texts
    <% if $::puppet::db' == 'puppetdb' { -%>
    storeconfigs_backend = puppetdb
    <% } -%>

