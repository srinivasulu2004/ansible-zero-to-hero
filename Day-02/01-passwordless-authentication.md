# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

PRACTICALS.....................

PASSWORDLESS AUTHENTICATION(...UISNG SSH...)
  steps ::

      --->> IN MANAGER_NODE(TARGETNODE) 
           STEPS;;;;;;
               -->> give the sudo privileges to the user(ex: ubuntu) on manager_node
                   ''
                       sudo usermod -aG sudo ubuntu

                    ''
                -->> now now copy the public ssh key from controler _node and paste them into targetnode

                      ...steps for controler node 
                           -> generating sshkeys on controler node 
                             ''
                             ssh-keygen -t rsa -b 4096
                           ''
                           -> now copy the public ssh key 
                           ;;
                            []$ cd ~/.ssh/
                             cat id_rsa.pub
                             ;;
                      ....stepd for managernode
                           ''
                           cd ~/.ssh/
                           vi authorized_keys
                           ........PASTE HERE........


                           --> now restart ssh
                               ''
                                sudo systemctl restart ssh
                                ''







  
    ----IN CONTROLER NODE ----
        --> install ansible in the controler node 
        
        ''
        sudo apt update
        sudo apt upgrade -y
        sudo apt install ansible -y
        ansible --version
        ''

        ---> copy public ssh keys into manager(target_node)

         ''
             ssh-copy-id ansible-user@192.168.1.100

          ''
      output::
      ''

            
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ubuntu/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed

/usr/bin/ssh-copy-id: WARNING: All keys were skipped because they already exist on the remote system.
                (if you think this is a mistake, you may want to use -f option)

''

   ---->> now connect to the targetnode (manager_node ) from controler_node with using password

           ''
              ssh ubuntu@<target_node public_ip>
        ''





        

        
        
