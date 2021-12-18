Vagrant.configure("2") do |config|
	(1..3).each do |i|
		config.vm.define "server#{i}" do |bd|
			bd.vm.box = "ubuntu/focal64"
			bd.vm.network "public_network", ip: "192.168.13.20#{i}", bridge: "wlp2s0"
			bd.vm.hostname = "server#{i}"

			bd.vm.provision "shell" do |s|
				ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
				s.inline = <<-SHELL
				echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
				SHELL
			end

			bd.vm.provider "virtualbox" do |v|
				v.name = "server#{i}"
				v.memory = 1024
				v.cpus = 1
			end
		end
	end
end