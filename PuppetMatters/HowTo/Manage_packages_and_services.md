# Managing packages

Installation of packages is managed by the **package** type.

The main arguments:

    package { 'apache':
      name      => 'httpd',  # (namevar)
      ensure    => 'present' # Values: 'absent', 'latest', '2.2.1'
      provider  => undef,    # Force an explicit provider
    }


# Managing services

Management of services is via the **service** type.

The main arguments:

    service { 'apache':
      name      => 'httpd',  # (namevar)
      ensure    => 'running' # Values: 'stopped', 'running'
      enable    => true,     # Define if to enable service at boot (true|false)
      hasstatus => true,     # Whether to use the init script' status to check
                             # if the service is running.
      pattern   => 'httpd',  # Name of the process to look for when hasstatus=false
    }
