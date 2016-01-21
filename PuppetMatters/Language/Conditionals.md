# Conditionals
Puppet provides different constructs to manage conditionals inside manifests:

**Selectors** allows to set the value of a variable or an argument inside a resource declaration according to the value of another variable.
Selectors therefore just returns values and are not used to manage conditionally entire blocks of code.

**case statements** are used to execute different blocks of code according to the values of a variable. It's possible to have a default block for unmatched entries.
Case statements are NOT used inside resource declarations.

**if elsif else** conditionals, like case, are used to execute different blocks of code and can't be used inside resources declarations.
We can can use any of Puppet's comparison expressions and we can combine more than one for complex patterns matching.

**unless** is somehow the opposite of **if**. It evaluates a boolean condition and if it's *false* it executes a block of code. It doesn't have elsif / else clauses.
