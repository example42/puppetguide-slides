# Information available on the Puppet Master

To see the facts of the Puppet Master's clients:

    sudo cat /var/lib/puppet/yaml/facts/<node_certname>.yaml # Puppet 3
    sudo cat /opt/puppetlabs/puppet/cache/yaml/facts.d/<node_certname>.yaml # Puppet 4

To check the value of an Hiera key for a node with given variables:

    hiera <key_name> -c /etc/puppet/hiera.yaml <param=value> <param=value> # Puppet 3
    hiera <key_name> -c /etc/puppetlabs/code/hiera.yaml <param=value> <param=value> # Puppet 4


## Information available on the CA server

List of all the signed and requested certificates

    sudo puppet cert -la

On the CA server, by default the same Puppet Master, you can manage all the certificates with the ```puppet cert``` command.


## Information available on the PuppetDB server

Query facts about a node

    sudo puppet node find <node_certname> | json_pp

To purge a node data from PuppetDB (useful when you have duplicated resources in a node that collects exported resources). Use if you know what you are doing:

    sudo puppet node deactivate <node_certname>

You can use the ```query``` action provided by the [puppetdbquery module](https://github.com/dalen/puppet-puppetdbquery). For example to list all the nodes, stored on PuppetDB than match a given fact:

    sudo puppet query nodes osfamily=Debian

To list specific facts of nodes matching your query:

    sudo puppet query facts osfamily=Debian --facts 'ipaddress,uptime'

Check the puppetdbquery [query format syntax](https://github.com/dalen/puppet-puppetdbquery#query-syntax) to learn more about the syntax of your queries.
