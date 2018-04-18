# 阿里云服务器(Linux)搭建Web服务器

## 使用SSH登录服务器

```shell
ssh root@ip-address
```

> 如果出现以下错误,输入 yes并回车

```
The authenticity of host 'ip-address' can't be established.
RSA key fingerprint is SHA256:pViPeyjiOZxH2/7+q5XWPxy0xbgyr7TkBUi5nbSbvfg.
Are you sure you want to continue connecting (yes/no)? 
```

>  输入登录密码



## 一键安装LNMP

文档: https://lnmp.org/install.html

## 创建虚拟主机

文档: https://lnmp.org/faq/lnmp-vhost-add-howto.html

## 安装FTP

```shell
yum install -y vsftpd
```

>  vsftpd命令
>
> ```shell
> /etc/rc.d/init.d/vsftpd start|stop|restart  
> ```



> 阿里ECS云服务器必须吧 `20/21` 规则打开