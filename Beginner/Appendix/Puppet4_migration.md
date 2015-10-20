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
