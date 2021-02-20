# zabbix
zabbix-server for docker-compose  

* 使用容器化环境部署zabbix，部署前提：  
1.需要安装docker  
2.需要安装docker-compose  
# Install docker  
* 安装必要的一些系统工具  
  yum install -y yum-utils  
* 添加软件源信息  
  yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo  
* 安装Docker  
  yum install docker-ce docker-ce-cli containerd.io  
* 开启Docker服务  
  systemctl start docker  
# Install docker-compose  
  yum install -y docker-compose.noarch  
# Deployment zabbix  
* 部署zabbix-server
  docker-compose up -d  
* 访问web页面  
  url: localhost:8081  
  user: Admin / passwd: zabbix  
# Agent  
* 创建映射目录
  mkdir zabbix-agent & cd zabbix-agent  
  copy 配置.conf文件到这个目录  
* 启动agent端镜像  
  docker run -d --name zabbix-agent  -v /root/jianshu/zabbix-docker/zabbix-agent:/etc/zabbix/ -p 10050:10050 zabbix/zabbix-agent:latest  
  检查启动情况：docker logs  
