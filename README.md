# completethetask2
Test task 2 assignment
The task is done using Vagrant Version 2.0.0, virtualbox and AWS
Operating system used for virtualbox and aws is ubuntu/xenial64

Prerequisites
- Valid aws account with keys
- Prior to start provisioning through aws it is needed to set up following environmental variables:
	export AWS_ACCESS_KEY="REPLACE_WITH_VALID_AWS_ACCESS_KEY" 
	export AWS_SECRET_KEY="REPLACE_WITH_VALID_AWS_SECRET_KEY"
	export AWS_PRIVATE_KEY="/path_to_AWS_private_key/vagrant.pem"
- Install vagrant aws plugin by typing 
	vagrant plugin install vagrant-aws
- Download vagrant dummy box for aws
	vagrant box add	dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box

	
1. in terminal run "git clone https://github.com/alvinhus/completethetask2"
2. change active directory to completethetask2 by running "cd completethetask2"
3. To start machine on aws type
	vagrant up --provider=aws
4. To start machine on local virtualbox type "vagrant up" and mini is available at 
	http://localhost:8080
	

