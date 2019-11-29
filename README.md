## The [DevOps] Guide to Puppet, Universe, and Everything

# SLIDES COLLECTION

This is collection of slides for presentation and workshops about Puppet.

This is part of The [DevOps] Guide to Puppet, Universe, and Everything:

- An Open Source [book](https://github.com/example42/puppetguide-book) [TODO]
- A set of sample Puppet code architectures. Evolved into the [psick project](https://github.com/example42/psick)
- A collection of [slides decks](https://github.com/example42/puppetguide-slides) (this repo)
- The [Puppet Universal Reference](https://github.com/example42/puppetguide-reference) [TODO]
- A collection of [Puppet cheatsheets](https://github.com/example42/puppetguide-cheatsheets) [TODO]

## Slide decks

We have different slides deck, for different purposes and skills:

- [Puppet Beginner](https://github.com/example42/puppetguide-slides/tree/master/PuppetBeginner) (Puppet usage and language basics) [Online rendered Slides](http://www.example42.com/guide/slides/beginner)
- [Puppet that Matters](https://github.com/example42/puppetguide-slides/tree/master/PuppetMatters) (Practical and useful stuff to know in order Deeper into Puppet language and components)

They are licensed under the [Creative Commons Attribution-NonCommercial](http://creativecommons.org/licenses/by-nc/4.0/) terms: they are free to use for not commercial purposes (you can use them for internal trainings in your company, but not for commercial trainings to your customers, unless you earn this right by sponsoring them. 

Sponsorships include:

- Your Logo on the main slide
- Social communication (Newsletter, Twitter, LinkedIN, Facebook, Google group... ) about the sponsorship
- LEGAL RIGHTS to use the slides for commercial purposes
- The certainty that the slide deck will be done in a given time period

For sponsorship opportunities [contact example42](http://www.example42.com/#contact).

## Rendering the slides

Slides are in markdown format and are rendered using Puppet's [showoff](https://github.com/puppetlabs/showoff) tool.

You can find the slides markdown files under the ```_slides``` directory. They are linked and used in the different decks according to what is defines in the ```showoff.json``` file of each deck directory.

In order to show them you have to install showoff:

    gem install showoff

Then move to the section you want to present and run showoff:

    cd Beginner
    showoff serve

Browse to http://127.0.0.1:9090 to see the slides.

Type ```t``` to show the table of contents.
