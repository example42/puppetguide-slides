# Data Types

Puppet 4 introduces a new powerful data types system.

Each kind of data can be expressed by a data type.

This is most usefule when declaring parameterized classes where data is fetched from a remote source.

Prior Puppet 4 it was recommended to make use of the ```validate_*``` or ```is_*``` functions from stdlib.

e.g.

    class my_ntp (
      $ntp_server,
      $secure = false,
    ) {
      validate_array($ntp_server)
      validate_bool($secure)
    }

This lead to very complex code and the data validation distracted users from the real code.

