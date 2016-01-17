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

The big difference is within Ruby gems. On the old Puppet master one could make use of any Ruby gem.
Now the Puppet server is running on top of JRuby.
JRuby does not support gems with native extensions (extensions which get compiled during installation).

Please carefully review the [list](https://github.com/jruby/jruby/wiki/C-Extension-Alternatives) of gems with JRuby support.

Gems which are required for functions or report processors (not providers or facter extensions) have to be installed within the puppet server JRuby installation.
THis can be done be running the ```puppetserver gem``` command:

    puppetserver gem list
    sudo puppetserver gem install rake --no-ri --no-rdoc


