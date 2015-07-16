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

关于尾递归
===
假定某个函数，它会处理一些I/O操作（比如解析某个日志文件），然后定期执行，另外你需要确保这个日志文件只能同时被一个函数解析（注：试想解析过程很长，周期间隔很短）。此时setInterval将不再是最佳方案。因为setInterval中的函数并不会判断是否上一个周期中的函数已经执行完毕，也就无法确保日志文件在同一时间只被一个函数处理。

假定现在有一个异步函数叫async，它会进行一些I/O操作，然后在完成后调用回调函数。我们让它每秒执行一次：
```javascript
var interval = 1000;
setInterval(function() {
	async(function() {
		console.log('async is done!');
	});
});
```
如果现在要求任意两个async函数之间在时间上不能重叠，就应该使用下面的方式：
```
var interval = 1000;
(function schedule() {
	setTimeout(function() {
		async(function() {
			console.log('async is done!');
			schedule();
		});
	}, interval);
})();
```
上面的代码中，我们先声明了函数schedule并立即执行了它。 函数schedule调用setTimeout来让另一个函数（之后称作定时器函数）在一秒后执行。定时器函数会调用async，当async完成I/O操作并回调之后，通过再次调用schedule，会设置一个新的定时器，以此重复。这样我们就能确保不再会同时调用async函数。

与setInterval不同的是：这种方式async将不会在每一秒都能执行“一次”，不过它可以保证你在上一次调用async结束1秒后，重新执行async函数。

