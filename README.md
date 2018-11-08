# marc-to-argot development machine

This defines a Centos-based vagrant box for working with marc-to-argot

## Usage

Install virtualbox.  Install vagrant.

    $ vagrant up

    $ vagrant ssh

You are now logged into the vagrant box.  Ruby 2.5.1, marc-to-argot, and the
argot-ruby gem should be installed, along with their command line utilities
`mta` and `argot`.  See the READMEs in the following repositories for more
information:

  * https://github.com/trln/marc-to-argot
  * https://github.xom/trln/argot
