# Masterless setup

A masterless setup doesn't need a Puppet Master.

Puppet manifests are deployed directly on nodes and applied locally, we need to specify the manifest to apply, the path where to find modules and eventually the location of Hiera configuration file.

    puppet apply --modulepath /puppetcode/modules/ --hiera_config /puppetcode/hiera.yaml /puppetcode/manifests/file.pp

To see the default values of these configuration options type:

    puppet config print hiera_config modulepath

Such a setup involves pros, cons and new infrastructural challenges:

  - (+) No need of a Puppet infrastructure: just the puppet package on the node
  - (+) There's not an external point of failure and a bottleneck on the Puppet Master (which still can scale)
  - (+) We can trigger multiple parallel Puppet runs
  - (+) Easier control of what version of our Puppet code is deployed and applied to each node 
  - (-) All the nodes have to store locally the Puppet code: we need a sane way to manage secrets
  - (-) StoreConfigs usage require access to Puppet DB from every node
  - (-) There aren't simple and ready solutions for centralized reporting and visualization of Puppet activity
  - (=) We need to define a fitting deployment workflow on all the nodes. Hints: [Rump](https://github.com/railsmachine/rump) - [supply_drop](https://github.com/pitluga/supply_drop)
