## CentOS 7服务器下Nginx安装配置

[超详细虚拟机VMware安装Centos7教程(图文)](https://zhuanlan.zhihu.com/p/145102034)

#### 1. 安装编译工具及库文件

```
$ yum -y install make zlib zlib-devel gcc gcc-c++ libtool  openssl openssl-devel pcre pcre-devel  //PCRE 作用是让 Nginx 支持 Rewrite 功能
```

#### 2. 安装Nginx

 1. 下载Nginx至文件夹/usr/local内

    ```
    $ cd /usr/local/     //进入目标目录
    $ wget http://nginx.org/download/nginx-1.14.2.tar.gz  //下载nginx,选择稳定版本
    ```

2. 解压缩文件包

   ```
   tar zxvf nginx-1.14.2.tar.gz
   ```
   
3. 进入安装目录，编译安装

   ```
   $ cd nginx-1.14.2
   $ ./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-pcre  --with-http_ssl_module
   $ make
   $ make install
   ```

4. 安装完成后的摘要信息：

   ```
   Configuration summary
     + using system PCRE library
     + using system OpenSSL library
     + using system zlib library
    
     nginx path prefix: "/usr/local/nginx"
     nginx binary file: "/usr/local/nginx/sbin/nginx"
     nginx modules path: "/usr/local/nginx/modules"
     nginx configuration prefix: "/usr/local/nginx/conf"
     nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
     nginx pid file: "/usr/local/nginx/logs/nginx.pid"
     nginx error log file: "/usr/local/nginx/logs/error.log"
     nginx http access log file: "/usr/local/nginx/logs/access.log"
     nginx http client request body temporary files: "client_body_temp"
     nginx http proxy temporary files: "proxy_temp"
     nginx http fastcgi temporary files: "fastcgi_temp"
     nginx http uwsgi temporary files: "uwsgi_temp"
     nginx http scgi temporary files: "scgi_temp"
   ```

   默认安装到/usr/local/nginx目录。

5. 查看Nginx版本

   ```
   $ /usr/local/nginx/sbin/nginx -v
   ```

   输出结果如下：
   nginx version: nginx/1.14.2
   到此，nginx安装完成。

6. 启动、关闭Nginx

   检查配置文件是否正确

   ```
   $ /usr/local/nginx/sbin/nginx -t
   $ /usr/local/nginx/sbin/nginx -V     //可以看到编译选项
   ```

   启动Nginx

   ```
   $ /usr/local/nginx/sbin/nginx     // 启动
   $ /usr/local/nginx/conf/nginx.conf  //配置文件
   ```

   重新载入配置文件

   ```
   $ /usr/local/nginx/sbin/nginx -s reload
   ```

   重启Nginx，不会改变启动时指定的配置文件

   ```
   $ /usr/local/nginx/sbin/nginx -s reopen
   ```

   停止Nginx

   ```
   $ /usr/local/nginx/sbin/nginx -s stop
   ```

   或

   ```
   $ pkill nginx
   ```

#### 3. Nginx配置

具体配置可搜索，这里不做介绍
配置文件nginx.conf,位置
/usr/local/nginx/conf/nginx.conf

#### 4. 防火墙配置

CentOS7默认的防火墙为firewall
开启端口80方法：

```
$ firewall-cmd --zone=public --add-port=80/tcp --permanent  //--permanent永久生效，没有此参数重启后失效
$ firewall-cmd --reload  //重新载入
$ firewall-cmd --zone=public --query-port=80/tcp  //查看
//$ firewall-cmd --permanent --query-port=80/tcp //或者这样查看
$ firewall-cmd --zone=public --remove-port=80/tcp --permanent  //删除端口
```

#### 5. 访问nginx.config 权限不够问题

修改/usr/local/nginx/conf/ 下nginx.conf文件，

```
原值#user  nobody; 修改为  user  root;
```

修改nginx.conf文件之后，使用

```
/usr/local/nginx/sbin/nginx -s reload 
```

命令重新加载配置文件即可。

#### 6. 解决 nginx: [error] invalid PID number "" in "/usr/local/nginx/logs/nginx.pid"

使用/usr/local/nginx/sbin/nginx -s reload 重新读取配置文件出错

解决方法：执行以下代码

```
[root@localhost nginx]/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

参考链接：[https://www.cnblogs.com/crazycode2/p/11185405.html](https://www.cnblogs.com/crazycode2/p/11185405.html)