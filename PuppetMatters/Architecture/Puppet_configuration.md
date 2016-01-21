
# Puppet configuration: puppet.conf

It's Puppet main configuration file.
On opensource Puppet is generally in:

    /etc/puppet/puppet.conf

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


# Main configuration options

To view all or a specific configuration setting:

    puppet config print all
    puppet config print modulepath

### Important options under **[main]** section:

  **vardir**: Path where Puppet stores dynamic data.

  **ssldir**: Path where SSL certifications are stored.

### Under **[agent]** section:

  **server**: Host name of the PuppetMaster. (Default: puppet)

  **certname**: Certificate name used by the client. (Default is its fqdn)

  **runinterval**: Number of minutes between Puppet runs, when running as service. (Default: 30)

  **report**: If to send Puppet runs' reports to the **report_server. (Default: true)

### Under **[master]** section:

  **autosign**: If new clients certificates are automatically signed. (Default: false)

  **reports**: How to manage clients' reports (Default: store)

  **storeconfigs**: If to enable store configs to support exported resources. (Default: false)

Full [configuration reference](http://docs.puppetlabs.com/references/latest/configuration.html)  on the official site.
