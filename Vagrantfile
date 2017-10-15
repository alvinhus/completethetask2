VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/xenial64"
  config.vm.synced_folder ".", "/vagrant", disabled:true

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.define:mini do |mini|
end

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  #config.vm.synced_folder "./app", "/var/www/django-app"
 config.vm.provider :aws do |aws, override|
	  aws.access_key_id = ENV['AWS_ACCESS_KEY']
	  aws.secret_access_key = ENV['AWS_SECRET_KEY']
	  aws.region = "eu-west-1"
	  aws.availability_zone = "eu-west-1"

	  # AMI from which we'll launch EC2 Instance
	  aws.ami =  "ami-eed00d97" # Ubuntu 16.04 HVM
	  aws.keypair_name = "vagrant"
	  aws.instance_type = "t2.micro"
	  aws.block_device_mapping = [{
                                       'DeviceName' => '/dev/sda1', 
                                       'Ebs.VolumeSize' => 10,
				       'Ebs.VolumeType'=>'gp2',
                                       'Ebs.DeleteOnTermination'=>'true' }]
	  aws.security_groups = ["vagrant-sg"]
          aws.tags = {
		        'Name' => 'Vagrant EC2 Instance',
			'Environment' => 'vagrant-sandbox'
		     }  
          # Credentials to login to EC2 Instance
	  override.ssh.username = "ubuntu"
	  override.ssh.private_key_path = ENV['AWS_PRIVATE_KEY']
  end

  config.vm.provision "shell" do |s|
    s.inline = "apt-get install -y python"
  end
config.vm.provision "ansible" do |ansible|
  ansible.groups= {
     "main" =>["default"]
    }

  ansible.playbook = "provisioning/playbook.yml"

end
end
