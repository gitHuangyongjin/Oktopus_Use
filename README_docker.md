# Docker加速和安装篇

### 配置Docker镜像加速器（适用于国内用户）
sudo tee /etc/docker/daemon.json <<EOF
{
    "registry-mirrors": [
        "https://docker.1ms.run",
        "https://docker.xuanyuan.me"
    ]
}
EOF


### 卸载旧版本Docker及相关组件
sudo apt-get remove docker docker-engine docker.io containerd runc

### 安装Docker依赖项
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

### 添加Docker官方GPG密钥
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

### 添加Docker官方APT源
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

### 安装Docker引擎
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

### 备用方案

### 一键安装脚本方式（备用方案）
curl -fsSL get.docker.com -o get-docker.sh && sudo sh get-docker.sh

### 使用阿里云镜像源安装（国内推荐）
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

### 系统安全更新（解决某些依赖问题）
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu $(lsb_release -cs)-security main"
sudo apt update

### 强制降级libseccomp2解决兼容性问题
sudo apt-get install libseccomp2=2.5.1-1ubuntu1~16.04.2 -y --allow-downgrades

### 验证Docker安装
docker --version

### 重启Docker服务使配置生效
sudo systemctl restart docker