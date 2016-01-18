# Data Types

As you have seen from last example, data types can optionally make use of a further description.

e.g. limiting Integers:

    class my_ssh(
      Integer[22-1024] $port,
    ){
      ...
    }

e.g. specifying the data types of array elements

    class my_users (
      Hash[String, Hash] $user,
    ) {
      ...
    }

e.g. limiting possibilities of variable content

    class my_apache (
      Enum[true, 'true', 'yes', false, 'false', 'no'] $enable_at_boot,
    ) {
    }

e.g. an optional parameter, but when set it should be String

    class my_motd (
      Optional[String] $copyright = undef,
    ) {
    }

