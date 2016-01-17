# Puppet agent

The new AIO (All In One) package that PuppetLabs uses to distribute Puppet 4 clients, and its components (Facter, Hiera, MCollective)

It has it's [own versioning](http://docs.puppetlabs.com/puppet/4.3/reference/about_agent.html).

First the repositories need to be added.
Please take care to only use the PC1 repository!

The [installation](https://docs.puppetlabs.com/puppet/4.3/reference/install_linux.html#install-a-release-package-to-enable-puppet-labs-package-repositories) of the repository meta package only installs the GPG key and the according repo snippet.

Afterwards you need to run either

```
yum makecache
```

or

```
apt-get update
```

Now the puppet agent package can be installed:

```
yum install puppet-agent
```

```
apt-get install puppet-agent
```

All required binaries can be found in ```/opt/puppetlabs/bin```.
All other binaries can be found in ```/opt/puppetlabs/puppet/bin```

You either watn to add the first path to your PATH environment variable or you create symlinks:

```
# /root/puppet_symlinks.pp
$binaries = ['puppet', 'facter', 'hiera']
$binaries.each |$binary| {
  file { "/usr/local/bin/${binary}":
    ensure => link,
    target => "/opt/puppetlabs/bin/${binary}",
  }
}
```

```
/opt/puppetlabs/bin/puppet apply /root/puppet_symlinks.pp
```

