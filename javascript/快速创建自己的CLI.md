# 如何快速创建自己的CLI

> CLI，全称是command-line interface，也就是命令行交互接口。
>
> 使用 `git-clone ` 从已经存在的模板快速创建项目
>
> 使用到的依赖包
>
> `git-clone` `commander` `chalk` `shelljs`



## npm 初始化项目

```bash
mkdir my-cli
cd my-cli
npm init
# 安装依赖
npm install git-clone commander chalk shelljs --save
```



## 配置 `package.json`

```javascript
"bin": {
  "my-cli": "./index.js"
}
```



## 创建node可执行文件 `index.js`

``` javascript
#!/usr/bin/env node
// 文件处理
const fs = require('fs')
// git仓库克隆
const clone = require('git-clone')
// 命令行命令处理
const program = require('commander')
// 命令执行
const shell = require('shelljs')
// 命令行颜色样式
const chalk = require('chalk')
// 模板所在仓库地址
const GIT_URL = 'http://xxx/my-cli-template.git'

// cli基础信息配置, 在用户输入 my-cli -h 后显示的信息
program
  .version('1.0.0', '-v, --version')
  .description('我的项目开发工程脚手架')
  .usage('<command> [options]')

// init 命令
program
  .command('init [component]')
  .action(function(component) {
    if (component) {
      // 使用例子: my-cli mycomponent
      console.log(chalk.blue('√ 命令初始化中...'))
      console.log(chalk.blue(`√ 正在创建组件: ${component}`))
      let pwd = shell.pwd()
      let path = pwd  + '/' + component
      // 判断文件夹是否已经存在, 防止覆盖原有文件夹
      fs.exists(path, function (exists) {
        if (exists) {
          console.log(chalk.red(`× 已经存在名称为 ${chalk.yellow(component)} 的文件夹`))
        } else {
          console.log(chalk.blue(`√ 正在拉取模板代码，下载位置：${pwd}/${component}/ ...`))
          // 从模板仓库拉取模板文件
          clone(GIT_URL, pwd + `/${component}`, null, function() {
              console.log(chalk.blue(`√ 模板代码拉取成功`))
              // 移除 .git 版本控制文件
              shell.rm('-rf', path + `/.git`)
              console.log(chalk.hex('#008b8b').bold('√ 模板工程创建成功'))
              // 自动执行安装和启动测试服务
              console.log(chalk.blue(`√ 正在为您安装代码依赖...`))
              shell.exec(`cd ${path} && npm install && npm run dev`)
          })
        }
      })
    } else {
      log.error('请输入组件名称')
    }
  })

// 用户输入未知命令时提示
program
  .arguments('<command>')
  .action((cmd) => {
    program.outputHelp()
    console.log(`  ` + chalk.red(`Unknown command ${chalk.yellow(cmd)}.`))
    console.log()
  })

program.parse(process.argv)
// 用户只输入 my-cli 命令式显示帮助信息
if (!process.argv.slice(2).length) {
  program.outputHelp()
}
```



## 全局安装

```bash
npm install -g
```

> 在 `my-cli` 项目根目录下



## 使用

```bash
my-cli init myproject
```

