# Hiera configuration: hiera.yaml

Hiera's configuration file is in yaml format and is called **hiera.yaml** here we define the hierarchy we want to use and the backends where data is placed, with backend specific settings.

Hiera's configuration file path is different according to how it's invoked:

### From the Command Line and Ruby code

Default path: ```/etc/hiera.yaml```

### From Puppet

Default path for Puppet OpenSource: ```/etc/puppet/hiera.yaml```

Default path for Puppet Enterprise: ```/etc/puppetlabs/puppet/hiera.yaml```

It's good practice the symlink these alternative configuration files in order to avoid inconsistencies when using Hiera from the shell line or within Puppet manifests:

    ln -s /etc/hiera.yaml /etc/puppet/hiera.yaml

## Default configuration
By default Hiera does not provide a configuration file. The default settings are equivalent to this:

    ---
    :backends: yaml
    :yaml:
      :datadir: /var/lib/hiera
    :hierarchy: common
    :logger: console
