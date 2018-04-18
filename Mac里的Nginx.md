# Mac里的Nginx

路径: `/usr/local/etc/nginx`

##服务器配置	

Nginx 会自动加载 conf.d/*.conf 配置文件

`test.cong` 文件

```
server
{
	listen 80;
	server_name test.com;
	index index.php index.html index.htm;
	root  /Users/lee/Projects/lee.com/bs;
}
```

`host` 文件

```
127.0.0.1	      test.com
```



##常用命令

重启

> `nginx -s reload`