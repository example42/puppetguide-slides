# Masterless setup

  Puppet manifests are deployed directly on nodes and applied locally:

    puppet apply --modulepath /modules/ /manifests/file.pp

  More fine grained control on what goes in production for what nodes

  Ability to trigger multiple truly parallel Puppet runs

  No single point of failure, no Master performance issues

  Need to define a fitting deployment workflow. Hints: [Rump](https://github.com/railsmachine/rump) - [supply_drop](https://github.com/pitluga/supply_drop)

  With Puppet > 2.6 we can use file sources urls like:

    puppet:///modules/example42/apache/vhost.conf

    # they point to
    $modulepath/example42/apache/vhost.conf

  StoreConfigs usage require access to Puppet DB from every node
