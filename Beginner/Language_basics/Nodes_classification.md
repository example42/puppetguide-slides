# Nodes classification

When clients connect, the Puppet Master generates a **catalog** with the list of the resources that clients have to apply locally.

The Puppet Master has to *classify* nodes and define for each of them:

- The **classes** to include
- The **parameters** to pass
- The Puppet **environment** to use

Nodes classification can be done in different ways (more details will follow):

- Using the ```node``` statement in Puppet
- Using and **External Node Classifier** (ENC): a separated tool that provides classification info
- Using the ```hiera_include``` function
- Using a nodeless setup: the classes to include are defined according to variables and facts.
