# Configuration Management

Configuration management tools allow to programmatically define how servers have to be configured. Their main benefits are:

- **Automation**: No need to manually configure systems
- **Reproducibility**: Setup once, repeat forever
- **Scale**: Done for one, use on many
- **Coherent** and consistent server setups
- **Aligned Environments** for devel, test, qa, prod nodes

Configuration management tools typically describe the systems setups via code or data (**Infrastructure as Code**), this involves a paradigm change in system administration:

- Systems are managed centrally and no more manually
- Code is versioned with a Source Control Management tool (**git** is the most used in Puppet world)
- Commits history shows the **history of change** on the infrastructure (who, what, when and why)
- Code can be tested before deployment in production
- Code has to be deployed


# Configuration Management tools

Common alternatives to Puppet:

- [Chef](http://www.opscode.com/chef/)
- [CFEngine](http://cfengine.com/)
- [Salt](http://saltstack.com/)
- [Ansible](http://www.ansibleworks.com/)
