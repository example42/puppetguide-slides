# Executing commands

We can run plain commands using Puppet's **exec** type. Since Puppet applies it at every run, either the command can be safely run multiple times or we have to use one of the **creates**, **unless**, **onlyif**, **refreshonly** arguments to manage when to execute it.

    exec { 'get_my_file':
        # (namevar) The command to execute
        command   => "wget http://mysite/myfile.tar.gz -O /tmp/myfile.tar.gz',
        # The search path for the command. Must exist when command is not absolute
        # Often set in Exec resource defaults
        path      => '/sbin:/bin:/usr/sbin:/usr/bin',
        # A file created by the command. It if exists, the command is not executed
        creates   => '/tmp/myfile.tar.gz',
        # A command or an array of commands, if any of them returns an error
        # the command is not executed
        onlyif    => 'ls /tmp/myfile.tar.gz && false',
        # A command or an array of commands, if any of them returns an error
        # the command IS executed
        unless    => 'ls /tmp/myfile.tar.gz',
    }
