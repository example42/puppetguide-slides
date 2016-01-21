
# Using Hiera in Puppet
The data stored in Hiera can be retrieved by the PuppetMaster while compiling the catalog using the hiera() function.

In our manifests we can have something like this:

        $my_dns_servers = hiera("dns_servers")

Which assigns to the variable ***$my_dns_servers*** (can have any name) the top value retrieved by Hiera for the key ***dns_servers***

We may prefer, in some cases, to retrieve all the values retrieved in the hierarchy's data sources of a given key and not the first use, use hiera_array() for that.

        $my_dns_servers = hiera_array("dns_servers")

If we expect an hash as value for a given key we can use the hiera() function to retrieve the top value found or hiera_hash to merge all the found values in a single hash:

        $openssh_settings = hiera_hash("openssh_settings")

### Extra parameters
All these hiera functions may receive additional parameters:

Second argument: **default** value if no one is found

Third argument: **override** with a custom data source added at the top of the configured hierarchy

        $my_dns_servers = hiera("dns_servers","8.8.8.8","$country")
