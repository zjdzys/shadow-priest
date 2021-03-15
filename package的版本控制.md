## package.json中依赖版本的定义
package.json是用来做依赖的统一管理。通过dependencies字段进行定义，如下。
```
  "dependencies": {
    "axios": "^0.18.0",
    "axios-mock-adapter": "^1.16.0",
    "babel-polyfill": "^6.26.0",
    "echarts": "^4.2.1",
    "element-ui": "^2.14.1",
    "mavon-editor": "^2.6.17",
    "mockjs": "^1.0.1-beta3",
    "vue": "^2.5.21",
    "vue-cropperjs": "^3.0.0",
    "vue-quill-editor": "^3.0.6",
    "vue-router": "^3.0.1",
    "vue-schart": "^1.0.0",
    "vuedraggable": "^2.17.0",
    "vuex": "^3.1.0"
  },
```
其中版本由三部分组成：X，Y，Z，分别是主要版本，次要版本和补丁版本。
例如：1.2.3，主要版本1，次要版本2，补丁3。
^符号表示保证大版本不变，安装最新的版本，当然还有很多其他种符号，可以另行百度查看。

## 版本不一致问题
假如我们创建了一个新的前端工程，npm install element-ui，在package.json中可以看到对应的版本信息是"element-ui":"^2.4.1"。我将这一份工程共享出去，几天后(element-ui最新的版本更新到了2.4.2，同事拉取我工程中最新的代码执行npm install。他会发现，我们同样都安装了element-ui，但是版本却不尽相同。虽然理论上，他们是兼容的。

## 引入package-lock.json来解决不一致
利用package-lock.json来锁定可变动的版本，通过举例来理解：

- 当package.json中依赖版本是^2.14.1，package-lock.json中该依赖版本是2.14.1，那么重新npm i时候，最终的版本依然是2.14.1

手动修改package.json中依赖版本^2.13.1，package-lock.json(2.14.1)，重新安装后还是2.14.1

手动修改package.json中依赖版本^2.15.1,package-lock.json(2.14.1)，重新安装后是2.15.1并且更新package-lock.json(2.15.1)

手动修改package.json中依赖版本2.13.1,package-lock.json(2.15.1)，重新安装后是2.13.1并且更新package-lock.json(2.13.1)

手动修改package.json中依赖版本^2.14.1,package-lock.json(2.13.1)，重新安装后是2.13.1并且更新package-lock.json(2.15.1)

规律：以package.json中依赖为准，若是存在多个版本可用，则优先以package-lock.json中的版本进行下载。
