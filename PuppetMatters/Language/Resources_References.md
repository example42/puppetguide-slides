# Resource references
In Puppet any resource is uniquely identified by its type and its name.
We can't have 2 resources of the same type with the same name in a catalog.

We have seen that we declare resources with a syntax like:

    type { 'name':
      arguments => values,
    }

When we need to reference to them in our code the syntax is like:

    Type['name']

Some examples:

    file { 'motd': ... }
    apache::virtualhost { 'example42.com': .... }
    exec { 'download_myapp': .... }

are referenced, respectively, with

    File['motd']
    Apache::Virtualhost['example42.com']
    Exec['download_myapp']
