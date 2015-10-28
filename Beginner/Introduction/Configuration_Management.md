# DevOps and Configuration management

DevOps is a [term](https://en.wikipedia.org/wiki/DevOps) that involves a remarkable number of concepts, nuances and definitions.

We won't try to give another one, but we can safely say that DevOps is (also) about **culture**, **processes**, **people** and **tools**.

A complete [DevOps tools chain](https://xebialabs.com/the-ultimate-devops-tool-chest/) contains software of these categories:

- Source Code Management
- Repository and software Management
- Software build
- Configuration Management (<- Puppet is here)
- Testing
- Monitoring and data analysis
- Systems and Applications Deployment (<- Puppet is somehow also here)
- Continuous integration
- Cloud
- Project management and Issue tracking
- Messaging and Collaboration
- Containerization and Virtualization
- Databases
- Application servers


# Configuration Management principles

Configuration management tools allow to programmatically define how servers have to be configured. Their main benefits are:

- **Automation**: No need to manually configure systems
- **Reproducibility**: Setup once, repeat forever
- **Scale**: Done for one, use on many
- **Coherent** and consistent server setups
- **Aligned Environments** for devel, test, qa, prod nodes

Configuration management tools typically describe the systems setups via code or data (**Infrastructure as Code**), this involves a paradigm change in system administration:

- Systems are managed **centrally** in an **automated** way: no more manually
- Code is versioned with a Source Control Management tool (**git** is the most used in Puppet world)
- Commits history shows the **history of change** on the infrastructure (who, what, when and why)
- Code can be **tested** before deployment in production
- Code has to be **deployed**


# Configuration Management tools comparison

Common alternatives to Puppet:

### [Chef](https://www.chef.io/)

- Has Chef clients that connect to Ceph server
- Has characteristic similar to Puppet
- Community code is shared on the [Chef Supermarket](https://galaxy.ansible.com/intro#review)
- Developed in Ruby.

### [CFEngine](http://cfengine.com/) - Written in C. The oldest CF tool around

- The first and oldest of the bunch
- CFEngine3 is a complete rework
- Developed  in C by Mark Burgess.

### [Salt](http://saltstack.com/) - Does cloud provisioning and configuration management

- Manages deployments on multiple clouds
- Developed in Python

###  [Ansible](http://www.ansibleworks.com/)

- Quick setup, no agents, communications over SSH
- Playbooks are Ansible manifests, with a simple YAML based
- Roles are equivalent to modules, they are shared on the [Ansible Galaxy](https://galaxy.ansible.com/intro#review)
- Can centralise multi node task executions, software deployments and configuration management.
- Developed in Python
- Bought by RedHad in October 2015
