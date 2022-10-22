machines = {
  "master" => {"ip" => "10"},
  "node01" => {"ip" => "11"},
  "node02" => {"ip" => "12"},
}

Vagrant.configure("2") do |config|

  machines.each do |name , conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "bento/ubuntu-22.04"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "192.168.56.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = "1024"
        vb.cpus = "1"
        
      end
      machine.vm.provision "shell", path: "docker.sh"
      
      if "#{name}" == "master"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end
    end
  end
end