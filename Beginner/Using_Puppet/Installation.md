# Puppet 3 Installation

Puppet version 3.x or earlier can be found by default in most distributions.

On Debian and derivates, you can install it with:

    apt-get install puppet       # On clients (nodes)
    apt-get install puppetmaster # On server (master)

On RedHat and derivates you need to add the EPEL repository or RHN Extra channel:

    yum install puppet        # On clients (nodes)
    yum install puppet-server # On server (master)

It generally recommended to use [Puppet Labs repositories](http://docs.puppetlabs.com/guides/puppetlabs_package_repositories.html) for the latest updates.

Check the [Installation Instructions](http://docs.puppetlabs.com/guides/installation.html) for different OS.

# Puppet 4 installation

Puppet version 4 can be installed using [Puppet Labs Software Collections](https://puppetlabs.com/blog/welcome-puppet-collections), once added the relevant repositories for your distro you can install it with:

    [apt-get|yum] install puppet-agent   # On clients (nodes)
    [apt-get|yum] install puppet-server  # On server (master)

# Puppet Enterprise installation
