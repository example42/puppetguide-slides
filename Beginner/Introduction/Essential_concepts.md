# Essential Puppet concepts

When approaching Puppet it's important to understand it's basic concepts and terminology. A complete official [glossary](http://docs.puppetlabs.com/references/glossary.html) is online, here we outline the most important Puppet concepts:

- A typical Puppet setup is based on a client-server architecture: the client is also called **agent** (or **agent node** or simply **node**), the server is called **master**
- The master provides a **catalog** that contains all the resources and their relationships that have to be applied to a given node.
- The catalog is based on Puppet code written in **manifests** (files with **.pp** extension) parsed by the master 
- In the code we declare **resources** that affect elements of the system (files, packages, services ...)
- Resources are grouped in **classes** which may expose **attributes** that affect their behavior.
- Classes and the configuration files that are shipped to nodes are organized in **modules**.
- On each node **facter** is executed to retrieve **facts**: piece of information about the node that are available as variables on the master during compilation.
