Vagrant.configure(2) do |config|
    config.vm.box              = "magehost/trusty-apache-php5"
    config.vm.box_url          = "http://vagrant.magehost.pro/catalog.json"
    config.vm.define "magehost_app" do |node|
    end
    config.push.define "ftp" do |push|
        push.secure                = true
        push.host                  = "vagrant.magehost.pro:2222"
        push.username              = "vagrant"
        push.destination           = "httpdocs"
        push.exclude               = "old"
        push.exclude               = "*~"
    end
end
