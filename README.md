### 1. 环境搭建

> 以linux下的配置为主，windows环境与linux保持一致

#### 1.1 Linux（CentOS 6.8 64bit）

- 备份：sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOd-Base.repo.backup
- 下载CentOS-Base.repo到/etc/yum.repos.d ：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
- 运行yum makecache生成缓存

#### 1.2 jdk1.7

yum -y install java-1.7.0*

#### 1.3 vsftpd

安装：yum -y install vsftpd

创建虚拟用户：

- 创建ftp文件夹：sudo mkdir ftpfile
- 添加匿名用户：sudo useradd ftpuser -d /ftpfile -s/sbin/nologin
- 修改ftpfile权限：sudo chown -R ftpuser.ftpuser /ftpfile
- 重设ftpuser密码：sudo passwd ftpuser（这里设123456）

配置：

- 进入文件：cd /etc/vsftpd
- 将ftpusert写入：sudo vim chroot_list
- 查看：sudo cat chroot_list
- sudo vim /etc/selinux/config，修改SELINUX=disabled
- （若遇到550拒绝访问，请执行sudo setsebool -P ftp_home_dir 1）
- 修改防火墙：sudo vim /etc/sysconfig/iptables
- 修改配置： sudo wget  http://learning.happymmall.com/vsftpdconfig/vsftpd.conf -O /etc/vsftpd/vsftpd.conf

#### 1.4 Nginx

> windows版：一定要在dos窗口启动，不要直接双击nginx.exe，这样会导致修改配置后重启、停止nginx无效，需要手动关闭任务管理器内的所有nginx进程，再启动才可以

-  下载nginx所需的依赖（包含gcc/zlib/openssl）：sudo yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
-  下载源码包：sudo wget http://nginx.org/download/nginx-1.10.2.tar.gz
-  解压：tar -zxvf nginx-1.10.2.tar.gz
-  进入安装nginx目录：cd nginx-1.10.2
-  执行配置（默认安装在/usr/local/nginx）：sudo ./configure
-  继续执行：sudo make
-  继续执行（安装完成）：sudo make install
-  部分可能用到的命令：
   - 测试配置文件：sudo /usr/local/nginx/sbin/nginx  -t
   - 启动：sudo /usr/local/nginx/sbin/nginx
   - 重启/停止：sudo /usr/local/nginx/sbin/nginx  -s reload/stop
   - 查看进程命令(为了查看nginx进程的PID)：ps -ef | grep nginx
   - 平滑重启：kill -HUP [nginx主进程号（即PID）]
-  修改防火墙


#### 1.5 Mysql 5.1.73

- 安装：sudo yum -y install mysql-server

- 字符集配置：

  - 编辑my.cnf：sudo vim /etc/my.cnf

  - 添加配置，在[mysqld]下添加

    - default-character-set=utf8

      character-set-server=utf8

- 执行：sudo chkconfig mysqld on

- 执行（如果2~5为on就ok）：sudo chkconfig --list mysqld

- 修改防火墙

- windows安装：https://cdn.mysql.com/archives/mysql-5.1/mysql-5.1.73-winx64.msi

