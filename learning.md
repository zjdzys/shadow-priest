在前后端严格分离的开发模式下，经常会遇到跨域的问题。比如前后端都由本地启动，那么端口必然不一样（造成跨域）。本地启动前端，对接别人的后端服务，那么ip必然不一样（造成跨域）。在跨域场景下，我们的api接口都无法调用成功，那么这里就介绍几种常用的解决办法。

### 1、vue工程配置proxy
在vue.config.js配置中可以设置proxy，如果没有这个配置文件，也可以在`package.json`中找到`vue`字段进行配置，如下。配置完成后，当前工程就会把所有的api接口请求往target域进行发送。你也可以设置不同的映射规则。
```javascript
	"dependencies":{},
	"vue":{
		"publicPath": "/",
		"outputDir": "dist2",
		"devServer": {
		  "proxy": {
			"/": {
			  "target": "http://localhost:18081"
			}
		  }
		}
	}
```
### 2、react工程配置proxy
在工程的`package.json`文件中，可以通过配置方式，实现所有接口转发到配置中ip:port服务去
```javascript
	"proxy":"http://10.190.89.24:18800"
```
### 3、利用nginx做统一代理
下回补充

### 4、后端服务配置允许跨域的属性
下回补充
