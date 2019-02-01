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
 
 - 
