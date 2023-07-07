# Configure Syslog Forwarding
## Verify Syslog/Rsyslog installation and version on the host
### RHEL-based Systems (RHEL / CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ rpm -qa syslog
$ rpm -qa rsyslog
```
### Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ apt list | grep -i "installed" | grep -i "syslog"
$ apt list | grep -i "installed" | grep -i "rsyslog"
```
---
## Install Rsyslog on the host
### RHEL-based Systems (RHEL / CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ sudo yum install -y rsyslog
# yum install -y rsyslog
```
or
```
$ sudo dnf install -y rsyslog
# dnf install -y rsyslog
```
### Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ sudo apt install -y rsyslog
# apt install -y rsyslog
```
---
## Enable and Start Rsyslog Service
### RHEL-based Systems (RHEL / CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ sudo systemctl enable --now rsyslog.service
# systemctl enable --now rsyslog.service
```
### Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ sudo systemctl enable --now rsyslog.service
# systemctl enable --now rsyslog.service
```
---
## Configure syslog forwarding on the host
### Syslog / Rsyslog v7.x and below
#### Edit the ```/etc/syslog.conf``` or ```/etc/rsyslog.conf``` configuration file as follows,
```
$ sudo vi /etc/syslog.conf
# vi /etc/syslog.conf
```
```
$ sudo vi /etc/rsyslog.conf
# vi /etc/rsyslog.conf
```

#### Append the following configuration to the file
```
*.* @@<Log_Collector_IP>:514
```

##### Example
```
*.* @@192.168.100.10:514
```

### Rsyslog v8.x and above
#### Edit the ```/etc/rsyslog.conf``` configuration file as follows,
```
$ sudo vi /etc/rsyslog.conf
# vi /etc/rsyslog.conf
```

#### Append the following configuration to the file
```
*.* action(type="omfwd" target="<Log_Collector_IP>" port="514" protocol="tcp")
```

##### Example
```
*.* action(type="omfwd" target="192.168.100.10" port="514" protocol="tcp")
```





