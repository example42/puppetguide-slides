# Resource defaults
It's possible to set default argument values for a resource in order to reduce code duplication. The syntax is:

    Type {
      argument => value,
    }

Common examples:

    Exec {
      path => '/sbin:/bin:/usr/sbin:/usr/bin',
    }

    File {
      mode  => 0644,
      owner => 'root',
      group => 'root',
    }

Resource defaults can be overriden when declaring a specific resource of the same type.

Note that the "Area of Effect" of resource defaults might bring unexpected results. The general suggestion is:

Place **global** resource defaults in /etc/pupept/manifests/site.pp outside any node definition.

Place **local** resource defaults at the beginning of a class that uses them (mostly for clarity sake, as they are parse-order independent).
