# Classification

When clients connect, the Puppet Master generates a **catalog** with the list of the resources that clients have to apply locally.

The Puppet Master has to **classify** nodes setting for each of them what are the classes to include.

Classes contain the resources to manage on the node.

Nodes classification can be done in different ways (more details will follow):

- Using the ```node``` statement in Puppet code
- Using an **External Node Classifier** (ENC): a separated tool that provides classification info
- Using **Hiera**, Puppet's companion tool to manage configuration data
- Using a **nodeless setup**: the classes to include are defined according to variables and facts.
