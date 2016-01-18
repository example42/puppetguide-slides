# Agenda
Why upgrading at all?
Is your code still working?
How to upgrading Puppet?
What brings Puppet 4?

Why do I need to bother?
Fast releases
Best Practices
Changing functionality
Removing deprecated stuff
Puppet 4 is coming

Why should I upgrade Puppet at all?
Do you want security updates?
Do you want to make use of new functionality? (e.g. automatic data bindings, environmentpath, future parser)
Do you want to get support (community or enterprise)?

Is my Puppet DSL code still working on new versions?
Your code was developed some years ago and is still running unmodified
Your code was written on old best practices and does not follow new style guide
You do not check your Puppet runs for deprecation warnings (or do you?)

What to look for?

BAD Best practice
Do you inherit from inherited classes?
Do you still use import?
Do you modify remote modules?
Do you access non-local variables without scope names?

BAD Best practice 
Stop doing multiple levels of inheritance
    class foo { }
    class foo::bar inherits foo { }
    class foo::baz inherits foo::bar { }
    class foo::foobar inherits foo::baz { }

BAD Best practice 
Stop doing inheritance at all
    class foo { }
    class foo::bar inherits foo { }
    class foo::baz inherits foo { }
    class foo::foobar inherits foo { }

Best practice
Restrict Inheritance
In most cases you can use parameterised classes instead. Only one kind of inheritance is proven good practice: inherit from module params.pp
    class ssh ( $server = $ssh::params::server, $client = $ssh::params::client, $x11fwd = false, ) inherits ssh::params { }
    class { ssh::params:: server => false, x11fwd => true, }

BAD Best practice 
Stop importing
    # foo/manifests/init.pp 
    class foo { import 'bar.pp'}
    # foo/manifests/bar.pp 
    class foo::baz { }
    # foo/manifests/baz.pp 
    class foo::baz { }

Which class foo::baz will be used?

Best practice 
Use include
In most cases you can make use of the puppet autoloader and you can use include.
    # foo/manifests/init.pp 
    class foo { include foo::baz }
    
    # foo/manifests/baz.pp
    class foo::baz { }

BAD Best practice 
Stop modifying remote modules
Take 'remote modules' as a software provided by others. Are you also patching apache?

Best practice Co-Work on remote modules
Do a PR if you want improvements.
Keep your remote modules upgradeable. BETTER

BAD Best practice 
Stop using non-local variables without scope
    class foo ( $bar = 'baz' ) { }
    class foo::baz { notify { $bar: } }

Best practice 
Start using non-local variables with scope
    class foo ( $bar ) { }
    class foo::baz { notify { $foo::bar: } } BETTER

Best practice 
Stop using un-scoped variables in templates
    key = <%= var %> BAD

Best practice 
Start using scoped variables in templates
    key = <%= @var %> BETTER

BAD Best practice 
Stop using factor variables without top-scope
    class foo { notify { "We are on OS: $operatingsystem": } }
    class foo::baz {
      if $is_virtual { 
        notify { "We are running on $virtual virtualisation": } 
      } else { 
        notify { "We are running on hardware: $productname": } 
      }
    }

Best practice 
Start using factor variables with top-scope
    class foo { notify { "We are on OS: ${::operatingsystem}": } }
    class foo::baz {
      if $::is_virtual { 
        notify { "We are running on ${::virtual} virtualisation": }
      } else { 
        notify { "We are running on hardware: ${::productname}": } 
      } BETTER
    }

BAD Best practice 
Stop not doing data validation
    class foo (
      $server = hiera('server', 'localhost')
    ){
      notify { "We will use Server: ${server}": } 
    }

Best practice BETTER 
Start doing data validation
    class foo (
      $server = hiera('server', 'localhost') 
    ){ 
      # validate_string is a function from stdlib 
      validate_string($server) 
      notify { "We will use Server: ${server}": } 
    }

Remote modules
Do foreign modules support your version?
Newer Puppet versions have new function attributes (arity)
New foreign module versions might need newer modules not supported by your Puppet version

