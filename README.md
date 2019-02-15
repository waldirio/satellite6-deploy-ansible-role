Hello all

Here you will find a simple way to install your Satellite. Let's do it.

Before, let's check some files that will be necessary update.

1. inventory
Inside the project directory, you will see the file `inventory`, update this file and add the IP addres or FQDN of the machine that you are planing to install. We will talk more about this file but at this time, this info will be enough. Below a example.
```
[node]
10.12.211.172
```

2. ssh
Once the main idea is use a `Bastion` to submit the playbook, will be necessary configure the ssh relation between them. To to that:
```
# ssh-keygen
# ssh-copy-id root@10.12.211.172
```
Note. Here I'm using the IP of my lab machine however in your case, feel free to use the correct IP address or fqdn.

We will talk about the vars/secret.yml file soon
```
# ansible-vault create vars/secret.yml
```
Ok, at this moment we are read to go. Let's take a look on the command below:
```
# ansible-playbook --ask-vault-pass sat6x-latest-installer.yml -e "node_name=node sat_hostname=wallsat64.usersys.redhat.com sat_version=6.4 baseos_version=7"
```
As you can see, there are some additional info under "". I'll explain below.

- Once we are using the encrypted file `ansible-vault` will be necessary this flag to prompt the password
```
--ask-vault-pass
```

- Remember the inventory file? node is the name of the group, if I add some additional IP address or FQDN under this group, the playbook will be send to all of them.
```
node_name=node 
```

- Here is the node FQDN
```
sat_hostname=wallsat64.usersys.redhat.com
```

- Here is the Satellite version to be installed (valid are 6.4, 6.3, 6.2, 6.1 and 6.0)
```
sat_version=6.4
```

- Here is the Base OS release (valid are 7 and 6)
```
baseos_version=7
```
