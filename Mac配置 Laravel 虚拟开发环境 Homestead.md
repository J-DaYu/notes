# Mac配置 Laravel 虚拟开发环境 Homestead

> Mac 配置 Laravel 虚拟开发环境 Homestead
>
> 可以提供各种PHP开发环境
>
> 官方文档地址 [链接](https://d.laravel-china.org/docs/5.5/homestead "外链") 
>
> 参考文档 [链接]( https://laravel-china.org/topics/491/homestead-2-installation-notes "外链")

*说明: Mac系统版本为 10.12.6* 



[TOC]

## 1. 安装 VirtualBox

官网下载可视化安装包

http://download.virtualbox.org/virtualbox/5.2.0/VirtualBox-5.2.0-118431-OSX.dmg

## 2. 安装 Vagrant 

官网下载可视化安装包

https://releases.hashicorp.com/vagrant/2.0.1/vagrant_2.0.1_x86_64.dmg?_ga=2.181302439.1474511145.1510138166-2070880863.1510138166

## 3. 安装 Homestead Vagrant Box

使用命令行进行安装

```shell
vagrant box add laravel/homestead
```

> **如果出现SSL错误则采用以下方法**
>
> 1. 使用迅雷等工具下载 `virtualbox.box`
>
>    https://vagrantcloud.com/laravel/boxes/homestead/versions/4.0.0/providers/virtualbox.box
>
> 2. `vagrant box add laravel/homestead /path/to/virtualbox.box`

## 4. 安装 Homestead

使用git方式安装

```
git clone https://github.com/laravel/homestead.git Homestead
```

切换到Homestead稳定版本

```
cd Homestead
git checkout v6.1.0
```

创建 `Homesstead.yaml` 文件

```
bash init.sh
```

## 5. 配置 Homestead

修改 `Homestead.ymal ` 配置来配置 Homestead

1. 配置共享文件夹

   > 所有项目的公用根目录
   >
   > ```shell
   > folders:
   > 	- map: ~/Projects
   > 	  to: /home/vagrant/Code
   > ```

2. 配置Nginx站点

   > 一个项目对应一个站点
   >
   > ```shell
   > sites:
   > 	- map: homestead.app
   > 	  to: /home/vagrant/Code/test #站点代码地址必须指向入口文件所在文件夹
   > ```

3. 配置host

   > `192.168.10.10       homestead.app`
   >
   > 注意: IP地址必须是 Homestead.ymal 中的IP 
   >
   > ```
   > ip: "192.168.10.10" // host中的IP为这里对应的IP
   > memory: 2048
   > cpus: 1
   > provider: virtualbox
   > ```

4. 配置数据库

   > ```shell
   > databases:
   > 	- homestead #数据库名称
   > ```

   > 数据库默认账号密码分别是 `homestead`／`secret`

5. 启动 Vagrant Box

   > `vagrant up` 

   > **必须首先 用 ssh-keygen 创建公钥** 
   >
   > `ssh-keygen -t rsa`  使用该命令的默认配置即可

   > **出现重新下载 Vagrant Box 错误时**
   >
   > 需要修改 ~/Homestead/scripts/homestead.rb文件中版本判断
   >
   > 修改
   >
   > `config.vm.box_version = settings["version"] ||= ">= 3.0.0"`
   >
   > 为
   >
   >  `config.vm.box_version = settings["version"] ||= ">= 0"`

6. 修改配置 `Homestead.ymal` 文件后需要重新启动vagrant

   > `vagrant reload`
   >
   > 注意: 如果修改了站点信息必须执行 `vagrant reload —provision`

7. 其它命令

   > 关闭虚拟机 `vagrant halt`
   >
   > 销毁虚拟机 `vagrant destory`
   >
   > SSH登录 `vagrant ssh`

## 6. 注意事项

1. 下载超时(SSL错误)

   ```
   Bringing machine 'homestead-7' up with 'virtualbox' provider...
   ==> homestead-7: Box 'laravel/homestead' could not be found. Attempting to find and install...
       homestead-7: Box Provider: virtualbox
       homestead-7: Box Version: >= 3.0.0
   ==> homestead-7: Loading metadata for box 'laravel/homestead'
       homestead-7: URL: https://vagrantcloud.com/laravel/homestead
   ==> homestead-7: Adding box 'laravel/homestead' (v4.0.0) for provider: virtualbox
       homestead-7: Downloading: https://vagrantcloud.com/laravel/boxes/homestead/versions/4.0.0/providers/virtualbox.box
   ==> homestead-7: Box download is resuming from prior download progress

   An error occurred while downloading the remote file. The error
   message, if any, is reproduced below. Please fix this error and try
   again.

   OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
   ```

   > 使用迅雷下载box文件
   >
   > ```
   > https://vagrantcloud.com/laravel/boxes/homestead/versions/4.0.0/providers/virtualbox.box
   > ```
   >
   > 下载完成后使用 `vagrant box add laravel/homestead /path/to/virtualbox.box` 命令指向下载好的box文件

2. SSH key不存在

   `Check your Homestead.yaml file, the path to your private key does not exist.`

   > 使用 `ssh-keygen -t rsa` 创建SSH公钥

3. 启动 box 时出现重新下载

   `Box 'laravel/homestead' could not be found. Attempting to find and install...`

   > 使用 `vagrant box list` 命令检查 box文件是否存在,
   >
   > 如果存在则修改homestead.db文件中的版本判断

4. 配置完host,且已经启动box但无法访问

   > host中的IP地址必须与Homestead.ymal配置文件中的ip一致