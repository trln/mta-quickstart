# marc-to-argot development machine

This defines a Centos-based vagrant box for working with marc-to-argot

## Usage

Install virtualbox.  Install vagrant.  Install the vagrant `vbguest` plugin, via
    
    $ vagrant plugin install vagrant-vbguest
    $ vagrant up
    $ vagrant ssh

You are now logged into the vagrant box.  Ruby 2.5.1, marc-to-argot, and the
argot-ruby gem should be installed, along with their command line utilities
`mta` and `argot`.  See the READMEs in the following repositories for more
information:

  * https://github.com/trln/marc-to-argot
  * https://github.com/trln/argot

The directory on the host machine (the one from which you run vagrant) is mounted at `/vagrant` on the VM.  So you should be able to copy MARCXML files on your host machine into this directory and process them using the `mta` tool via something like:


    $ mta create ncsu /vagrant/some-marcxml.xml argot-test.json

And so forth.
