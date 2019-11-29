# Resource Metaparameters

Metaparameters are parameters available to any resource type, they can be used for different purposes:

- Manage dependencies (**before**, **require**, **subscribe**, **notify**, **stage**)

- Manage resources' application policies (**audit**, **noop**, **schedule**, **loglevel**)

- Add information to a resource (**alias**, **tag**)

[Official documentation on Metaparameters](http://docs.puppetlabs.com/puppet/latest/reference/metaparameter.html)

The metaparameters that manage dependencies are widely used to apply the resources in a catalog following the expected order.