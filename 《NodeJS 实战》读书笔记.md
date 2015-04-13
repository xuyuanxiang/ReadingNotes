Node如何解析引用模块路径
===

## 核心模块

> 在Node二进制发行包里有一张核心模块的清单。如果需要引用其中一个模块，使用require()函数直接引用。

## 使用完整路径或相对路径引用模块

> 如果模块的引用路径是以`./`或者`/`开头，Node将以文件形式加载这个模块。如果加载不成功，Node尝试以字典表形式加载这个模块。

##文件形式加载
如果文件存在，Node以Javascript文本形式加载这个文件。如果这个文件不存在，Node尝试在当前路径下将这个文件名结尾添加`.js`加载。如果还是不成功，Node将尝试在这个文件名结尾添加`.node`并以二进制的附件组件（add-on）形式加载。

##目录形式加载
如果追加的`/package.json`是一个文件，将加载其定义并查找主体部分，尝试以文件形式加载。如果不成功，将添加`/index`再去加载。

NPM命令
===
##检索
```bash
node ls [过滤条件]
```
列表显示所有已安装的Node包：
```bash
npm ls installed
```

列表显示所有的稳定版发行包：
```bash
npm ls stable
```

使用版本号查询，版本号前需要添加`@`符号：
```bash
npm ls @1.0
```
## 安装
```bash
npm install package[@过滤条件]
```
安装最新版本的Node包：
```bash
npm install package
```
安装指定版本的包：
```bash
npm install package@version
```

## 删除
```bash
npm rm package
```

##查看
```bash
npm view package
```

