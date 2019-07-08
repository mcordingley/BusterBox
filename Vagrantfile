Vagrant.configure('2') do |config|
    config.ssh.insert_key = false
    config.vm.box = "debian/buster64"

    config.vm.provider :virtualbox do |vb|
        vb.name = "BusterBoxBuild"
    end

    config.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
    end
end