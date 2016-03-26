# Modules

Self Contained and Distributable *recipes* contained in a directory with a predefined structure

Used to manage an application, system's resources, a local site or more complex structures

Modules must be placed in the Puppet Master's modulepath

    @@@shell
    puppet config print modulepath
    /etc/puppet/modules:/usr/share/puppet/modules

Puppet module tool to interface with Puppet Modules Forge

  @@@shell
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
