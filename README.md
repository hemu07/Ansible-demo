#configure target server (ubuntu instance using ansible server)

- Spin up two servers on AWS (ubuntu servers)
![image](https://github.com/hemu07/Ansible-demo/assets/90203539/a911f649-43a1-495a-ada1-7343e9a39dc6)

- in the Ansible server, install Ansible
  `sudo apt update`
  `sudo apt install ansible `

- configure passwordless authentication so that the Ansible server can access target servers without any password
- in the ansible server, generate public/private key:
  `ssh-keygen`
  this will generate public, and private keys and store them in /home/ubuntu/.ssh folder

- do the same in the target server, ssh-keygen
- add the public key in the target server--> authorised_keys folder to implement passwordless authentication
  by default the .pem key details will be there in this server (keypair used while creating the server) -- overwrite this public key on that
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/f406ceca-a24e-4369-90b3-5bb3bd3c03c2)

- now from the Ansible server, SSH into the target server
  `ssh target-server-private-ipv4`
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/01aeb030-59af-467a-9dc5-2cb3a09e1e69)
- we are now logged in to the target server without a password

- now we can write an Ansible playbook to manage the target servers
   
    - inventory file: a simple txt file with private IP addresses of target servers
- add the target server's private IP in this file

- Ansible ADHOC commands
  ` ansible -i inventory.txt all -m "shell" -a "touch devops calls"`
  this command will execute shell command [-m "shell" indicates use shell module to execute the later commands]
                                          [-a indicates to execute the command in target server ]
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/23b9eb83-a30b-4d21-bb86-8f30478fe847)

- we can execute simple shell commands like this
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/f8e43f2a-6a24-4f4a-96a0-fdc86cf9c9fd)

- for managing different types of servers like webserver/ db servers/ test server/ staging servers etc group them in the inventory file using []
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/e895c1dd-db77-42c9-9857-4cd602591dc8)
- at runtime give the specific server group name to configure the changes in the specific server group

  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/22a6ae06-f73f-49ef-a7c5-bfae4148fdf1)
  here, we are creating demo files, in db servers with dbserver name  and in webserver with webserver name
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/c023cc7a-85d8-410b-b13f-7f06b1e3a212)
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/e20c2cca-ba61-49d3-9c1c-f5313d384da4)
  The same is visible on the respective servers

- we write Ansible playbook when there are multiple tasks to be performed if one or two are to then go with Ansible ad-hoc commands
- 
  - playbook is a Yaml.manifest file
    
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/2c03f022-a377-4fe7-a417-63bb69bfb572)

- run the playbook file using `ansible-playbook -i inventory.txt my-first-playbook`
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/4a25590a-f827-47c0-99dc-9dd7c964d79c)

- Verify NGINX running in the target server
  ![image](https://github.com/hemu07/Ansible-demo/assets/90203539/10507491-f6cf-4661-857a-a8a1b7f5e4f9)

- in real-time usecase ansible-playbook will be used to manage Kubernetes clusters
