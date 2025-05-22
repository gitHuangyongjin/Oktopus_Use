# Oktopus_Use
### Oktopus Use manual

## 1. 安装docker 和 docker-compose
sudo apt-get install docker.io
sudo systemctl start docker

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
#### 如果网速慢：可以尝试  先翻墙下载：
curl-L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-Linux-x86_64 -o docker-compose
然后复制到服务器上面； cp docker-compose /usr/local/bin/docker-compose
也可以直接使用这里的docker-compose

## 2. 安装docker-compose
wget https://github.com/OktopUSP/oktopus/archive/refs/tags/v1.24.4.tar.gz && tar -xvf v1.24.4.tar.gz && cd oktopus-1.24.4/deploy/compose 

## 3. 修改配置文件
修改docker-compose.yaml ==> docker-compose_1.24.4.yaml （docker tag：8e0a8e5）为里边的内容

## 4. 启动
sudo  COMPOSE_PROFILES=nats,controller,cwmp,mqtt,stomp,ws,adapter,frontend,portainer docker-compose up -d

### 关闭服务：
COMPOSE_PROFILES=nats,controller,cwmp,mqtt,stomp,ws,adapter,frontend,portainer docker-compose down

####  这一步如果网速慢，需要修改docker源，复制以下命令可以修改源
sudo mkdir -p /etc/docker
   sudo tee /etc/docker/daemon.json <<EOF
    {
        "registry-mirrors": [
            "https://docker.1ms.run",
            "https://docker.xuanyuan.me"
        ]
    }
    EOF

### 重启docker和daemon
sudo systemctl daemon-reload
sudo systemctl restart docker

### 测试是否docker修改源成功：
sudo docker info | grep -A 2 "Registry Mirrors"