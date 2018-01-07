# Docker Compose部署Wordpress

## 1. docker安装

### 1.1 更新yum源
```
sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/7/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
```

### 1.2 安装docker
```
sudo yum update -y
sudo yum install -y docker-engine
sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

### 1.3 启动docker
```
sudo systemctl enable docker
sudo systemctl start docker
```
## 2. https/nginx配置

### 2.1 替换证书
将domain.key/chained.pem替换成自己域名的私钥/共钥，可以在Let's Encrypt申请免费的证书

### 2.2. 修改nginx
替换nginx.conf中wanghongmeng.com为自己域名，其他配置可自行调整

## 3. wordpress配置

### 3.1 初始化
登陆```http://xxx.com```初始化wordpress配置

### 3.2. 安装https插件
安装Really Simple SSL插件，启用全站https

### 3.3. 测试访问
访问```https://xxx.com```

