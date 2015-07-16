# TypeScript学习笔记

## Interfaces

### 第一个接口

	function printLabel(labelledObj: {label: string}) {
		console.log(labelledObj.label);
	}
	
	var myObj = {size: 10, label: "Size 10 Object"};
	printLabel(myObj);
	
**类型检查器（type-checker）**检查了对`printLabel`的调用。
`printLabel`函数只接收一个参数，该参数必须是拥有一个名为`label`且类型为string的属性的对象。
在实际调用时，所传递的对象有更多的属性，但编译器只检查是否具备所要求的属性且其数据类型是否正确。

使用**interface**重写这个例子：

	interface LabelledValue {
		label: string;
	}
	
	function printLabel(labelledObj: LabelledValue) {
		console.log(labelledObj.label);
	}
	
	var myObj = {size: 10, label: "Size 10 Object"};
	printLabel(myObj);

接口`LabelledValue`是一个用来描述第一个例子中函数接收参数的要求的名称。
注意，我们并没有像在其他编程语言中一样声明所传递给`printLabel`的对象实现了该接口。
这里仅仅是“形状”匹配，如果我们所传递给函数的对象，复合（接口所定义的）需求清单，那么它就是被允许的。

值得指出的是，类型检查器并不强制要求所需求的属性在对象中的次序，只要对象中具有该属性即可。

### 可选属性

```
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config:SquareConfig):{color:string;area:number} {
    var newSquare = {color: "white", area: 100};
    if (config.color) {
        newSquare.color = config.color;
    }
    if (config.width) {
        newSquare.area = config.width * config.width;
    }

    return newSquare;
}

var mySquare = createSquare({color:"black"});	
```