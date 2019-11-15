
# Paths of a module

  Modules have a standard structure:

    mysql/            # Main module directory

    mysql/manifests/  # Manifests directory. Puppet code here. Required.
    mysql/lib/        # Plugins directory. Ruby code here
    mysql/templates/  # ERB Templates directory
    mysql/files/      # Static files directory
    mysql/spec/       # Puppet-rspec test directory
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
