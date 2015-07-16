# TypeScript学习笔记

## 基本类型

### Boolean

	var isDone: boolean = false;
	
### Number

	var height: number = 6;
	
### String

	var name: string = "bob";
	
### Array

	var list:number[] = [1, 2, 3];
	
or

	var list:Array<number> = [1, 2, 3];
	
### Enum

**默认**从0开始:

	enum Color {Red, Green, Blue};
	var c: Color = Color.Green;

---	

设置为从1开始：

	enum Color {Red = 1, Green, Blue};
	var c: Color = Color.Green;

---
	
或者手动设置所有值：

	enum Color {Red = 1, Green =  2, Blue = 4};
	var c: Color = Color.Green;

---
	
通过value`2`反查其在枚举中的name：

	enum Color {Red = 1, Green, Blue};
	var colorName: string = Color[2];
	
	console.log(colorName); // Green
	
### Any

当我们编写应用时，可能需要描述一些未知类型的变量。这些变量可能来自动态内容，比如来自用户或者第三方类库。在这些情况下，我们想要免除类型检测让这些变量通过编译时检测就需要用到`any`类型：

	var list:any[] = [1, true, "free"];
	list[1] = 100;

### Void

最常见的就是作为function的返回类型：

	function warnUser(): void {
		alert("This is my warning message");
	}

	
