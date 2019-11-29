# Executing commands

We can run plain commands using Puppet's **exec** type. Since Puppet applies it at every run, either the command can be safely run multiple times or we have to use one of the **creates**, **unless**, **onlyif**, **refreshonly** arguments to manage when to execute it.

    @@@ Puppet
    exec { 'get_my_file':
        command => 'wget http://mysite/myfile.tar.gz -O /tmp/myfile.tar.gz',
        path    => '/sbin:/bin:/usr/sbin:/usr/bin',
        creates => '/tmp/myfile.tar.gz', 
        onlyif  => 'ls /tmp/myfile.tar.gz && false',
        unless  => 'ls /tmp/myfile.tar.gz',
        user    => 'my_user',
    }

The parameters are as follows:

- **command**, (namevar, if not specified, title is used) The actual command to execute
- **path**, the search paths where to look for the command, if not set, command must have an absolute path
- **creates**, a method to test if to run command, it refers to a file created by the command. It if exists, the command is not executed
- **onlyif**, alternative test method, if command here  returns an error the main command IS NOT executed
- **unless**, alternative test method, if command here  returns an error the main command IS executed
- **user**, which user the command should be run as (default root)