Vagrant and PuPHPet on Windows7
=======

LAMP, CentOS 6.5, Apache 2.4, PHP 5.6, MySQL 5.6, MongoDb 2.6.6

.. with Rsync (best performance)

1. Download and install Oracle VirtualBox (https://www.virtualbox.org/wiki/Downloads)
2. Download and install Vagrant (https://www.vagrantup.com/downloads.html)
3. Download and install Cygwin (with rsync) (https://cygwin.com/install.html)
4. Go to PuPHPet (https://puphpet.com/) - Online GUI configurator for Puppet & Vagrant and configure your own new unix system
    - choose Rsync syncing folder
    - in parameters type:
        - "--chmod=ug=rwX,o=rX" for proper permissions on your guest machine (unix)
        - "--delete" for deleting already deleted files on you host machine (windows)
        - "--links" for proper copying symlinks from guest (unix) to host (windows)
    - in source type: "c:/xampp/htdocs/vagrant/workspace" or other folder
    - in target type "/var/www/workspace"
5. Create vagrant folder ie. c:/xampp/htdocs/vagrant
6. Extract and paste there your PuPHPet files
    - edit "Vagrant" file and paste on top as 3rd line:
        - ENV["VAGRANT_DETECTED_OS"] = ENV["VAGRANT_DETECTED_OS"].to_s + " cygwin"
        - this fix problems with cygwin rsync on Windows 
7. Run console, ie. "cmd" or "Cygwin64 Terminal" or "Git Bash", and go that folder
8. Run command: "vagrant up", if everything will be ok, you will see the green welcome message.
    - if you see on your VirtualBox screen shot information about problem with your processor x86,
      you need go to bios and enable virtualization in processor settings
    - if you see other message, probably some package you chose have some problems, go to PuPHPet and chose another one
    - other bugs - pray :)
9. Run command "vagrant plugin install vagrant-rsync-back"
    - now you can sync your guest (unix) files to host (windows)
10. Login to guest (host) by command: "vagrant ssh"
    - next "cd /var/www/workspace", create some files "touch example.php"
    - on second console go to vagrant folder and type "vagrant rsync-back"
    - your file "example.php" should be in your host workspace
11. To auto rsync your host files to guest (one direction) type "vagrant rsync-auto"
12. Enjoy! (I spent 20h to fix all problems) 

