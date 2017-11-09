# 如何正确运行一个Laravel项目

## 安装好 Homestead 环境

## 克隆项目到 Homestead共享目录中

## 在Homestead.ymal中配置Nginx站点

```Shell
ip: "192.168.10.10"
# other config
sites:
	- map: hostname.app
	  to: /path/to/your/project/index/dir
```

## 在host文件中配置拦截

```
192.168.10.10   hostname.app
```

## 手动创建运行时目录

####storage 创建 `app` `framework` `views`文件夹, 并设置777权限

```shell
cd storage
mkdir app framework views
chmod -R 777 app framework views
```

#### 在 storage/framework中创建 `cache` `sessions` `views`文件夹 并设置777权限

```shell
cd framework
mkdir cache sessions views
chmod -R 777 cache sessions views
```

####在bootstrap中创建 `cache` 文件夹,并设置777权限

```shell
cd bootstrap
mkdir cache
chmod -R 777 cache
```

## 在项目中 使用 `composer update ` 更新依赖

```shell
composer update
```

## 新建 ` .evn` 项目配置文件

把 ` .evn.example` 中的内容复制到 `.evn` 中,并修改为本地相关配置

