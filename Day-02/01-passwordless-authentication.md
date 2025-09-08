# How to setup Passwordless Authentication.

### Using Password 
in manager_node  :
- got to the file and un comment "PasswordAuthentication yes" -> 'vi /etc/ssh/sshd_config'
- Go to the file   `vi /etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`
- craeae password -> 'sudo passwd ubuntu'
- keep in remember that password
- ---- in controler_node----
- use this commands
- []$ 'ssh-copy-id ubuntu@publicip-manager_node'
- 
 now it will ask password please provide


  -- now try to access that manager_node by using
  ''
    ssh ubuntu@publicip_of_managernode
    
    ''

  now you can observe that with out using any password we can access our manager_node 


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





        

        
        
