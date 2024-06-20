# JenkinsForMe
https://github.com/jenkinsci/docker/blob/master/README.mddocker 
Ensure the environment variable is correctly set before running docker commands DOCKER_CERT_PATH=C:\Users\<user>\.docker\machine\certs
docker run -d -v C:\Users\rgajul\jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11
docker run -d -v C:\Users\rgajul\jenkins_home:/var/jenkins_home -p 2020:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11

# Docker-Compose
docker run -d -v jenkins_home:/var/jenkins_home -p 2020:8080 -p 50000:50000 jenkins/jenkins:lts-jdk11
Or use the below compose file (docker-compose up -d)
```yml
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
```

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
```yml
version: '3'
services:
  jenkins: null
  container_name: jenkins
  image: jenkins/jenkins
  ports:
    - '8080:8080'
  volumes:
    - '$PWD/jenkins_home:/var/jenkins_home'
  networks:
    - net
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
      - net: null
```
    

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
Cron jobs in Jenkins allow you to schedule tasks to run at specified intervals. Jenkins uses a syntax similar to Unix cron syntax but with a few differences. Here’s a breakdown of the syntax and how to use it in Jenkins:

### Cron Job Syntax Overview

A cron expression in Jenkins consists of five fields separated by spaces:

```
* * * * *
│ │ │ │ │
│ │ │ │ │
│ │ │ │ └─── Day of the week (0 - 7) (Sunday is both 0 and 7)
│ │ │ └──────── Month (1 - 12)
│ │ └───────────── Day of the month (1 - 31)
│ └────────────────── Hour (0 - 23)
└─────────────────────── Minute (0 - 59)
```

### Field Values

- **Minute**: `0-59`
- **Hour**: `0-23`
- **Day of the month**: `1-31`
- **Month**: `1-12`
- **Day of the week**: `0-7` (where both 0 and 7 represent Sunday)

### Special Characters

- `*` : All values
- `,` : Separate items of a list
- `-` : Range of values
- `/` : Step values

### Examples

1. **Every Minute**: 
    ```
    * * * * *
    ```
    Runs every minute.

2. **Every Hour**:
    ```
    H * * * *
    ```
    Runs at a random minute every hour (the `H` is a Jenkins-specific feature that spreads the load).

3. **Daily at Midnight**:
    ```
    H 0 * * *
    ```
    Runs at a random minute of the hour 0 (midnight) every day.

4. **Every Sunday at 2:30 AM**:
    ```
    30 2 * * 0
    ```
    Runs at 2:30 AM every Sunday.

5. **Every Weekday at Noon**:
    ```
    H 12 * * 1-5
    ```
    Runs at a random minute of the hour 12 PM, Monday through Friday.

6. **Monthly on the 1st at Midnight**:
    ```
    H 0 1 * *
    ```
    Runs at a random minute of the hour 0 on the 1st of every month.

7. **Every 15 Minutes**:
    ```
    H/15 * * * *
    ```
    Runs every 15 minutes.

8. **Every 5 Minutes During Working Hours (8 AM - 6 PM) on Weekdays**:
    ```
    H/5 8-18 * * 1-5
    ```
    Runs every 5 minutes between 8 AM and 6 PM, Monday through Friday.

### Notes

- **H (Hash)**: The `H` character is used in Jenkins to distribute the load evenly by choosing different values for each project (e.g., if you use `H` in the minute field, Jenkins will pick a different minute for each project). This helps to avoid all jobs running at the same time.
- **Empty Field**: Leaving a field empty is not allowed in Jenkins. Use `*` or other appropriate values.

### Usage in Jenkins

1. Go to your Jenkins job configuration page.
2. In the "Build Triggers" section, select "Build periodically."
3. Enter your cron expression in the "Schedule" field.

By using these cron expressions, you can effectively schedule your Jenkins jobs to run at specific times or intervals as required.
