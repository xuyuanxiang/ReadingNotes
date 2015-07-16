# Staff App 员工端App
1. [结构](#structure)
2. [准备](#prepare)
3. [开发](#develop)
4. [测试](#test)
5. [构建](#distribute)

---

# <a id="structure" name="structure">结构</a>
```
staff_app/ 
├── package.json
├── node_modules/
├── bower.json-------------------第三方依赖库声明文件（bower包管理工具）
├── vendor/  --------------------第三方依赖库（由bower下载安装） 
├── config.xml-------------------Phonegap配置文件
├── plugins/ --------------------Phonegap插件
│   ├── angroid.json
│   ├── fetch.json
│   ├── ios.json
├── src/
│   ├── app/ --------------------各模块controller及html模板			
│   ├── common/ 
│   │	 ├── directives/---------Angular指令
│   │	 ├── resources/----------数据交互层
│   │	 └── services/-----------Angular单例服务
│   ├── sass/--------------------CSS预处理工具（最终编译为CSS）
│   │	 ├── animate/------------CSS3动画
│   │	 ├── common/
│   │	 │   ├── global.scss-----全局通用样式
│   │	 │   ├── mixin.scss------Sass函数，代码片段
│   │	 │   ├── reset.scss------全局样式重置，复写。
│   │	 │   └── variables.scss--全局变量
│   │	 ├── component/----------组件样式：Angular封装directive组件的样式
│   │	 ├── theme/--------------主题样式：配色、字体...
│   │	 └── index.scss
│   ├── application.js-----------Angular主模块
│   ├── index.html---------------入口文件
├── test/
│   ├── conf/--------------------测试配置文件
│   ├── unit/--------------------单元测试
│   └── e2e/---------------------端到端测试
├── www/-------------------------最终发布的Web版或打包原生应用
├── platforms/-------------------各原生平台源码（由Phonegap自www构建而得）
│   ├── ios/
│   └── android/
└── gulpfile.js------------------项目构建脚本（Gulp项目构建工具）
```
# <a id="prepare" name="prepare">搭建</a>
## Android 环境搭建
## iOS 环境搭建

# <a id="develop" name="develop">开发</a>


# <a id="test" name="test">测试</a>
## 单元测试
## 端到端测试

# <a id="distribute" name="distribute">构建</a>
## Web版
## Android版
## iOS版