# Data Types validation

When specifiying data types on parameters, type validation is done automatically.

Variables, which are not parameters, but where data validation is required need to do the data validation in Puppet DSL code:

    class my_example {
      case $::my_dc_location {
        String: { ... }
        Array: { ... }
        Integer: { ... }
        Default: { ... }
      }
    }

In the given example the Data Type of the fact ```my_dc_location``` decides which code gets executed.

Another approach is the ```assert_type``` function:

    class my_example2 {
      if assert_type($::my_dc_location, String) {
        ...
      }
    }

