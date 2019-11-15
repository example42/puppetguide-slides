# Puppet configuration: puppet.conf

It's Puppet main configuration file.

On open source Puppet 3 is generally in:

    /etc/puppet/puppet.conf

On Puppet Enterprise and Puppet 4 is in:

    /etc/puppetlabs/puppet/puppet.conf

On Windows is in:

    C:\ProgramData\PuppetLabs\puppet\etc

When running as a normal user can be placed in the home directory:

    /home/<user>/.puppet/puppet.conf

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


Important options under **[main]** section:

    vardir = /var/lib/puppet # Path where Puppet stores dynamic data.
    ssldir = $vardir/ssl # Path where SSL certifications are stored.

Important options Under **[agent]** section:

    server = puppet.example42.com # Host name of the PuppetMaster. (Default: puppet)
    certname = web01.example42.com # Certificate name of the client. (Default is its fqdn)
    runinterval = 60 # Number of minutes between Puppet runs, when running as service. (Default: 30)
    report = true # If to send Puppet runs' reports to the **report_server**. (Default: true)

Important options under **[master]** section:

    autosign = /etc/puppet/autosign.conf # If new clients certificates are automatically signed. (Default: false)
    reports = puppetdb # How to manage clients' reports (Default: store)
    storeconfigs = true # If to enable store configs to support exported resources. (Default: false)

Full [configuration reference](http://docs.puppetlabs.com/references/latest/configuration.html)  on the official site.
