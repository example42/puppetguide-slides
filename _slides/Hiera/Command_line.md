# Using hiera from the command line

Hiera can be invoken via the command line to interrogate the given key's value:

    @@@ shell
    hiera dns_servers

This will return the default value as no node's specific information is provided. More useful is to provide the whole facts' yaml of a node, so that the returned value can be based on the dynamic values of the hierarchy.
On the Pupppet Masters the facts of all the managed clients are collected in $vardir/yaml/facts so this is the best place to see how Hiera evaluates keys for different clients:

    @@@ shell
    hiera dns_servers --yaml /var/lib/puppet/yaml/facts/<node>.yaml

We can also pass variables useful to test the hierarchy, directly from the command line:

    @@@ shell
    hiera ntp_servers operatingsystem=Centos
    hiera ntp_servers operatingsystem=Centos hostname=jenkins

To have a deeper insight of Hiera operations use the debug (-d) option:

    @@@ shell
    hiera dns_servers -d

To make an hiera array lookup (equivalent to hiera_array()):

    @@@ shell
    hiera dns_servers -a

To make an hiera hash lookup (equivalent to hiera_hash()):

    @@@ shell
    hiera openssh::settings -h
