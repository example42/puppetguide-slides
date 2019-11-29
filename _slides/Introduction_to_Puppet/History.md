# History of Puppet Versions

During its history Puppet has constantly improved and added features, still most of the core principles are the same and have't changed.

From version 2 Puppet follows [Semantic Versioning](http://semver.org/) standards to manage versioning, with a pattern like: MAJOR.MINOR.PATCH

This implies that MAYOR versions might not be backwards compatible, MINOR versions may introduce new features keeping compatibility and PATCHes are for backwards compatible bug fixes.

This is the history of the main Puppet versions and some relevant changes
Check also [Puppet Language History](http://docs.puppetlabs.com/guides/language_history.html) for a more complete review:

- ```0.9.x ```  - First public beta
- ```0.10.x/0.21.x```  - Various "early" versions
- ```0.22.x/0.25.x```  - Improvements and OS wider support
- ```2.6.x ```  - Many changes. Parametrized classes
- ```2.7.x ```  - Windows support
- ```3.x.x ```  - Many changes. Disabled dynamic variables scope. Data bindings
- ```3.2.x ```  - Future parser (experimental, will be default in Puppet 4)
- ```4.x.x ```  - Released in early 2015. New parser, new type system and lot of changes, various language cleanups and some backwards incompatibilities
- ```4.0.9 ```  - Released in February 2017. Hiera 5 is with data in modules is introduced.
- ```5.x.x ```  - Released in June 2017. No major changes. Ruby 2.4 used.
- ```6.x.x ```  - Released in September 2018. Some core types moved to separated modules. Resource API. CA moved to puppetserver. Deferred data type. 

In terms of code base migrations the biggest "jumps", which involve more or less large refactoring, have been:

- from ```0.x``` to ```2.6``` with the introduction of parametrized classes
- from ```2.x``` to ```3.x``` with the removal of variables dynamic scoping
- from ```3.x``` to ```4.x``` with the introduction of the Future parser
