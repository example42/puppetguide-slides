# Hiera Backends

One powerful feature of Hiera is that the actual key-value data can be retrieved from different backends.

With the ```:backends``` global configuration we define which backends to use, then, for each used backend we can specify backend specific settings.

### Build it backends:

**yaml** - Data is stored in yaml files (in the ```:datadir``` directory)

**json** - Data is stored in json files (in the ```:datadir``` directory)

**puppet** - Data is defined in Puppet (in the ```:datasouce``` class)

### Extra backends:
Many additional backends are available, the most interesting ones are:

[**gpg**](https://github.com/crayfishx/hiera-gpg) - Data is stored in GPG encripted yaml files

[**http**](https://github.com/crayfishx/hiera-http) - Data is retrieved from a REST service

[**mysql**](https://github.com/crayfishx/hiera-mysql) - Data is retrieved from a Mysql database

[**redis**](https://github.com/reliantsecurity/hiera-redis) - Data is retrieved from a Redis database

### Custom backends
It's relatively easy to write custom backends for Hiera. Here are some [development instructions](http://docs.puppetlabs.com/hiera/1/custom_backends.html)
