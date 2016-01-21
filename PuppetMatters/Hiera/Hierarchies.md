# Hierarchies

With the ```:hierarchy``` global setting we can define a string or an array of data sources which are checked in order, from top to bottom.

When the same key is present on different data sources by default is chosen the top one. We can override this setting with the ```:merge_behavior``` global configuration. Check [this page](http://docs.puppetlabs.com/hiera/1/lookup_types.html#deep-merging-in-hiera--120) for details.

In hierarchies we can interpolate variables with the %{} notation (variables interpolation is possible also in other parts of hiera.yaml and in the same data sources).

This is an example Hierarchy:

        ---
        :hierarchy:
          - "nodes/%{::clientcert}"
          - "roles/%{::role}"
          - "%{::osfamily}"
          - "%{::environment}"
          - common

Note that the referenced variables should be expressed with their fully qualified name. They are generally facts or Puppet's top scope variables (in the above example, **$::role** is not a standard fact, but is generally useful to have it (or a similar variable that identifies the kind of server) in our hierarchy).

If we have more backends, for each backend is evaluated the full hierarchy.

We can find some real world hierarchies samples in this [Puppet Users Group post](https://groups.google.com/forum/?hl=it#!topic/puppet-users/cCfimbolUio)

More information on hierarchies [here](http://docs.puppetlabs.com/hiera/1/hierarchy.html).
