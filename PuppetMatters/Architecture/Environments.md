# Environments
Puppet environments allow isolation of Puppet code and data: for each environment we can have different paths manifest files, Hiera data and modules.

Puppet's environments DO NOT necessarily have to match the operational environments of our servers.

Environments mamanagement has changed from Puppet 3.6 onwards:

Earlier versions were based on so-called **Config file Environments** where each environment had to be defined in **puppet.conf**.

From 3.6 **directory environments** have been introduced and the older approach has been deprecated.

On Puppet 4.x only directory environments are supported.

# [Config file Environments](https://docs.puppetlabs.com/puppet/latest/reference/environments_classic.html)

The "old" config file environments are defined inside ```puppet.conf``` with a syntax like:

     [test]
       modulepath = $confdir/environments/test/modules:$condfir/modules
       manifest = $confdir/environments/test/manifests

For the default **production** environment there were the config parameters, now deprecated, ```manifest``` and ```modulepath``` in the ```[main]``` section.

# [Directory Environments](https://docs.puppetlabs.com/puppet/latest/reference/environments_configuring.html)

Directory Environments are configured in ```puppet.conf``` as follows:

    [main]
    environmentpath = $configdir/

Then inside the ```/etc/puppet/environments/$environment/``` directory we have:

    modules/   # Directory containing modules
    manifests/ # Directory containing site.pp
    environment.conf # Conf file for the environment
