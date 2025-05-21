# Oktopus_Use
Oktopus Use manual



sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
#如果网速慢：可以尝试  先翻墙下载：curl-L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-Linux-x86_64 -o docker-compose
#然后复制到服务器上面；

wget https://github.com/OktopUSP/oktopus/archive/refs/tags/v1.24.4.tar.gz && tar -xvf v1.24.4.tar.gz && cd oktopus-1.24.4/deploy/compose 

修改docker-compose.yaml ==> docker-compose_1.24.4.yaml （docker tag：8e0a8e5）为里边的内容

sudo  COMPOSE_PROFILES=nats,controller,cwmp,mqtt,stomp,ws,adapter,frontend,portainer docker-compose up -d

  这一步如果网速慢，需要修改源
      sudo mkdir -p /etc/docker
          sudo tee /etc/docker/daemon.json <<EOF
          {
              "registry-mirrors": [
                  "https://docker.1ms.run",
                  "https://docker.xuanyuan.me"
              ]
          }
          EOF
          sudo systemctl daemon-reload
          sudo systemctl restart docker

      sudo systemctl daemon-reload
      sudo systemctl restart docker






检查监听端口
# 检查TCP端口(如8088)
ss -tulnp | grep ':8088'

# 检查UDP端口
ss -u -a | grep ':8088'

检查iptables规则
sudo iptables -L -n | grep '8088'

sudo firewall-cmd --list-ports | grep '8088'
sudo firewall-cmd --list-all | grep '8088'

测试联通性：
telnet 127.0.0.1 8088
# 或
nc -zv 127.0.0.1 8088


sudo ufw status
# 或更详细的状态
sudo ufw status verbose


sudo ufw logging on  # 开启日志
sudo tail -f /var/log/ufw.log  # 查看实时日志