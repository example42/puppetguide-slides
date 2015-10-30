# Introduction to Hiera

Hiera is the most used solution to manage the data we need to configure our systems according to the logic we need.

It allows to separate data from code, allowing us to avoid to place inside our Puppet manifests information which is strictly related to our infrastructure and its settings.

It's shipped together with Puppet from version 3 and it's strictly integrated: for each class parameter Puppet does an automatic lookup on a corresponding Hiera value.

Hiera can use different backends to store it's data. The default one is Yaml (all data is placed in simple Yaml files). Other backend are Json, Mysql, Redis and so on.

Data is looked on Hiera following a hierarchy based on Puppet variables, in this way we can attribute to an Hiera Key (for example ```ntp::server```) different values according to different conditions (for example the role, the environment or the location of a server).

Inside Puppet code with can use the ```hiera()``` function to look for a given Hiera key. For example the following code assign to the variable ```$server``` the value of the Hiera key called ```ntp_server```. An optional parameter can be added to set the default value (here ```ntp.pool.org```) to return if the key is not found on Hiera:

    $server = hiera('ntp_server','ntp.pool.org')

Since Puppet 3 Puppet does an automatic lookup on Hiera for each parameter of a class. In the following example the parameter ```server``` (whose value can be referred, inside the same class, using the ```$server``` variable and, inside any other class with its *fully qualified name*: ```$::ntp::server```) can be changed by setting, on Hiera a value for the key called ```ntp::server```:

    class ntp (
      server = 'ntp.pool.org',
    ) { }



# Hiera configuration

Hiera's configuration file for Puppet is ```/etc/puppet/hiera.yaml``` (On Puppet 4 ```/etc/puppet/puppetlabs/hiera.yaml```). It's a Yaml file which looks like this:

    ---
      :backends:
        - yaml

      :hierarchy:
         - "%{::environment}/nodes/%{::fqdn}"
         - "%{::environment}/roles/%{::role}"
         - "%{::environment}/zones/%{::zone}"
         - "%{::environment}/common"
       :yaml:
         :datadir: /etc/puppet/hieradata

In the above sample it's configured the **backend(s)** to use, the **hierarchy** based on Puppet variables (inside ```%{}```) and the configuration specific to the used backend (here is set the **datadir** when Yaml files containing Hiera keys are placed, named acconding to the defined hierarchy).
