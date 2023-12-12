<img src="../images/c4logo.png">

### Steps:
## 1. Install Java 17
```
sudo yum -y update
```
```
sudo yum -y install wget vim curl unzip 
```
```
sudo yum install java-1.8.0-openjdk.x86_64 -y
```
```
wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.rpm
```
```
sudo yum -y install ./jdk-17_linux-x64_bin.rpm
```
```
java -version
```

## 2. Download the latest nexus. 
You can get the latest download links fo for nexus from [here](https://help.sonatype.com/repomanager3/product-information/download).

```
sudo mkdir /app && cd /app
```
```
sudo wget -O nexus.tar.gz https://download.sonatype.com/nexus/3/latest-unix.tar.gz
```

```
sudo tar -xvf nexus.tar.gz
```

```
sudo mv nexus-3* nexus
```

```
sudo adduser nexus
```

```
sudo chown -R nexus:nexus /app/nexus
```

```
sudo chown -R nexus:nexus /app/sonatype-work
```

```
echo  "run_as_user=\"nexus\"" | sudo tee -a /app/nexus/bin/nexus.rc
```
## 3. Running Nexus as a System Service

```
sudo tee -a /etc/systemd/system/nexus.service<<EOF
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
User=nexus
Group=nexus
ExecStart=/app/nexus/bin/nexus start
ExecStop=/app/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
EOF
```

## 4. Access Nexus UI

visit http://VM_IP_address:8081

Note: Default username is **admin** and You can find the default admin password in **/app/sonatype-work/nexus3/admin.password** file
