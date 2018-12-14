# marc-to-argot development machine

This defines a Centos-based vagrant box for working with marc-to-argot and the spofford client.

## Usage

Install virtualbox.  Install vagrant.  Install the vagrant `vbguest` plugin, via
    
    $ vagrant plugin install vagrant-vbguest

Next, create a new, empty directory somewhere, and check this repository out
into that directory.  While vagrant is creating the virtual machine and getting it ready, it it will check out copies
of `marc-to-argot` and `spofford-client` from github and install them into the VM.

Next, run the following commands in the directory where you checked this repository out:

    $ vagrant up [--provider virtualbox] # last part if your host OS is linux

At this point, the VM is created and provisioned, and ready to run `mta` and `spofford`.  The provisioning process will create `marc-to-argot` and `spofford-client` directories as siblings of the directory containing the `Vagrantfile`, and both of these are active git repositories.

To log into your new VM,

    $ vagrant ssh

Ruby 2.5.1, marc-to-argot, argot-ruby, and the spofford-client gems will also be installed, along with their command line utilities `mta`, `argot`, and `spofford`.

See the READMEs in the following repositories for more details about running and developing.

## Working with the repositories.

The reason to check this repository out into a new, empty directory is to allow the Vagrant process to mount several shared folders that are synced between the VM and the host.  This allows you to use your favourite code editors and git software on the *host* that are visible from within the guest.

e.g. to make changes to `marc-to-argot` using, say, Notepad or Visual Studio Code on Windows, you would edit files under `..\marc-to-argot`, and this also changes files in `/home/vagrant/marc-to-argot` in the guest.  While logged into the guest, you can install a new `mta` script that incoroporates your changes via:

    $ cd /home/vagrant/marc-to-argot
    $ rake spec
    $ rake install
    $ mta create ncsu /path/to/some/marc.xml

Similarly for `argot` and `spofford` binaries.  See the documentation on the relevant projects for more information.

You can also use your preferred Git software (GitHub Desktop, e.g. or Sublime Merge, or the command line client) from  your host to do all the git stuff.  Other than pushing changes up to GitHub, the `git` command line client installed inside the VM can also be used for git operations.

More information:

  * https://github.com/trln/marc-to-argot
  * https://github.com/trln/argot-ruby
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
