
# Puppet configuration: puppet.conf

It's Puppet main configuration file.

On Open Source Puppet <= 3 is generally in:

    /etc/puppet/puppet.conf

On Puppet 4 is in:

    /etc/puppet/puppetlabs/puppet.conf

On Puppet Enterprise:

    /etc/puppetlabs/puppet/puppet.conf

When running as a normal user can be placed in the home directory:

    /home/user/.puppet/puppet.conf

Configurations are divided in [stanzas] for different Puppet sub commands

Common for all commands: **[main]**

For puppet agent (client): **[agent]** (Was [puppetd] in Puppet pre 2.6)

For puppet apply (client): **[user]** (Was [puppet])

For puppet master (server): **[master]** (Was [puppetmasterd] and [puppetca])

Hash sign (#) can be used for comments.

To view all or a specific configuration setting:

    puppet config print all
    puppet config print modulepath


### Options worth attentions

Here are some options (and the relevant [stanza]) worth noting:

  - [main] **vardir**: Path where Puppet stores dynamic data.
  - [main] **ssldir**: Path where SSL certifications are stored.
  - [agent] **server**: Host name of the PuppetMaster. (Default: puppet)
  - [agent] **certname**: Certificate name used by the client. (Default is its fqdn)
  - [agent] **runinterval**: Number of minutes between Puppet runs, when running as service. (Default: 30)
  - [agent] **report**: If to send Puppet runs' reports to the **report_server**. (Default: true)
  - [master] **autosign**: If new clients certificates are automatically signed. (Default: false)
  - [master] **reports**: How to manage clients' reports (Default: store)
  - [master] **storeconfigs**: If to enable store configs to support exported resources. (Default: false)

For details check the full [configuration reference](http://docs.puppetlabs.com/references/latest/configuration.html)  on the official site.
