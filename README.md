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

## 2. docker-compose创建启动wordpress/mysql
```
sudo docker-compose -f blog-compose.yml up -d
```

## 3. 测试wordpress
```
http://localhost
```

> P.S. 不使用docker-compose，单独创建wordpress/mysql
```
docker run --name blog-mysql -v /var/lib/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mysql -e MYSQL_DATABASE=blog -e MYSQL_USER=blog -e=MYSQL_PASSWORD=blog -d mysql:5.7 --character-set-server=utf8 --collation-server=utf8_general_ci
docker run --name blog-wordpress --link blog-mysql:mysql -e WORDPRESS_DB_USER=blog -e WORDPRESS_DB_PASSWORD=blog -e WORDPRESS_DB_NAME=blog -p 8080:80 -d wordpress:4.9.1
```
## https版本请参考https分支
