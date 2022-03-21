# Part 2 - Cài đặt Docker trên Ubuntu 20.04 (LTS)

## 1. Thiết lập repository
1. Update hệ thống
    ```
    apt-get update -y
    ```
2. Cài đặt các gói cho phép `apt` sử dụng repo qua HTTPS:
    ```
    apt-get install -y \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    ```

3. Thêm Docker GPG key:
    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    ```

4. Thiết lập repo stable"
    ```
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null    
    ```

## 2. Cài đặt Docker engine
Cài đặt Docker:
```
apt-get update -y

apt-get install docker.io -y
```

Kiểm tra phiên bản Docker:
```
docker --version
```
Kết quả
```
Docker version 20.10.7, build 20.10.7-0ubuntu5~20.04.2
```

Kiểm tra thông tin Docker engine:
```
docker info
```
Kết quả:
```
Client:
 Context:    default
 Debug Mode: false

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 20.10.7
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version:
 runc version:
 init version:
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.4.0-84-generic
 Operating System: Ubuntu 20.04.3 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 3.843GiB
 Name: haidd-u20-docker-68
 ID: AGUR:OG3Z:K3LE:K23A:EOWK:MP7V:TRDG:4D5H:C7YF:4Y2C:2KZK:PMZM
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

# Tham khảo
- https://docs.docker.com/engine/install/

