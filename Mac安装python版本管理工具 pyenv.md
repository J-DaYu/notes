# Mac 安装Python版本管理工具pyenv

## 安装`pyenv`

1. 使用 `homebrew` 安装 pyenv

   ```shell
   brew install pyenv
   ```

   > 会自动在 `/User/本地用户/`文件夹下创建 `.pyenv` 文件夹

2. 使用 pyenv 提供的自动安装工具

   ```shell
   curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
   ```

   ​

## 使用不同版本的Python

### 安装

>  使用 `pyenv` 安装 python 3.6.2

```Shell
pyenv install -v 3.6.2
```

> 查看全部可用安装版本列表

```bash
pyenv install --list
```

>  如果在安装python版本时出现zlib 错误则执行

```shell
xcode-select install
```
### 切换

> 切换python全局版本 到3.6.2

```Shell
pyenv global 3.6.2
```

如果切换失败(pyenv切换成功,但是系统python版本未改变)

> 查看全局python版本

```bash
pyenv global
```

> 查看已安装的python版本

```bash
pyenv versions
```



修改.zshrc文件, 在末尾增加如下命令:

```bash
export PYENV_ROOT="${HOME}/.pyenv"
if [ -d "${PYENV_ROOT}" ]; then
export PATH="${PYENV_ROOT}/bin:${PATH}"
eval "$(pyenv init -)"
fi
```

重新打开命令行窗口, 切换版本成功

```shell
python
Python 3.6.2 (default, Apr  8 2018, 10:28:40)
[GCC 4.2.1 Compatible Apple LLVM 9.1.0 (clang-902.0.39.1)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

​

## 常用命令

```bash
# 安装 版本为 version 的python
pyenv install version

# 卸载 版本为 version 的python
pyenv install version

# 查看当前 python
pyenv version

# 查看全部 python
pyenv versions

# 设置或查看全局 python 版本
pyenv global

# 设置或查看本地 python 版本
pyenv local
```



