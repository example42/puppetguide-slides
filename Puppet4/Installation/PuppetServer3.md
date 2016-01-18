# Puppet Server

In case of low memory is it possible to reduce the Java Heap size.
Depending on the Operatingsystem this is done in ```/etc/default/puppetserver``` (Debian) or ```/etc/sysconfig/puppetserver``` (RedHat).
Best way to change the setting would be using puppetlabs-inifile module:

    cd root
    puppet module install puppetlabs-inifile --modulepath=.

Then create a proper inisubsetting resource type:

    # /root/puppetserver_lowmem.pp
    $cfgfile = $::osfamily ? {
      'Debian' => '/etc/default/puppetserver',
      'RedHat' => '/etc/sysconfig/puppetserver',
      default  => undef,
    }
    ini_subsetting { 'puppetserver lowmem':
      ensure            => present,
      section           => '',
      key_val_separator => '=',
      path              => $cfgfile,
      setting           => 'JAVA_ARGS',
      subsetting        => '-Xmx',
      value             => '1g',
      notify            => Service['puppetserver'],
    }
    service { 'puppetserver':
      ensure => running,
      enable => true,
    }

```
puppet apply /root/puppetserver_lowmem.pp --modulepath=.
```


