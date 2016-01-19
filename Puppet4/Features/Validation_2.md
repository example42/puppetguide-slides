# Tata Types validation

Another approach to check variables using data types is possible by using comparison rules:

    class my_example3 (
      $enable = true,
    ){
      if $enable =~ Boolean {
        ...
      } else {
        ...
      }
    }

