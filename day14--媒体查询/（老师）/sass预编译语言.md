# sass预编译语言

sass 自称世界上最成熟、最稳定、最强大的专业级CSS扩展语言！

是css的辅佐工具，它在 CSS 语法的基础上增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能

## 1、sass的优点

- 完全兼容 CSS3
- 在 CSS 基础上增加变量、嵌套 (nesting)、混合 (mixins) 等功能
- 通过[函数]进行颜色值与属性值的运算
- 提供[控制指令 (control directives)]等高级功能
- 自定义输出格式

## 2、sass的语法格式

（1）后缀名为： .scss的文件格式（常用）

（2）后缀名为： .sass的文件格式



## 3、css的扩展功能

### （1）嵌套规则

```
.box{
	header{
		height:100px;
		width:100px;
	}
	footer{
		width:200px;
		height:200px;
		color:red;
	}
}
```

编译为：

```
.box header{
	height:100px;
	width:100px;
}
.box footer{
	width:200px;
	height:200px;
	color:red;
}
```

**优点：嵌套功能避免了重复输入父选择器，而且令复杂的 CSS 结构更易于管理：**

### （2）父选择器（&）

在嵌套 CSS 规则时，有时也需要直接使用嵌套外层的父选择器，例如，当给某个元素设定 `hover` 样式时

```
.nav {
	li{
		height:40px;
		width:100px;
		background:#ccc;
		a{
			display:block;
			width:100%;
			height:100%;
		}
		&:hover{
			backgorund:orange;
		}
	}
}
```

编译后：

```
.nav li{
	height:40px;
	width:100px;
	background:#ccc;
}
.nav li a{
	display:block;
	width:100%;
	height:100%;
}
.nav li:hover{
	background:orange;
}
```

### （3）属性嵌套 

有些 CSS 属性遵循相同的命名空间 ，比如 `font-family, font-size, font-weight` 都以 `font` 作为属性的命名空间。为了便于管理这样的属性，同时也为了避免了重复输入，Sass 允许将属性嵌套在命名空间中

```
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```

编译后：

```css
.funky {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold;
}
```

## 4、变量

SassScript 最普遍的用法就是变量，变量以美元符号开头，赋值方法与 CSS 属性的写法一样：

```
$width:200px;

.box {
    .box1 {
        width: $width;
        height: 100px;
       border: 1px solid red;
    }
}
```

变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 `!global` 声明：

```
.box {
    .box1 {
   // 在.box里面定义局部变量，只能由.box里面调用，如果想要其他的元素也可以调用，就给变量后面添加!global
        $width: 200px !global;
        width: $width;
        height: 100px;
        border: 1px solid red;
    }

    .box2 {
        width: $width;
        height: $width;
        border: 1px solid green;
    }
}
```

## 5、函数指令

Sass 支持自定义函数，并能在任何属性值或 Sass script 中使用：

格式：

```
@function 函数名{
	@return 值;
}
.box{
	width:函数名(100px)
}
```

例如：

```
//定义函数
@function vw($px) {
    @return ($px / 750) *100vw;
}

//调用函数
.box2 {
	height: vw(80);
	border: 1px solid green;
}
```

