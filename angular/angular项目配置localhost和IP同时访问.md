#### angular 项目配置 localhost 和 IP 同时访问

1、项目中找到此文件“node_modules/webpack-dev-server/lib/Server.js”，按照下图修改：

![](assets/image-20201023112034120.png)

二、修改配置文件package.json，见下图：

![](assets/1137423-20191016142913976-1077010777.png)

三、npm start运行项目，就可以访问项目；

​		通过localhost:4200或者本机IP:4200