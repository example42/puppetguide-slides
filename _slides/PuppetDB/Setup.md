
# PuppetDB installation
For a complete overview of the installation process check the official documentation and choose between installatio from [puppetdb module](http://docs.puppetlabs.com/puppetdb/latest/install_via_module.html) or from [packages](http://docs.puppetlabs.com/puppetdb/latest/install_from_packages.html).

PuppetDB can persist data either on an embedded HSQLDB database or on PostgreSQL.
The latter is definitively recommended on production environment where there are a few dozens of servers or more.

The configuration files are:

```/etc/sysconfig/puppetdb``` (```/etc/default/puppetdb``` on Debian) is the init script configuration file, here we can set JAVA settings like JAVA_ARGS or JAVA_BIN


```/etc/puppetdb/conf.d/``` is the configuration directory, here we may have different .ini files where to configure **[global]** settings, **[database]** backends, **[command-processing]** options, **[jetty]** parameters for HTTP connections and **[repl]** settings for remote runtime configurations (used for development/debugging).


```/etc/puppetdb/log4j.properties``` is the logging config file based on Log4j.


```/etc/puppet/puppetdb.conf``` is the configuration file for **Puppet** with the settings to be used by the PuppetDB terminus
