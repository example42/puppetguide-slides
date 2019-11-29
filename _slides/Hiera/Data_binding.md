# Puppet data bindings
Starting from Puppet version 3 Hiera is shipped directly with Puppet and an automatic hiera lookup is done for each class' parameter using the key **$class::$argument**: this functionality is called data bindings or automatic parameter lookup.

For example in a class definition like:

    @@@puppet
    class openssh (
      template = undef,
    ) { . . . }

Puppet 3 automatically looks for the Hiera key `openssh::template` if no value is explicitly set when declaring the class.

To emulate a similar behaviour on pre Puppet 3 we should write something like:

    @@@puppet
    class openssh (
      template = hiera("openssh::template"),
    ) { . . . }

If a default value is set for an argument, that value is used only when user has not explicitly declared avalue for that argument and Hiera automatic lookup for that argument doesn't return any value.

In modern Puppet setups data bindings is widely used to configure the classes included (without parameters declaration) via any classification method.