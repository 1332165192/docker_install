# docker_install
docker安装脚本
~~~
#查看内核
uname -r
#查看已安装的CentOS的版本信息
cat /etc/redhat-release
#yum安装gcc
yum -y install gcc
yum -y install gcc-c++
#卸载旧版本docker
sudo yum remove docker \
	docker-client \
	docker-client-latest \
	docker-common \
	docker-latest \
	docker-latest-logrotate \
	docker-logrotate \
	docker-engine
#安装所需要的软件包
sudo yum install -y yum-utils \ 
	device-mapper-persistent-data \ 
	lvm2
#设置stable镜像仓库
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
#更新yum软件包索引
yum makecache fast
#安装Docker
yum -y install docker-ce
#启动Docker
systemctl start docker
#验证docker是否安装成功
docker version
#卸载Docker
#systemctl stop docke
#yum -y remove docker-ce
#rm -rf /var/lib/docker
#配置阿里云镜像加速
#创建/etc/docker目录
#mkdir -pv /etc/docker
vi daemon.json
{
  "registry-mirrors": ["自己的阿里云镜像加速地址"],
  "live-restore": true,
  "log-driver":"json-file",
  "log-opts": {"max-size":"500m", "max-file":"3"}
}
#重启docker服务
systemctl daemon-reload
systemctl restart docker
~~~
