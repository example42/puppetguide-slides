
# Using Hiera in Puppet
The data stored in Hiera can be retrieved by the PuppetMaster while compiling the catalog using the legacy (now deprecated) `hiera()` function or the more modern `lookup()` one.

In our manifests we can have something like this:

    @@@ puppet
    # Deprecated Hiera function for direct lookup
    $my_dns_servers = hiera('dns_servers')

    # Current lookup function alternative
    $my_dns_servers = lookup('dns_servers')

Both of them assign to the variable ***$my_dns_servers*** (can have any name) the first value retrieved by Hiera for the key ***dns_servers***

We may prefer, in some cases, to retrieve all the values retrieved in the hierarchy's data sources of a given key and not the first use. If the expected data is an array we can use hiera_array() for that (deprecated) or specify the unique merge method in the lookup() function.

    @@@ puppet
    # Deprecated Hiera function for merging arrays lookup
    $my_dns_servers = hiera_array('dns_servers')

    # Current lookup function alternative with unique merge method
    $my_dns_servers =  lookup('ntp::servers', {merge => unique})

If we expect an hash as value for a given key we can use the hiera() legacy function or lookup() with the default "first" lookup method to retrieve the first value found in the hierarchies, but, if we want to merge the hash values found in all the hierarchy levels in a single hash  we can use the legacy hiera_hash() function or the deep merge method in lookup():

    @@@ puppet
    # Deprecated Hiera function for merging hashes lookup
    $openssh_settings = hiera_hash('openssh_settings')

    # Current lookup function alternative with merge methods hash or deep
    $openssh_settings = lookup('openssh_settings', {merge => hash}) # Normal hash merge
    $openssh_settings = lookup('openssh_settings', {merge => deep}) # Deep hash merge

The difference between hash and deep merge methods is that, when exist the same subkeys in hash looked up via Hiera, with deep merge the subkeys values are merged recursively, with normal hash merge the first one is the returned value.

Finally it's possible to include classes via Hiera, this is the so called Hiera driven classification.

In these examples, the key looked for ('classes') contain an array of the names of the classes to include (merged across the hierarchies):

    @@@ puppet
    # Deprecated Hiera_ function for including classes
    hiera_include('classes')
    
    # Alternative in modern Puppet
    lookup('classes', {merge => unique}).include
