# Introduction to Hiera

Hiera is the **key/value lookup tool** of reference where to store Puppet user data.

It provides an highly customizable way to lookup for parameters values based on a custom hierarchy using many different backends for data storage.

It provides a command line tool ```hiera``` that we can use to interrogate direclty the Hiera data and functions to be used inside Puppet manifests: ```hiera()``` , ```hiera_array()``` , ```hiera_hash()``` , ```hiera_include()```

Hiera is installed by default with Puppet version 3 and is available as separated download on earlier version ([Installation instructions](http://docs.puppetlabs.com/hiera/1/installing.html)).

We need Hiera only on the PuppetMaster (or on any node, if we have a masterless setup).

Currently version 1 is available, here is its [official documentation](http://docs.puppetlabs.com/hiera/1/).
