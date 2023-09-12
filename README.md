## How to Install XWiki on CentOS 7

#### 1. Install Java
```sh
sudo yum install java-11-openjdk unzip wget curl -y 
```
```sh
sudo java --version
```
Result : 
```sh
openjdk 11.0.20 2023-07-18 LTS
OpenJDK Runtime Environment (Red_Hat-11.0.20.0.8-1.el7_9) (build 11.0.20+8-LTS)
OpenJDK 64-Bit Server VM (Red_Hat-11.0.20.0.8-1.el7_9) (build 11.0.20+8-LTS, mixed mode, sharing)

```


#### 2. Download Tomcat 8

##### First, Add tomcat user
```sh
sudo groupadd tomcat
sudo useradd  -g tomcat -d /opt/tomcat tomcat
```

```sh
su - tomcat
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.13/bin/apache-tomcat-10.1.13.zip
unzip apache-tomcat-10.1.13.zip
mv apache-tomcat-10.1.13 tomcat
chmod +x tomcat/bin/*.sh
exit
```

