BRIDGE_NET="192.168.0."
DOMAIN="naidadv.com"

servers=[
  #{
   # :hostname => "ansible." + DOMAIN,
    #:ip => BRIDGE_NET + "150",
	#:ram => "2000"
  #},
  {
    :hostname => "loadbalancer." + DOMAIN,
    :ip => BRIDGE_NET + "151",
	:ram => "2000"
  },
  {
    :hostname => "webapp." + DOMAIN,
    :ip => BRIDGE_NET + "152",
	:ram => "2000"
  },
  {
    :hostname => "database." + DOMAIN,
    :ip => BRIDGE_NET + "153",
	:ram => "2000"
  }
]

Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true
	servers.each do |machine|
		config.vm.define machine[:hostname] do |node|
			config.vm.box = "ubuntu/trusty64"
			node.vm.usable_port_range = (2200..2250)
			node.vm.hostname = machine[:hostname]
			node.vm.network "public_network", ip: machine[:ip], bridge: 'Intel(R) Wireless-AC 9560 160MHz'
			node.ssh.password = "vagrant"
			node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
				vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected"]
                vb.name = machine[:hostname]				
			end
		end
	end
end
