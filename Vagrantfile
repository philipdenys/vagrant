Vagrant.configure(2) do |config|
    config.ssh.forward_agent             = true
    config.vm.box                        = "magehost/trusty-apache-php5"
    config.vm.box_url                    = "http://magentohosting.pro/vagrant/catalog.json"
    config.vm.synced_folder              "httpdocs", "/data/vhosts/magehostdev.pro/httpdocs", create: true
    config.vm.provision                  "shell", inline: "/bin/bash /root/bin/provision.sh"
    config.vm.hostname                   = 'magehostdev.pro'
    config.vm.network                    "private_network", type: "dhcp"
    config.vm.define "magehost_app" do |node|
    end
    if Vagrant.has_plugin?("vagrant-hostmanager")
        config.hostmanager.enabled           = true
        config.hostmanager.manage_host       = true
        config.hostmanager.ignore_private_ip = false
        config.hostmanager.include_offline   = true
        config.hostmanager.aliases           = %w(www.magehostdev.pro)
        config.hostmanager.ip_resolver = proc do |vm, resolving_vm|
            if hostname = (vm.ssh_info && vm.ssh_info[:host])
                `vagrant ssh -c "/usr/local/bin/get_local_ip.sh eth1"`
            end
        end
    end
    config.vm.provider "parallels" do |prl|
        prl.update_guest_tools           = true
        prl.use_linked_clone             = true
    end
    config.push.define "ftp" do |push|
        push.secure                      = true
        push.host                        = "vagrant.magehost.pro:2222"
        push.username                    = "vagrant"
        push.destination                 = "httpdocs"
        push.exclude                     = "old"
        push.exclude                     = "parallels"
        push.exclude                     = "*~"
        push.exclude                     = ".*"
    end
end