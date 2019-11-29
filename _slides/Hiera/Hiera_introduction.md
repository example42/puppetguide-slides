# Introduction to Hiera

Hiera is the most used solution to manage the data we need to configure our systems according to the logic we need.

It allows to separate data from code, allowing us to avoid to place inside our Puppet manifests information which is strictly related to our infrastructure and its settings.

Hiera has been integrated in starting from Puppet 3: for each class parameter Puppet does an automatic lookup on a corresponding Hiera value.

Since Puppet 4.9 a totally new version of Hiera (5) has been introduced, which introduces the possibility to use Hiera data directly in modules.

Hiera can use different backends to store it's data. The default one is Yaml (all data is placed in simple Yaml files). Other backend are Json, Mysql, Redis and so on.

Data is looked on Hiera following a hierarchy based on Puppet variables, in this way we can attribute to an Hiera Key (for example ```ntp::server```) different values according to different conditions (for example the role, the environment or the location of a server).

Inside Puppet code with can use the ```hiera()``` function (obsoleted by the ```lookup()``` function from Puppet 4.9) to look for a given Hiera key. For example the following code assign to the variable ```$server``` the value of the Hiera key called ```ntp_server```. An optional parameter can be added to set the default value (here ```ntp.pool.org```) to return if the key is not found on Hiera:

    $server = hiera('ntp_server','ntp.pool.org')

On modern Puppet versions this is equivalent to:

    $server = lookup('ntp_server',String,'first','ntp.pool.org')


Since Puppet 3 Puppet does an automatic lookup on Hiera for each parameter of a class. In the following example the parameter ```server``` (whose value can be referred, inside the same class, using the ```$server``` variable and, inside any other class with its *fully qualified name*: ```$::ntp::server```) can be changed by setting, on Hiera a value for the key called ```ntp::server```:

    class ntp (
      server = 'ntp.pool.org',
    ) { }



# Hiera configuration (old, pre Hiera 5)

Hiera 's configuration file for Puppet is ```/etc/puppet/hiera.yaml``` (On Puppet 4 ```/etc/puppetlabs/puppet/hiera.yaml```). It's a Yaml file which looks like this:

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

# Hiera configuration (new, starting from Hiera 5 - Puppet 4.9)

Starting from Hiera version 5 (available from Puppet version 4.9) hiera.yaml configuration file can be present in [3 different layers](https://puppet.com/docs/puppet/5.5/hiera_intro.html#ariaid-title3):

- Global layer: ```/etc/puppetlabs/puppet/hiera.yaml```. Equivalent to the single hiera.yaml in older versions.
- Environment layer: ```/etc/puppetlabs/code/environments/<environment>/hiera.yaml```. Inside each Puppet environment directory
- Module layer ```hiera.yaml```inside each module.

The hierarchies defined in each of these files are traversed in the same order: first all the ones in the global layer, then the ones in the environment layer and then the ones in module layer.

This means that a common.yaml defined in ```/etc/puppetlabs/puppet/hiera.yaml``` would override any more specific, variable dependent, hierarchy level in environment or module layers.

For this reason when using Hiera 5 layes are geenrally used as follows:

- Global layer is disabled (empty or missing hiera.yaml), used to set to global overrides, which "win" over everything, or used for special backends (like, as default on PE, the PE console)

- Environment layer is used for the most common data, where infrastructure related settings are placed

- Module layer is used generally by module authors, for OS related settings.

The format of hiera.yaml is slightly different, a sample one might look as follows:

    version: 5
    hierarchy:
      - name: "Hierarchy"
        paths:
        - "nodes/%{::fqdn}.yaml"
        - "roles/%{::role}.yaml"
        - "zones/%{::zone}.yaml"
        - "common.yaml"
    defaults:
      data_hash: yaml_data
      datadir: hieradata

If the above were an environment hiera.yaml, the data directory would be relative to the environment: ```/etc/puppetlabs/code/environments/<environment>/hieradata/```.