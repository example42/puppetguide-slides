# Roles and profiles

A common challenge we have when designing a Puppet architecture is how and where to define the logic that assigns to a group of nodes a specific set of classes (and the relevant resources).

There's not a single way or approach, but a consolidated best practices involves the usage of roles and profiles.

- A node has one and only one role (a variation involves more roles per node)

- Roles are classes that just include one or more profiles and describe the machines' function according to our business needs

- Profiles are classes that define a technological stack. They can include classes or declare them with parameters, they can have specific single resources. They either have parameters or hiera lookups inside the code.

- The modules that manage a single applications, typically the ones we find on the Forge for apache, nginx etc, are called **component** modules. Their classes and defines are supposed to be used in profile classes.

For further reference:

- The [original blog post](http://www.craigdunn.org/2012/05/239/) on Roles and Profiles by Craig Dunn 

- The series of [Gary Larizza's blog posts](http://garylarizza.com)

- Some [presentations](https://puppetlabs.com/presentations/designing-puppet-rolesprofiles-pattern) on Roles and Profiles
