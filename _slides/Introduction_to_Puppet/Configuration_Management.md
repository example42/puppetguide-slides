# DevOps and Configuration management

DevOps is a [term](https://en.wikipedia.org/wiki/DevOps) that involves a remarkable number of concepts, nuances and definitions.

We won't try to give another one, but we can safely say that DevOps is (also) about **culture**, **processes**, **people** and **tools**.

A complete [DevOps tools chain](https://xebialabs.com/the-ultimate-devops-tool-chest/) contains software of these categories:

- Source Code Management (We use them when writing Puppet code)
- Repository and software Management  (Puppet can configure them)
- Software build (Puppet can configure them)
- Configuration Management (**Puppet is here**)
- Testing  (We can test our Puppet code)
- Monitoring and data analysis  (Puppet can configure them)
- Systems and Applications Deployment (Puppet can be also here)
- Continuous integration  (We can manage Puppet code deployments in a CI pipeline)
- Cloud (Puppet code can manage cloud resources)
- Project management and Issue tracking  (We can use them to manage our Puppet projects)
- Messaging and Collaboration (We can use them to collaborate on Puppet works)
- Containerization and Virtualization (Puppet can configure them)
- Databases (Puppet can configure them)
- Application servers (Puppet can configure them)


# Configuration Management principles

Configuration management tools allow to programmatically define how servers have to be configured. Their main benefits are:

- **Automation**: No need to manually configure systems
- **Reproducibility**: Setup once, repeat forever
- **Recoverability**: Setup again in case of outage
- **Scale**: Done for one, use on many
- **Coherent** and consistent server setups
- **Aligned Environments** for development, test, qa, production nodes

Configuration management tools typically describe the systems setups via code or data (**Infrastructure as Code**), this involves a paradigm change in system administration:

- Systems are managed **centrally** in an **automated** way: no more manually
- Code is versioned with a Source Control Management tool (**git** is the most used in Puppet world)
- Commits history shows the **history of change** on the infrastructure (who, what, when and why)
- Code can be **tested** before deployment in production
- Code has to be **deployed** after a CI/CD pipeline


# Configuration Management tools

Common alternatives to Puppet:

#### [Chef](https://www.chef.io/)

- Has Chef clients that connect to Chef server
- Has characteristic similar to Puppet
- Community code is shared on the [Chef Supermarket](https://supermarket.chef.io)
- Chef code is Ruby with dedicated extensions
- Software developed in Ruby.

#### [CFEngine](http://cfengine.com/)

- The first and oldest of the bunch
- CFEngine3 is a complete and modern rework
- Different daemons for different functions in a distributed environment
- Based on the [Promise theory](https://en.wikipedia.org/wiki/Promise_theory)
- Software developed in C by Prof. Mark Burgess.

#### [Salt](http://saltstack.com/)

- Manages deployments on multiple clouds in a fast way
- Salt code is composed of states (Puppet resources) written in YAML files
- [Formulas](https://github.com/saltstack-formulas) are equivalent to modules
- Sotfware developed in Python

####  [Ansible](http://www.ansibleworks.com/)

- Quick setup, no agents, communications over SSH
- Ansible code is YAML based and written on playbooks
- Roles are equivalent to modules, they are shared on the [Ansible Galaxy](https://galaxy.ansible.com/)
- Can centralise multi node task executions, software deployments and configuration management.
- Software developed in Python. Bought by RedHad in October 2015
