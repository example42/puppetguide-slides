# Puppet Essentials - Overview

- Puppet installation
- Puppet commands
- Files and paths
- Puppet versions



# Puppet Installation

Puppet version 3.x or earlier can be found by default in most distributions.

On Debian and derivates, you can install it with:

    apt-get install puppet       # On clients (nodes)
    apt-get install puppetmaster # On server (master)

On RedHat and derivates you need to add the EPEL repository or RHN Extra channel:

    yum install puppet        # On clients (nodes)
    yum install puppet-server # On server (master)

It generally recommended to use [Puppet Labs repositories](http://docs.puppetlabs.com/guides/puppetlabs_package_repositories.html) for the latest updates.

Check the [Installation Instructions](http://docs.puppetlabs.com/guides/installation.html) for different OS.

Puppet version 4 can be installed using [Puppet Labs Software Collections](https://puppetlabs.com/blog/welcome-puppet-collections), once added the relevant repositories for your distro you can install it with:

    [apt-get|yum] install puppet-agent   # On clients (nodes)
    [apt-get|yum] install puppet-server  # On server (master)


# Using the Puppet command



# Masterless - puppet apply

Our Puppet code (written in manifests) is applied directly on the target system.

No need of a complete client-server infrastructure.

Have to distribute manifests and modules to the managed nodes.

Command used: ```puppet apply``` (generally as **root**)

# Master / Client - puppet agent

We have clients, our managed nodes, where Puppet agent is installed.

And we have one or more Masters where Puppet server runs as a service

Client/Server communication is via https (**port 8140**)

Clients certificates have to be accepted (**signed**) on the Master

Command used on the client: ```puppet agent```  (generally as **root**)

Command used on the server: ```puppet master```  (generally as **puppet**)

# Puppet Versions

From version 2 Puppet follows [Semantic Versioning](http://semver.org/) standards to manage versioning, with a pattern like: MAJOR.MINOR.PATCH

This implies that MAYOR versions might not be backwards compatible, MINOR versions may introduce new features keeping compatibility and PATCHes are for backwards compatible bug fixes.

This is the history of the main Puppet versions and some relevant changes
Check also [Puppet Language History](http://docs.puppetlabs.com/guides/language_history.html) for a more complete review:

- 0.9.x  - First public beta
- 0.10.x - 0.21.x - Various "early" versions
- 0.22.x - 0.25.x - Improvements and OS wider support
- 2.6.x  - Many changes. Parametrized classes
- 2.7.x  - Windows support
- 3.0.x  - Many changes. Disabled dynamic variables scope. Data bindings
- 3.2.x  - Future parser (experimental, will be default in Puppet 4)
- 4.x.x  - Released in early 2015. New parser, new type system and lot of changes, various language cleanups and some backwards incompatibilities


# Migrating to Puppet 4

With Puppet 4 many things have changed:

- New Parser, new Type system, a lot of code tuning
- Puppet agent and its components (facter, mcollective and the relevant stack) is shipped with All In One package (AIO) to retrieve from PuppetLabs site
- All directory paths are changed
- The Master function is done via **Puppet Server** (a new dedicated clojure application)

Migration from previous versions to Puppet 4 probably need some code refactoring.

Most of current modules are Puppet 4 ready but don't fully use its power (they keep 3.x compatibility).

Some useful links about Puppet 4:

- Puppet 4 [release notes](https://docs.puppetlabs.com/puppet/4.0/reference/release_notes.html)
- Online reference for [agent](https://docs.puppetlabs.com/puppet/4.0/reference/upgrade_agent.html) upgrade
- Online reference for [server](https://docs.puppetlabs.com/puppet/4.0/reference/upgrade_server.html) upgrade
- Article on how to [prepare our code](http://www.camptocamp.com/en/actualite/getting-code-ready-puppet-4/) for Puppet 4.
