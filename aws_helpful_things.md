
## scp copy in aws 
- only file :- scp -i r_login.pem  artifactory-oss-6.7.2.tar.gz  ec2-user@34.222.132.1:/home/ec2-user 
- for folder :- scp -ri r_login.pem  artifactory-oss-6.7.2.tar.gz  ec2-user@34.222.132.1:/home/ec2-user

how to have ssh connectivity between two aws instances 

        login to first server to   
              - ssh-keygen
              - ssh copy-id username@other_machine_id as we dont know ec2-user password we should manually go to .ssh folder copy id_rsa.pub
               content and then patse the entire thing in other machines authorized_keys file present in .ssh
              - then you can try ssh second_machines_ip
              
## mounting EBS to ec2 instance 
    1  ls
    2  clear
    3  yum update
    4  lsblk
    5  cd /
    6  mkdir /myebs
    7  ls
    8  mkfs -t ext4 /dev/xvdb
    9  mount /dev/xvdb /myebs
    10  cd /myebs/
    11  lsblk
    12  history
