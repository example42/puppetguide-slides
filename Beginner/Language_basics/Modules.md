# Modules

  Self Contained and Distributable *recipes* contained in a directory with a predefined structure

  Used to manage an application, system's resources, a local site or more complex structures

  Modules must be placed in the Puppet Master's modulepath

    puppet config print modulepath
    /etc/puppet/modules:/usr/share/puppet/modules

  Puppet module tool to interface with Puppet Modules Forge

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

  GitHub, also, is full of Puppet modules


# Paths of a module

  Modules have a standard structure:

    mysql/            # Main module directory

    mysql/manifests/  # Manifests directory. Puppet code here.
    mysql/lib/        # Plugins directory. Ruby code that extends Puppet here.
    mysql/templates/  # ERB and EPP Templates directory
    mysql/files/      # Static files directory
    mysql/spec/       # Puppet-rspec directory
    mysql/tests/      # Tests / Usage examples directory

    mysql/Modulefile  # Module's metadata descriptor

  This layout enables useful conventions


# Modules paths conventions

  Classes and defines autoloading:

    include mysql
    # Main mysql class is placed in: $modulepath/mysql/manifests/init.pp

    include mysql::server
    # This class is defined in: $modulepath/mysql/manifests/server.pp

    mysql::conf { ...}
    # This define is defined in: $modulepath/mysql/manifests/conf.pp

    include mysql::server::ha
    # This class is defined in: $modulepath/mysql/manifests/server/ha.pp

  Provide files based on Erb Templates (Dynamic content)

    content => template('mysql/my.cnf.erb'),
    # Template is in: $modulepath/mysql/templates/my.cnf.erb

  Provide static files (Static content). Note we can't use content AND source for the same file.

    source => 'puppet:///modules/mysql/my.cnf'
    # File is in: $modulepath/mysql/files/my.cnf


# ERB templates

Files with .erb extension used typicall by in ```file``` resources.

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
