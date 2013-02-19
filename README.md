Sample of how Symfony can be set up with Vagrant and Chef.
==========================================================

Installation
------------

*   Install [Virtualbox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/).
*   Clone this repository using 
    `git clone --recursive git://github.com/sebastianljunggren/symfony2-vagrant-sample.git`.
*   Change into the new directory: `cd symfony2-vagrant-sample`
*   Copy Vagrantfile.local.dist to Vagrantfile.local and change the variables to appropriate values
*   Set up the virtual machine with Vagrant: `vagrant up` (This step will take some time
    since it includes downloading a lot.)

Usage
-----

SSH into the machine with `vagrant ssh`. Then docroot is fount in "/home/vagrant/symfony".
When in the project folder symfony commands can be executed with `sf2` and composer commands with 
`composer`.