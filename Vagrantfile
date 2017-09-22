# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "scotchbox"
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
    
    config.vm.provider "virtualbox" do |v|
        v.name = "scotch_symfony"
    end
    
    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    config.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        yes Y | sudo apt-get install libapache2-mod-php7.0 libphp7.0-embed libssl-dev openssl php7.0-cgi php7.0-cli php7.0-common php7.0-dev php7.0-fpm php7.0-phpdbg php7.0-xml && sudo service apache2 restart
        sudo service apache2 restart
        sudo composer self-update
        rm -rf /var/www/public
        printf '\n\nscotchbox\nroot\n\n\n\n\n' | composer create-project symfony/framework-standard-edition /var/www/public
    SHELL
end
