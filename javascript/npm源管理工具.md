# npm源管理工具- NRM

## 安装

``` shell
npm install -g nrm
```
## 使用

> 查看可用源

```shell
nrm ls
```
> 切换源

```shell
nrm use taobao
```
> 手动添加一个可用源

```shell
nrm add registry-name url
```
## 实践 - 本地搭建npm源服务器

> 本地搭建npm私有源
>
> 参考: https://www.cnblogs.com/zycbloger/p/sinopia.html

### 安装 `sinopia`

> `sinopia` 依赖 python2.7 ,本地python环境必须切换为2.7

```bash
npm install sinopia -g
```
### 启动 sinopia 服务器

```
sinopia
```
>  浏览器打开 `http://localhost:4873/`
>
> 如果能显示源玩站则成功

### 本地添加私有源地址

```shell
# 添加私有源
nrm add local http://localhost:4873/
# 切换本地npm源
nrm use local
# 添加源用户
npm adduser --registry http://localhost:4873
Username: yu
Password: 123456
Email: 296241072@qq.com
```
> 发布npm包
>
> ```bash
> npm publish
> ```

### sinopia 配置

```yaml
#
# This is the default config file. It allows all users to do anything,
# so don't use it on production systems.
#
# Look here for more config file examples:
# https://github.com/rlidwka/sinopia/tree/master/conf
#

# path to a directory with all packages
# npm包存放的路径
storage: ./storage    

auth:
  htpasswd:
    file: ./htpasswd
    # Maximum amount of users allowed to register, defaults to "+inf".
    # You can set this to -1 to disable registration.
    # max_users: 1000
    # 默认为1000，改为-1，禁止注册
    max_users: 1000     

# a list of other known repositories we can talk to
uplinks:
  npmjs:
    url: http://registry.npm.taobao.org/  
    # 默认为npm的官网，由于国情，修改 url 让sinopia使用 淘宝的npm镜像地址

packages:
  '@*/*':
    # scoped packages
    access: $all
    publish: $authenticated

  '*':
    # allow all users (including non-authenticated users) to read and
    # publish all packages
    #
    # you can specify usernames/groupnames (depending on your auth plugin)
    # and three keywords: "$all", "$anonymous", "$authenticated"
    access: $all

    # allow all known users to publish packages
    # (anyone can register by default, remember?)
    publish: $authenticated

    # if package is not available locally, proxy requests to 'npmjs' registry
    # 这个去掉的话,sinopia 将不去下载依赖包, 如果只是要放自己资源仓库的话就去掉      
    # proxy: npmjs   
    # 

# log settings
logs:
  - {type: stdout, format: pretty, level: http}
  #- {type: file, path: sinopia.log, level: info}

# you can specify listen address (or simply a port) 
# 默认没有，只能在本机访问，添加后可以通过外网访问。
listen: 0.0.0.0:4873  
```

​