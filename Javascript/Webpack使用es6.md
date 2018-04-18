# Webpack使用ES6开发

## 安装loader

```Shell
npm install babel-loader babel-core babel-preset-es2015 --save
```

## 配置`webpack.config.js`

```javascript
{
	test: /\.js$/,
	use: [
		{
			loader: 'babel-loader',
			query: {
				presets: ['es2015']
			}
		}
	]
}
```

