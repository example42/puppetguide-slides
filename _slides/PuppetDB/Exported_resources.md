# Exported resources

When we need to provide to an host informations about resources present in another host, we need **exported resources**: resources declared in the catalog of a node (based on its facts and variables) but applied (collected) on another node.

Resources are declared with the special @@ notation which marks them as exported so that they are not applied to the node where they are declared:

    @@host { $::fqdn:
      ip  => $::ipaddress,
    }

    @@concat::fragment { "balance-fe-${::hostname}",
      target  => '/etc/haproxy/haproxy.cfg',
      content => "server ${::hostname} ${::ipaddress} maxconn 5000"
      tag     => "balance-fe",
    }

Once a catalog containing exported resources has been applied on a node and stored by the PuppetMaster (typically on PuppetDB), the exported resources can be collected with the spaceshift syntax (where is possible to specify search queries):

    Host << || >>
    Concat::Fragment <<| tag == "balance-fe" |>>
    Sshkey <<| |>>
    Nagios_service <<||>>

# Exported resources - Configuration

In order to use exported resources we need to enable on the Puppet Master the **storeconfigs** option and specify the backend to use.
We can do this configuring a PuppetMaster to use PuppetDB:

    storeconfigs = true
    storeconfigs_backend = puppetdb

In earlier Puppet versions storeconfigs is based on ActiveRecord, which is considerable slower.
