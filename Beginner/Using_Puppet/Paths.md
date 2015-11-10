
# Puppet paths

The paths of the most important locations are different on Puppet versions on Linux systems. Check the [Official specification](https://github.com/puppetlabs/puppet-specifications/blob/master/file_paths.md) for all the details.

Configuration directory (```$confdir```):

    /etc/puppet/            # Puppet 3 or earlier
    /etc/puppetlabs/puppet/ # Puppet 4 and PE

Log directory (```$logdir```):

    /var/log/puppet # Puppet 3 or earlier
    /var/log/puppetlabs/puppet # Puppet 4


Lib directory (```$libdir```) (contains Puppet operational data such as catalog, backup of files...):

    /var/lib/puppet # Puppet 3 or earlier
    /opt/puppetlabs/puppet/lib # Puppet 4

SSL directory (```$libdir```) (contains all the SSL certificates)

    $logdir/ssl  # Puppet 3 or earlier
    $confdir/ssl # Puppet 4

Manifest file (the first manifest parsed by the Master when compiling the catalog

    /etc/puppet/manifests/site.pp # Puppet 3 with config-file environments
    /etc/puppet/environments/$environment/manifests/site.pp # Puppet 3 with directory environments
    /etc/puppetlabs/code/environments/$environment/manifests/site.pp # Puppet 4

Modulepath (comma separated directories where modules are stored):

    /etc/puppet/modules:/usr/share/puppet/modules # Puppet 3
    /etc/puppet/environments/$environment/modules # Added modules dir in Puppet 3 when using **directory environments**

Code directory in Puppet 4:

    /etc/puppetlabs/code # $codedir
    /etc/puppetlabs/code/environments/$environment # $environmentpath

Inside the $environmentpath
    hieradata/ # Hiera files dir
    environment.conf *
        manifests *
        modules *
        hiera.yaml *                      # :hiera_config
    modules *                         # user modulepath    
