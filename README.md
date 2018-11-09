# marc-to-argot development machine

This defines a Centos-based vagrant box for working with marc-to-argot

## Usage

Install virtualbox.  Install vagrant.  Install the vagrant `vbguest` plugin, via
    
    $ vagrant plugin install vagrant-vbguest
    $ vagrant up
    $ vagrant ssh

You are now logged into the vagrant box.  Ruby 2.5.1, marc-to-argot, argot-ruby, and the spofford-client gems will also be installed, along with their command line utilities `mta`, `argot`, and `spofford`.

See the READMEs in the following repositories for more
information:

  * https://github.com/trln/marc-to-argot
  * https://github.com/trln/argot
  * https://github.com/trln/spofford-client

The directory on the host machine (the one from which you run vagrant) is mounted at `/vagrant` on the VM.  So you should be able to copy MARCXML files on your host machine into this directory and process them using the `mta` tool via something like:

    $ mta create ncsu /vagrant/some-marcxml.xml argot-test.json

And so forth.

## `mrcToXml`

The `/vagrant` directory also contains a shell script (which is copied to
`/home/vagrant/bin`, meaning it's on the default user's PATH) that converts the
MARC8-encoded MARC21 files exported by Sirsi into UTF-8 encoded MARCXML (which
is what `mta` is configured to work with NCSU's records).  This script can
read from STDIN or a filename, and can output to a filename or STDOUT, so the
following are all equivalent:

    $ mrcToXml some-marc8-file.mrc utf8marcxml.xml
    $ mrcToXml < some-marc8-file.mrc > utf8marcxml.xml
    $ cat some-marc8-file.mrc | mrcToXml > utf8marcxml.xml

(although the last falls under the 'useless use of `cat` description ...)
