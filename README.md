# JenkinsForMe
https://github.com/jenkinsci/docker/blob/master/README.mddocker 

docker run -d -v C:\Users\rgajul\jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11
docker run -d -v C:\Users\rgajul\jenkins_home:/var/jenkins_home -p 2020:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11

# Docker-Compose
    docker run -d -v jenkins_home:/var/jenkins_home -p 2020:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11
    Or use the below compose file (docker-compose up -d)
    version: '3'
    services:
    jenkins:
    container_name: jenkins
    image: jenkins/jenkins
    ports:
    - "8080:8080"
    volumes:
    - "$PWD/jenkins_home:/var/jenkins_home"
    networks:
    - net
    networks:
    net:

# Get IP Address
    Ipconfig and get the internal ip address of the hostmachine and access
    Ethernet adapter vEthernet (WSL):

    Connection-specific DNS Suffix  . :
    Link-local IPv6 Address . . . . . : fe80::d03b:85a7:66e3:2357%38
    IPv4 Address. . . . . . . . . . . : 172.17.183.241
    Subnet Mask . . . . . . . . . . . : 255.255.255.240
    Default Gateway . . . . . . . . . :

    http://172.17.183.241:8080/

# Copy a script from local to docker container
    Docker cp script.sh <<nameofthecontainer>>:<<fullpath of where the file is exepcted to be copied>>

    java -jar jenkins-cli.jar -s http://localhost:9090/ -auth admin:admin list-jobs

    java -jar jenkins-cli.jar -s http://localhost:9090/ -auth admin:admin install-plugin log-parset:2.1


# Install jenkins on docker on centos

    Get the ip address of virtual box
    Ip a

    Add user jenkins to group docker.
        1. Sudo  usermod -aG docker jenkins 
        
    How much space is docker taking?
        1. Sudo du -sh /var/lib/docker
	
# Docker-compose.yml

    version: '3'
    services:
    jenkins:
    container_name: jenkins
    image: jenkins/jenkins
    ports:
        - "8080:8080"
    volumes:
        - "$PWD/jenkins_home:/var/jenkins_home"
    networks:
        - net
    networks:
    net:

# Give jenkins user the permission to jenkins_home
    sudo chown 1000:1000 jenkins_home -R

# Spin up the container
    Docker-compose up 

# Check logs
    Docker logs -f jenkins

# DNS Name 
    C:\Windows\System32\drivers\etc

# Check cores
    Cat /proc/cpuinfo | grep cores

# Check memory
    Free -h 

  git: 
    container_name: git-server  
    image: 'gitlab/gitlab-ee:latest'  
    hostname: gitlab.example.com  
    ports:  
      - '8090:80'  
    volumes:   
      - '/srv/gitlab/config:/etc/gitlab'  
      - '/srv/gitlab/logs:/var/log/gitlab'  
      - '/srv/gitlab/data:/var/opt/gitlab'  
    networks:  
      - net:  

