# Nodes classification

When clients connect, the Puppet Master generates a **catalog** with the list of the resources that clients have to apply locally.

The Puppet Master has to *classify* nodes and define for each of them what are the classes to include.

Nodes classification can be done in different ways (more details will follow):

- Using the ```node``` definition in Puppet code
- Using an **External Node Classifier** (ENC): a separated tool that provides classification info
- Using **Hiera**
- Using a **nodeless setup**: the classes to include are defined according to variables and facts.
