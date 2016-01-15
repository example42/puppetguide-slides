# Agenda • Why upgrading at all? • Is your code still working? • How to upgrading Puppet? • What brings Puppet 4?
6. Why do I need to bother? • Fast releases • Best Practices • Changing functionality • Removing deprecated stuff • Puppet 4 is coming
7. Why should I upgrade Puppet at all? • Do you want security updates? • Do you want to make use of new functionality? (e.g. automatic data bindings, environmentpath, future parser) • Do you want to get support (community or enterprise)?
8. Is my Puppet DSL code still working on new versions? • Your code was developed some years ago and is still running unmodified • Your code was written on old best practices and does not follow new style guide • You do not check your Puppet runs for deprecation warnings (or do you?)
9. What to look for?
10. BAD Best practice • Do you inherit from inherited classes? • Do you still use import? • Do you modify remote modules? • Do you access non-local variables without scope names?
11. BAD Best practice Stop doing multiple levels of inheritance ! class foo { } ! class foo::bar inherits foo { } ! class foo::baz inherits foo::bar { } ! class foo::foobar inherits foo::baz { }
12. BAD Best practice Stop doing inheritance at all ! class foo { } ! class foo::bar inherits foo { } ! class foo::baz inherits foo { } ! class foo::foobar inherits foo { }
13. Best practice Restrict Inheritance ! In most cases you can use parameterised classes instead. Only one kind of inheritance is proven good practice: inherit from module params.pp ! class ssh ( $server = $ssh::params::server, $client = $ssh::params::client, $x11fwd = false, ) inherits ssh::params { } ! class { ssh::params:: server => false, x11fwd => true, } BETTER
14. BAD Best practice Stop importing ! # foo/manifests/init.pp class foo { import ‘bar.pp’ } ! # foo/manifests/bar.pp class foo::baz { } ! # foo/manifests/baz.pp class foo::baz { } ! Which class foo::baz will be used?
15. Best practice Use include ! In most cases you can make use of the puppet autoloader and you can use include. ! # foo/manifests/init.pp class foo { include foo::baz } BETTER ! # foo/manifests/baz.pp class foo::baz { } !
16. BAD Best practice Stop modifying remote modules ! Take “remote modules” as a software provided by others. Are you also patching apache?
17. Best practice Co-Work on remote modules ! Do a PR if you want improvements. ! Keep your remote modules upgradeable. BETTER
18. BAD Best practice Stop using non-local variables without scope ! class foo ( $bar = ‘baz’ ) { } ! class foo::baz { notify { $bar: } }
19. Best practice Start using non-local variables with scope ! class foo ( $bar ) { } ! class foo::baz { notify { $foo::bar: } } BETTER
20. Best practice Stop using un-scoped variables in templates !! key = <%= var %> ! ! ! BAD
21. Best practice Start using scoped variables in templates !! key = <%= @var %> !!!! BETTER
22. BAD Best practice Stop using factor variables without top-scope ! class foo { notify { “We are on OS: $operatingsystem”: } } ! class foo::baz { if $is_virtual { notify { “We are running on $virtual virtualisation”: } } else { notify { “We are running on hardware: $productname”: } }
23. Best practice Start using factor variables with top-scope ! class foo { notify { “We are on OS: ${::operatingsystem}”: } } ! class foo::baz { if $::is_virtual { notify { “We are running on ${::virtual} virtualisation”: } } else { notify { “We are running on hardware: ${::productname}”: } } BETTER
24. BAD Best practice Stop not doing data validation ! class foo ( $server = hiera(‘server’, ‘localhost’) ){ notify { “We will use Server: ${server}”: } } !
25. Best practice BETTER Start doing data validation ! class foo ( $server = hiera(‘server’, ‘localhost’) ){ # validate_string is a function from stdlib validate_string($server) notify { “We will use Server: ${server}”: } } !
26. Remote modules • Do foreign modules support your version? • Newer Puppet versions have new function attributes (arity) • New foreign module versions might need newer modules not supported by your Puppet version
