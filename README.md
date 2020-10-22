### 环境搭建

1. Linux（CentOS 6.8 64bit）

   - 备份：sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOd-Base.repo.backup
   - 下载CentOS-Base.repo到/etc/yum.repos.d/ ：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
   - 运行yum makecache生成缓存

2. jdk1.7（linux和win）yum -y install java-1.7.0*

3. vsftpd（linux和win）

   - Linux

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
     - sudo vim /etc/vsftpd/vsftpd.conf 使用env文件下的配置即可（注意前提是要在同一网段）

4. ​

