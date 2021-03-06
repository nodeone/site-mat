Vagrant.configure("2")  do |config|
    config.vm.box = "precise64"
    # The url from where the 'config.vm.box' box will be fetched if it
    # doesn't already exist on the user's system.
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"

    # Disable totally unnecessary default shared folder
    config.vm.synced_folder '.', '/vagrant', :id => 'vagrant-root', :disabled => true


    # Assign this VM to a host only network IP, allowing you to access it
    # via the IP.
    config.vm.network :private_network, ip: "192.168.50.32"
    config.vm.hostname = "mat.lollen"

    config.vm.provider "virtualbox" do |v|
        v.name = "MatBuild.se"
        v.customize ["modifyvm", :id, "--memory", "2048"]
        v.customize ["modifyvm", :id, "--cpus", "1"]
    end

    # Provisioning settings.
    config.vm.provision :puppet do |puppet|
       # Cheat a bit to get our usual webroot
       puppet.facter = {
        'drupal_root' => '/srv/www/site-mat/web'
       }
       puppet.manifests_path = "./"
       puppet.manifest_file = "manifests/site.pp"
       puppet.module_path = "./manifests/modules"
     end

     #Change if you need a difefrent drush version
     config.vm.provision :shell do |shell|
        shell.inline = "drush dl drush-7.x-5.9 -y"
     end
    # The path to the platform
    config.vm.synced_folder "./", "/srv/www/site-mat", :nfs => true

end
