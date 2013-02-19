Symfony development using Vagrant
=================================

Installation
------------

*   Install [Virtualbox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/).
*   Clone this repository using 
    `git clone --recursive git://github.com/sebastianljunggren/symfony2-vagrant-sample.git`.
*   Change into the new directory: `cd symfony2-vagrant-sample`
*   Copy Vagrantfile.local.dist to Vagrantfile.local and change the variables to appropriate values
*   Set up the virtual machine with Vagrant: `vagrant up` (This step will take some time
    since it includes downloading a lot.)
*   Add the following to your [hosts file](https://www.google.com/search?q=host+file):
    
    ```33.33.33.10     symfony.local```

*   Due to problems with shared folder performance on some platforms with Virtualbox another manual 
    step is required. Different ways of doing this is required for each platform:
    -   **Windows**

        [SSH into the virtual machine](http://docs.vagrantup.com/v1/docs/getting-started/ssh.html)
        and change into the project directory (`cd symfony`). Run `composer install`.

    -   **Linux**

        Make sure PHP is installed on the host. Then 
        [install Composer globally](http://getcomposer.org/doc/00-intro.md#globally) (also on the host). Change to the
        location of the project on the host and run `composer install`.

    -   **OSX**

        Not tested yet.

*   You should now be able to access http://symfony.local/app_dev.php in your browser and see a
    welcome page

Usage
-----

SSH into the machine with `vagrant ssh`. Then docroot is found in "/home/vagrant/symfony".
When in the project folder symfony commands can be executed with `sf2` and composer commands with 
`composer`.