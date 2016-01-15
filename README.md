# The [DevOps] Guide to Puppet, Universe, and Everything

This is an holistic documentation project about Puppet.

It consists on:

- An Open Source [book](https://github.com/example42/puppetguide-book)

- A set of sample Puppet code [architectures](https://github.com/example42/puppetguide-architectures)

- A modular set of [Slides](https://github.com/example42/puppetguide-slides) (this repo)

- The [Puppet Universal Reference](https://github.com/example42/puppetguide-reference)

To support this project check our [IndieGogo campaign](https://www.indiegogo.com/projects/the-devops-guide-to-puppet-universe-and/x/12116665#/)

## Slide decks

Slides are in markdown format and are rendered using Puppet Labs's [showoff](https://github.com/puppetlabs/showoff).

We have different slides deck, for different purposes and skills:

- [DONE] [Beginner](https://github.com/example42/puppetguide-slides/tree/master/Beginner) (Puppet usage and language basics) [Online rendered Slides](http://www.example42.com/guide/slides/beginner)
- [WIP] [Puppet that Matters](https://github.com/example42/puppetguide-slides/tree/master/PuppetMatters) (Practical and useful stuff to know in order Deeper into Puppet language and components)
- [WIP] [Puppet 4](https://github.com/example42/puppetguide-slides/tree/master/Puppet4) (A guide to Puppet 4 features and innovations)
- [TODO] [Alien Puppet](https://github.com/example42/puppetguide-slides/tree/master/AlienPuppet) (Puppet to manage Windows, Cloud infrastructures and network devices)
- [TODO] [Deploying Puppet](https://github.com/example42/puppetguide-slides/tree/master/DeployingPuppet)  (A guide to Puppet testing methodologies and deployment patterns)
- [TODO] [Puppet developing](https://github.com/example42/puppetguide-slides/tree/master/PuppetDeveloping) (A guide to development of Puppet extensions)
- [TODO] [Puppet Orchestration](https://github.com/example42/puppetguide-slides/tree/master/PuppetOrchestration) (A guide to MCollective and Application Orchestration)

Development of each slide deck can be sponsored. Sponsorships include:

- Your Logo on the main slide
- Social communication (newsletter, Twitter... ) about the Sponsorships
- LEGAL RIGHTS you use the slides for commercial purposes
- The certainty that the slide desk will be made in a given time period

For sponsoring opportunities [contact example42](http://www.example42.com/#contact)


## Rendering the slides

You can find the source markdown files under the relevant directories.

In order to show them you have to install showoff:

    gem install showoff

Then cd to the section you want to present and run showoff:

    cd Beginner
    showoff serve

Browse to http://127.0.0.1:9090 to see the slides.

Type ```t``` to show the table of contents.
