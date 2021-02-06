> 整理自珠峰培训

## 1 与WEBPACK 相类似的工具还有哪些？谈谈为什么选择或放弃使用用WEBPACK？

![image-20201231130529340](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231130529340.png)

![image-20201231131433748](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231131433748.png)



![image-20201231131300574](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231131300574.png)

![image-20201231131334446](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231131334446.png)

![image-20201231131735993](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231131735993.png)

![image-20201231132052814](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231132052814.png)

![image-20201231132655900](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231132655900.png)

## 2 如何调试WEBPACK?

![image-20201231133222059](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231133222059.png)

## 3 LOADER 与PLUGIN 有什么不同？

![image-20201231133548480](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231133548480.png)

## 4 WEBPACK 的构建流程是什么？

![image-20201231133734019](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231133734019.png)

![image-20201231133808669](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231133808669.png)



## 5 有哪些常见的Loader 和 Plugin？他们是解决什么问题的？

![image-20201231150949065](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231150949065.png)

![image-20201231151141615](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20201231151141615.png)

add-asset-html-cdn-webpack-plugin // 全局引入 CDN 资源

```javascript
module.exports={
	externals: {
	"jQuery":"$" // 外部变量,不需要打包
	}
}
```



## 6 SOURCE MAP 是什么？生产环境怎么用?

![image-20210101021808871](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101021808871.png)

![image-20210101022143317](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101022143317.png)

![image-20210101022435499](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101022435499.png)



## 7  如何利用WEBPACK 优化前端性能?

### 压缩JS  TerserPlugin

### 压缩 CSS OptimizeCssAssetsWebpackPlugin

![image-20210101022642316](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101022642316.png)



### 压缩图片 file-loader image-webpack-loader

![image-20210101022828496](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101022828496.png)

### 清除无用的CSS purgecss-webpack-plugin

![image-20210101022937842](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101022937842.png)

![image-20210101023004833](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101023004833.png)

### Tree Shaking

![image-20210101023136289](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101023136289.png)

```javascript
// package.json
{
  //"sideEffects": false
  "sideEffects": ["**/*.css"]
}
```

### scope hoisting

![image-20210101023226584](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101023226584.png)

### 代码分隔

![image-20210101023328879](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101023328879.png)

![image-20210101155451178](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101155451178.png)

![image-20210101160428469](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101160428469.png)

![image-20210101160514801](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101160514801.png)

![image-20210101160853660](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101160853660.png)

![image-20210101161221958](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101161221958.png)

![image-20210101161448282](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101161448282.png)

![image-20210101161601719](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101161601719.png)

![image-20210101161705229](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101161705229.png)

![image-20210101161804760](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101161804760.png)

![image-20210101161924731](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101161924731.png)

![image-20210101162402282](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101162402282.png)

![image-20210101162517029](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101162517029.png)

![image-20210101162615760](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101162615760.png)



![image-20210101162654129](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101162654129.png)

![image-20210101163013399](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101163013399.png)

![image-20210101162933630](Webpack%E9%9D%A2%E8%AF%95%E6%95%B4%E7%90%86.assets/image-20210101162933630.png)

maxAsyncRequests: 通过异步引入模块(如 import() ) 的最大拆分文件数

maxInitialRequests: 每个入口文件最大拆分文件数

## 8 暴露全局变量

1. 直接使用CDN的方式

  add-asset-html-cdn-webpack-plugin // 全局引入 CDN 资源
  ```javascript
  module.exports={
    externals: {
    "jQuery":"$" // 外部变量,不需要打包
    }
  }
  ```
2. providePlugin

3. 暴露全局下 expose-loader

   ```
   module.exports = {
   	module:{
   		rules:[
   			{
   				test:require.reslove('jquery'),
   				use:{
   					loader: 'expose-loader',
   					options:'$$'
   				}
   			}
   		]
   	}
   }
   ```

   

4. 

## 9 ESLINT

需要安装的包 eslint eslint-loader

```javascript
npm i eslint eslint-loader -D

module.exports = {
	module:{
		rules:[
			{
				test:/\.js$/,
				use:'es-loader',
				enforce: 'pre'
			}
		]
	}
}
```























