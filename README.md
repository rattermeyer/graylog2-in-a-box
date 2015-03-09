# graylog2-in-a-box #

Vagrant box with Graylog2 server installed. The vagrant box uses a virtual private host adapter with the IP address 192.168.56.100.

**Usage for provisioning the vagrant box itself (e.g. when you start the vagrant box from a Windows OS):**

You have to uncomment the lines for the shell provisioning to install ansible inside the box.

	# config.vm.provision "shell", path: "install_in_box.sh" 

After that comment out the ansible provisioner.

	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "provisioning/playbook.yml"
	end

Then run the follwing commands:

	vagrant up
	vagrant ssh	
	cd /home/vagrant && git clone https://github.com/fred4jupiter/graylog2-in-a-box.git
	cd ~/graylog2-in-a-box/provisioning
	ansible-playbook -i inventory playbook.yml


**Usage for provisioning the vagrant box from a Linux/Unix system:**

    vagrant up

##Graylog2 Web Interface##

After waiting a long time for provisioning you can access graylog2 web interface under:

[http://192.168.56.100:9000/](http://192.168.56.100:9000/ "Graylog2 Web Console")

	Username: admin
	Password: yourpassword

## Helpfull commands ##

Testing if Elasticsearch is running:

	curl -XGET 'http://192.168.56.100:9200/_cluster/health?pretty=true'

Before running the ansible playbook you can test which tasks would be executed by running:

	ansible-playbook --syntax-check --list-tasks -i inventory playbook.yml