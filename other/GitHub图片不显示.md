#### 解决github图片不显示的问题

修改hosts

C:\Windows\System32\drivers\etc\hosts

在文件末尾添加：

```
# GitHub Start 
192.30.253.112    Build software better, together 
192.30.253.119    gist.github.com
151.101.184.133    assets-cdn.github.com
151.101.184.133    raw.githubusercontent.com
151.101.184.133    gist.githubusercontent.com
151.101.184.133    cloud.githubusercontent.com
151.101.184.133    camo.githubusercontent.com
151.101.184.133    avatars0.githubusercontent.com
151.101.184.133    avatars1.githubusercontent.com
151.101.184.133    avatars2.githubusercontent.com
151.101.184.133    avatars3.githubusercontent.com
151.101.184.133    avatars4.githubusercontent.com
151.101.184.133    avatars5.githubusercontent.com
151.101.184.133    avatars6.githubusercontent.com
151.101.184.133    avatars7.githubusercontent.com
151.101.184.133    avatars8.githubusercontent.com

 # GitHub End
```

如何添加以上配置后还不能正常显示，请检查DNS配置问题，俺的DNS配置是

```
首选：8.8.8.8
备用：192.168.1.1
```

原文链接：[https://zhuanlan.zhihu.com/p/107196957