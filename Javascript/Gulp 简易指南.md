# Gulp简易指南

> 使用管道模式, 单文件编译

## 全局安装gulp

```Shell
npm install gulp -g
```



## 项目中安装依赖

```shell
npm install gulp --save-dev
```



## 项目根目录下创建 `gulpfile.js`

```javascript
var gulp = require('gulp');

gulp.task('default', function(){
  // 一些默认的任务执行代码
});
```



## 编译

```Shell
gulp
```



## 常用插件

### `less` 

`npm install gulp-less gulp-minify-css --save-dev`

```Javascript
var gulp = require('gulp');
var less = require('gulp-less');

gulp.task('less', function(){
  gulp.src('./src/*.less')			// 读取源文件
  	.pipe(less()) 					// 使用less插件编译
  	.pipe(gulp.dest('./build/')); 	// 默认按照源文件的名称生成 .css 到目标文件夹
});
```

###压缩CSS `gulp-minify-css`

`npm install gulp-minify-css --save-dev`

```javascript
var gulp = require('gulp');
var minify = require('gulp-minify-css');

gulp.task('minify', function(){
  gulp.src('./src/*.css')			// 读取源文件
	.pipe(minify()) 				// 使用minify插件压缩
  	.pipe(gulp.dest('./build/')); 	// 默认按照源文件的名称生成 .css 到目标文件夹
});
```

###压缩图片`gulp-imagemin`

`npm install gulp-imagemin --save-dev`

```javascript
var gulp = require('gulp');
var imgminfy = require('gulp-imagemin');

gulp.task('image',function(){
  gulp.src('./src/image/*')
    .pipe(imgminfy({progressive: true}))
    .pipe(gulp.dest('assets/image'))
})
```

