d# TypeScript学习笔记

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

### 函数类型
使用调用签名（call signature)来描述函数接口：
*`调用签名`类似于定义函数时没有给出函数名只给出参数列表和返回类型。*

	interface SearchFunc {
		(source: string, subString: string): boolean;
	}
	
	var mySearch: SearchFunc;
	mySearch = function(source: string, subString: string) {
		var result = source.search(subString);
		if (result == -1) {
			return false;
		} else {
			return true;
		}
	}
	
函数的参数会被顺序检查，参数名并不需要和interface中所定义的一致。
函数返回number或string时，类型检查器将会给出警告。

### 数组类型

	interface StringArray {
		[index: number]: string;
	}
	
	var myArray: StringArray;
	myArray = ["Bob", "Fred"];
	
`[index: number]`：索引（index）类型支持：string 和 number。

`: string`：通过索引所获取的数组元素的类型

**注意**：有一个严格的限制，数字类型索引的返回值类型必须是字符类型索引返回值类型的子类。

	interface Dictionary {
		[index: string]: string;
		length: number; // ERROR
	}
	
索引类型为string，且索引返回类型为string，则length的返回类型必须是string的子类,
例如：

	class Base {}
	
	class Sub extends Base {}
	
	interface Dictionary {
		[index: string]: Base;
		propertyOOXX: Sub;
	}
	
### 接口与实现类（Class Types）

	interface ClockInterface {
		currentTime: Date;
	}
	
	class Clock implements ClockInterface {
		currentTime: Date;
		setTime(d: Date) {
			this.currentTime = d;
		}
		constructor(h: number, m: number){}
	}


