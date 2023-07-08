# 1. Configure Syslog Forwarding
## 1.1. Verify Syslog/Rsyslog installation and version on the host
### 1.1.1. RHEL-based Systems (CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ rpm -qa syslog
$ rpm -qa rsyslog
```
### 1.1.2. Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ apt list | grep -i "installed" | grep -i "syslog"
$ apt list | grep -i "installed" | grep -i "rsyslog"
```
### 1.1.3. Solaris
```
$ pkginfo | grep -i "syslog"
$ pkginfo | grep -i "rsyslog"
```
### 1.1.4. AIX
```
$ lslpp -l | grep -i "syslog"
$ lslpp -l | grep -i "rsyslog"
```
or
```
$ rpm -qa syslog
$ rpm -qa rsyslog
```

---
## 1.2. Install Rsyslog on the host
### 1.2.1. RHEL-based Systems (CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ sudo yum install -y rsyslog
# yum install -y rsyslog
```
or
```
$ sudo dnf install -y rsyslog
# dnf install -y rsyslog
```
### 1.2.2. Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ sudo apt install -y rsyslog
# apt install -y rsyslog
```
### 1.2.3. Solaris
```
# pkg install system/rsyslog
```

---
## 1.3. Enable and Start Syslog/Rsyslog Service
### 1.3.1. RHEL-based Systems / Debian-based Systems
#### SystemD
```
$ sudo systemctl enable --now syslog.service
# systemctl enable --now syslog.service
```
```
$ sudo systemctl enable --now rsyslog.service
# systemctl enable --now rsyslog.service
```
#### SysVInit
```
$ sudo service syslog start
# service syslog start
```
```
$ sudo service rsyslog start
# service rsyslog start
```
### 1.3.2. Solaris
```
# svcadm enable svc:/system/system-log:syslog
# svcadm refresh svc:/system/system-log:syslog
```
```
# svcadm enable svc:/system/system-log:rsyslog
# svcadm refresh svc:/system/system-log:rsyslog
```
> **Note** : You may have to disable ```system-log:default``` before enabling rsyslog
```
# svcadm disable svc:/system/system-log:default
```

### 1.3.3. AIX
```
# startsrc -s syslogd
# startsrc -s rsyslogd
```

---
## 1.4. Configure syslog forwarding on the host
### 1.4.1. Syslog / Rsyslog v7.x and below
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

##### - Example
```
*.* @@192.168.100.10:514
```

### 1.4.2. Rsyslog v8.x and above
#### Edit the ```/etc/rsyslog.conf``` configuration file as follows,
```
$ sudo vi /etc/rsyslog.conf
# vi /etc/rsyslog.conf
```

#### Append the following configuration to the file
```
*.* action(type="omfwd" target="<Log_Collector_IP>" port="514" protocol="tcp")
```

##### - Example
```
*.* action(type="omfwd" target="192.168.100.10" port="514" protocol="tcp")
```

---
## 1.5. Restart Syslog/Rsyslog Service
### 1.5.1. RHEL-based Systems / Debian-based Systems
#### SystemD
```
$ sudo systemctl restart syslog.service
# systemctl restart syslog.service
```
```
$ sudo systemctl restart rsyslog.service
# systemctl restart rsyslog.service
```
#### SysVInit
```
$ sudo service syslog restart
# service syslog restart
```
```
$ sudo service rsyslog restart
# service rsyslog restart
```

### 1.5.2. Solaris
```
# svcadm restart system/system-log:syslog
# svcadm restart system/system-log:rsyslog
```

### 1.5.3. AIX
```
# refresh -s syslogd
# refresh -s rsyslogd
```
---
