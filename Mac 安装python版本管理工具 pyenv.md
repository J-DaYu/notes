# Mac 安装Python版本管理工具pyenv

## 安装

1. 使用 `homebrew` 安装 pyenv

   ```shell
   brew install pyenv
   ```

   > 会自动在 `/User/本地用户/`文件夹下创建 `.pyenv` 文件夹

## 安装不同版本的Python

1. 使用 `pyenv` 安装 python 3.6.2

   ```Shell
   pyenv install -v 3.6.2
   ```

   > 查看全部可用安装版本列表
   >
   > ```shell
   > pyenv install --list
   > ```

   如果在安装python版本时出现zlib 错误则执行 

   ```shell
   xcode-select install
   ```

2. 切换python全局版本 到3.6.2

   ```Shell
   pyenv global 3.6.2
   ```

   如果切换失败(pyenv切换成功,但是系统python版本未改变) 

   > 查看全局python版本
   >
   > ```shell
   > pyenv global
   > ```
   >
   > 查看已安装的python版本
   >
   > ```sehll
   > pyenv versions
   > ```

   ​

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
   ```

   ​

## 常用命令

1. pyenv install/uninstall 安装/卸载python
2. pyenv version/versions 查看当前/全部 python
3. pyenv global/local 设置或查看全局/本地 python版本