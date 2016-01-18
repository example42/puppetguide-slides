# Data Types

Puppet 4 knows about all common data types:

- Numeric, Interger, Float
- Boolean
- String, Regexp, Pattern
- Array, Hash
- Optional, Variant, Enum

Data types can be specified by writing the Data type in front of the parameter of parameterized classes:

e.g.

    class my_ntp (
      Array[String] $ntp_servers,
      Boolean       $secure,
    ) {
    }

One can now omit the ```validate_*``` and ```is_*``` functions.

Please note: older Puppet versions will not understand this code.
With Puppet 3.5 or later the future parser needs to get activated in puppet.conf file (```parser = future```).

