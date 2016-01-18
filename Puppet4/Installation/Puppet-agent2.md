# Puppet agent

All required binaries can be found in ```/opt/puppetlabs/bin```

All other binaries can be found in ```/opt/puppetlabs/puppet/bin```

You either want to add the first path to your PATH environment variable or you create symlinks

    # /root/puppet_symlinks.pp
    $binaries = ['puppet', 'facter', 'hiera']
    $binaries.each |$binary| {
      file { "/usr/local/bin/${binary}":
        ensure => link,
        target => "/opt/puppetlabs/bin/${binary}",
      }
    }

```
/opt/puppetlabs/bin/puppet apply /root/puppet_symlinks.pp
```
