# zabbix
zabbix-server for docker-compose  

* 使用容器化环境部署zabbix，部署前提：  
1.需要安装docker  
2.需要安装docker-compose  
# Install docker  
* 安装必要的一些系统工具  
  ```shell  
  yum install -y yum-utils  
  ```  
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
  docker run -d --name zabbix-agent  -v /mnt/zabbix-agent:/etc/zabbix/ -p 10050:10050 zabbix/zabbix-agent:latest  
  检查启动情况：docker logs  
  客户端启动需要挂载配置文件 以上为通用部署方法，k8s部署的配置文件为zabbix_agentd.kuberneter,部署时去掉后缀，修改为.conf格式。  
* 时区问题  
  在docker-compose.yml的zabbix-web-nginx-mysql中的加上  
  ```yaml  
  environment:  
   - PHP_TZ=Asia/Shanghai  
  ```  
* 字体问题  
  只需要把docker-compose中的zabbix-web-nginx-mysql下添加如下挂载即可:  
  ```yaml  
    volumes:
   - ./font:/usr/share/zabbix/assets/fonts:ro  
  ```  
  字体的可以从windows上拷贝至挂载目录中./font目录下，并修改文件名称后重启zabbix即可
