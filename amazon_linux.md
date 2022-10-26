### install java 8 
```
yum install java-1.8.0-openjdk
```
### install maven 
- wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
- sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
- yum install -y apache-maven
- mvn –version

### install nexus 

- apt-get install wget ( install if you dont have wget )
- java -version ( make sure java is installed which should be java 8 or higher version )
- wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
- tar -xvf latest-unix.tar.gz
- cd nexus-3.35.0-02/bin
- ./nexus start ( starts the nexus artifactory )
- ./nexus status ( by this you check the status of nexus artifactory )
- To access this use http://ip_Address:8081 ( by deafault which will be running on 8081)
intial password will be present in /opt/sonatype-work/nexus3/admin.password
