#### Linux上部署Vue/angular网站 由于history模式导致刷新页面出现404报错的解决方式

Linux 上部署如果采用 nginx 进行部署前端站点，当nginx运行的时首页没有问题，链接也没有问题，但在点击刷新后，页面就会显示（404）

原配置：

```
location / {
    root  /home/testhadoop/www/html;
    index index.html index.htm;
}
```

解决方案如下：

##### **方案一：**

使用try_files

语法：`try_files file1 [file2 ... filen] fallback`

```
location / {
    root  /home/testhadoop/www/html;
    index index.html index.htm;
    try_files $uri $uri/ /index.html;
}
```

##### **方案二：**

使用try_files

```
location /{

    root  /home/testhadoop/www/html;
    index  index.html index.htm;

    if (!-e $request_filename) {
        rewrite ^/(.*) /index.html last;
        break;
    }
}
```

##### **方案三：**

使用error_page （一般不建议用， 404的方式会被第三方劫持）

```
location /{

    root  /home/testhadoop/www/html;
    index  index.html index.htm;

    error_page 404 /index.html;
}
```

原文链接:  [https://www.jianshu.com/p/f7a19f1bafa0](https://www.jianshu.com/p/f7a19f1bafa0)

