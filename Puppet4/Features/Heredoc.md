# Heredoc support

With Puppet 3 it was already possible to specify the content of a file within a variable.
But this mostly lead to bad formatted code.

e.g.

    class my_motd {
      $content = "Welcome to ${::fqdn}
    This system is managed by Puppet.
    Local changes will be overwritten."
      file { '/etc/motd':
        ensure  => file,
        content => $content,
      }
    }

The $content variable spreads among multiple lines. To prevent empty whitespaces at the beginning of a new line, the content ha to start from first character.

