## How to Install XWiki on CentOS 7

#### 1. Install Java
```sh
sudo yum install java-11-openjdk unzip wget curl nano -y 
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

#### 3. Create SystemD unit file
```sh
sudo nano /etc/systemd/system/tomcat.service
```
##### Copy and paste the following code:
```sh
[Unit]
Description=Apache Tomcat 8 Service
After=syslog.target network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_PID=/opt/tomcat/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat/tomcat
Environment=CATALINA_BASE=/opt/tomcat/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -XX:MaxPermSize=192m -server -XX:+UseParallelGC'
Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

ExecStart=/opt/tomcat/tomcat/bin/startup.sh
ExecStop=/bin/kill -15 $MAINPID

[Install]
WantedBy=multi-user.target
```
Save and close the file.
The following commands to reload units and to start the Apache Tomcat service:
```sh
sudo systemctl daemon-reload
sudo systemctl start tomcat
sudo systemctl enable tomcat
```

