## Installation of httpd
- yum install httpd  -y
- service httpd start
- chkconfig httpd on
- cd /var/www/html/

## Terraform installation in Centos

- SSH into your cloud server
- sudo yum install -y zip unzip (if these are not installed)
- wget https://releases.hashicorp.com/terraform/0.9.8/terraform_0.9.8_linux_amd64.zip
- unzip terraform_0.9.8_linux_amd64.zip
- sudo mv terraform /usr/local/bin/
- Confirm terraform binary is accessible: terraform --version

## Git installation in Centos

- yum update -y
- yum install git -y 
- To confirm: git --version 

## Maven installation in Centos

- java -version (if java and JDK already exists follow below steps else , refer link mentioned at the end)
- cd /usr/local/src
- wget http://www-us.apache.org/dist/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz
- tar -xf apache-maven-3.5.4-bin.tar.gz
- mv apache-maven-3.5.4/ apache-maven/
- cd /etc/profile.d/
- vim maven.sh
- chmod +x maven.sh
- ls
- source /etc/profile.d/maven.sh
- To confirm: mvn --version

   compiler issue in aws instance refer https://forums.aws.amazon.com/thread.jspa?messageID=455613

   refer link for more details https://www.tecmint.com/install-apache-maven-on-centos-7/ 
   
 ## Gradle installation in Centos
 
 - java -version (if java and JDK already exists follow below steps else , refer link mentioned at the end)
 - wget https://services.gradle.org/distributions/gradle-3.4.1-bin.zip 
 - sudo mkdir /opt/gradle
 - sudo unzip -d /opt/gradle gradle-3.4.1-bin.zip
 - export PATH=$PATH:/opt/gradle/gradle-3.4.1/bin
 - To confirm: gradle -v
 
    refer link for more deatails https://www.vultr.com/docs/how-to-install-gradle-on-centos-7  
 
 ## Jenkins installation in Centos
 
 - wget https://updates.jenkins-ci.org/download/war/2.162/jenkins.war 
 - java -jar jenkins.war --httpPort=5000
 
 
 ## Upgrading Centos java from 1.7 to 1.8 in centos
 - sudo yum install java-1.8.0
 - sudo yum remove java-1.7.0-openjdk
 - to Verify: java -version 
   
   refere link for more details https://serverfault.com/questions/664643/how-can-i-upgrade-to-java-1-8-on-an-amazon-linux-server 
   
 ## Installation of Docker in centos
 
- yum update -y 
- sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
- sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
- sudo yum install docker -y
- service docker start 
- service docker status 


      If you face below problem which is same as mentione below the you can refer this link

      https://stackoverflow.com/questions/25183063/docker-on-rhel-6-cgroup-mounting-failing

      Starting cgconfig service: Error: cannot create directory /cgroup/blkio
      /sbin/cgconfigparser; error loading /etc/cgconfig.conf: Cgroup, operation not allowed
      Failed to parse /etc/cgconfig.conf                         [FAILED]

       After doing this you need run all the commands with sudo concatenated to it.

      - To solve this issue we need to add current user to docker group , to do the same follow the below commands 
        sudo groupadd docker
        sudo usermod -aG docker $USER ( got a error while runing docker commands with the current user)
        sudo usermod -aG docker jenkins (got a error while runing docker commands with jenkins user )
        getent group <groupname> (to check the list of users in particular group)
        sudo passwd jenkins to change password of jenkins user
        
      - even after following the above commands if you face any issue in ruuning commands then run below command
        chmod 777 /var/run/docker.sock
        
## Installation of Nginx in centos 
- yum update -y
- yum install nginx
- service nginx start

## Tomcat installation in Centos

- yum install -y tomcat7
- which tomcat7
- service tomcat7 start
- cd /usr/share/tomcat7/
- cd webapps/
- netstat -tulnp ( To check ports is listning ports )
   
   Tomcat8 - sudo yum install tomcat8 tomcat8-webapps
             chkconfig tomcat8 on 
   
## Installation of Ansible in centos

- yum update -y
- sudo pip install ansible

https://medium.com/@khandelwal12nidhi/ansible-setup-on-aws-ec2-instance-d83fac41fcc8

## Installation of Jfrog Artifactory 

- wget https://bintray.com/jfrog/artifactory/download_file?file_path=jfrog-artifactory-oss-6.11.1.zip
- unzip download_file?file_path=jfrog-artifactory-oss-6.11.1.zip 
- you will get artifactory-oss-6.11.1 , goto bin folder inside artifactory-oss-6.11.1 and run ``sh artifactory.sh``
- access through http://hostmachineip:8081/artifactory/



