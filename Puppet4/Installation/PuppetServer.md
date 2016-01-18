# Puppet Server

Is the new [server component](http://docs.puppetlabs.com/puppetserver/latest/index.html) to manage Puppet agents.

It's written in Clojure and runs inside a JVM.

By default it uses 2GB of RAM. It can be configured to only use 1 GB of RAM for testing purposes.

Slower startup times, better performances.

Works also with [Puppet 3 agents]()

The installation can also be done via puppet code:

    # /root/install_puppetserver.pp
    package { 'puppetserver':
      ensure => present,
    }
    service { 'puppetserver':
      ensure => running,
      enable => true,
    }

```
puppet apply /root/install_puppetserver.pp
```


