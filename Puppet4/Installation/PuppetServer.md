# Puppet Server

Is the new [server component](http://docs.puppetlabs.com/puppetserver/latest/index.html) to manage Puppet agents.

It's written in Clojure and runs inside a JVM.

By default it uses 2GB of RAM. It can be configured to only use 1 GB of RAM for testing purposes.

Slower startup times, better performances.

Works also with [Puppet 3 agents]()

The installation can also be done via puppet code:

```
# /root/install_puppetserver.pp
package { 'puppetserver':
  ensure => present,
}
service { 'puppetserver':
  ensure => running,
  enable => true,
}
```

```
puppet apply /root/install_puppetserver.pp
```

~~~PAGEBREAK~~~

The big difference is within Ruby gems. On the old Puppet master one could make use of any Ruby gem.
Now the Puppet server is running on top of JRuby.
JRuby does not support gems with native extensions (extensions which get compiled during installation).

Please carefully review the [list](https://github.com/jruby/jruby/wiki/C-Extension-Alternatives) of gems with JRuby support.

Gems which are required for functions or report processors (not providers or facter extensions) have to be installed within the puppet server JRuby installation.
This can be done be running the ```puppetserver gem``` command:

    puppetserver gem list
    sudo puppetserver gem install rake --no-ri --no-rdoc


In case of low memory is it possible to reduce the Java Heap size.
Depending on the Operatingsystem this is done in ```/etc/default/puppetserver``` (Debian) or ```/etc/sysconfig/puppetserver``` (RedHat).
Best way to change the setting would be using puppetlabs-inifile module:

```
cd root
puppet module install puppetlabs-inifile --modulepath=.
```

Then create a proper inisubsetting resource type:
```
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

```
puppet apply /root/puppetserver_lowmem.pp --modulepath=.
```


