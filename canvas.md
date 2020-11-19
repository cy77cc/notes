# canvas

从上到下同步执行代码

1、获取canvas标签

```javascript
<canvas id="canvas" width="400px" height="400px"></canvas>
var canvas = document.getElementById('canvas')
```

## 绘制矩形

```JavaScript
1.绘制矩形
	canvas提供了三种方法绘制矩形：
		---->绘制一个填充的矩形（填充色默认为黑色）
			fillRect(x, y, width, height)
		---->绘制一个矩形的边框（默认边框为:一像素实心黑色）
			strokeRect(x, y, width, height)
		---->清除指定矩形区域，让清除部分完全透明。	
			clearRect(x, y, width, height)
			
	x与y指定了在canvas画布上所绘制的矩形的左上角（相对于原点）的坐标。
	width和height设置矩形的尺寸。（存在边框的话，边框会在width上占据一个边框的宽度，height同理）

2.strokeRect时，边框像素渲染问题
	按理渲染出的边框应该是1px的，
	canvas在渲染矩形边框时，边框宽度是平均分在偏移位置的两侧。
		context.strokeRect(10,10,50,50)
			:边框会渲染在10.5 和 9.5之间,浏览器是不会让一个像素只用自己的一半的
			  相当于边框会渲染在9到11之间
		context.strokeRect(10.5,10.5,50,50)
			:边框会渲染在10到11之间

3.添加样式和颜色
	fillStyle   :设置图形的填充颜色。
	strokeStyle :设置图形轮廓的颜色。
		默认情况下，线条和填充颜色都是黑色（CSS 颜色值 #000000）
	lineWidth : 这个属性设置当前绘线的粗细。属性值必须为正数。
		描述线段宽度的数字。 0、 负数、 Infinity 和 NaN 会被忽略。
		默认值是1.0。
		
4.lineWidth & 覆盖渲染

5.lineJoin
	设定线条与线条间接合处的样式（默认是 miter）
	round : 圆角
	bevel : 斜角
	miter : 直角
```

## 绘制路径

### canvas绘制路径

​	图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。
步骤
​	1.首先，你需要创建路径起始点。
​	2.然后你使用画图命令去画出路径
​	3.之后你把路径封闭。
​	4.一旦路径生成，你就能通过描边或填充路径区域来渲染图形。

### 绘制三角形

​	beginPath()
​		新建一条路径，生成之后，图形绘制命令被指向到路径上准备生成路径。

```javascript
生成路径的第一步叫做beginPath()。本质上，路径是由很多子路径构成，这些子路径都是在一个列表中，
所有的子路径（线、弧形、等等）构成图形。而每次这个方法调用之后，列表清空重置，
然后我们就可以重新绘制新的图形。

moveTo(x, y)
	将笔触移动到指定的坐标x以及y上
	当canvas初始化或者beginPath()调用后，你通常会使用moveTo()函数设置起点
	
lineTo(x, y)
	将笔触移动到指定的坐标x以及y上
	绘制一条从当前位置到指定x以及y位置的直线。

closePath()
	闭合路径之后图形绘制命令又重新指向到上下文中。
		闭合路径closePath(),不是必需的。这个方法会通过绘制一条从当前点到开始点的直线来闭合图形。
	如果图形是已经闭合了的，即当前点为开始点，该函数什么也不做
		当你调用fill()函数时，所有没有闭合的形状都会自动闭合，所以你不需要调用closePath()函数。
	但是调用stroke()时不会自动闭合
	
stroke()
	通过线条来绘制图形轮廓。
	不会自动调用closePath()
	
fill()
	通过填充路径的内容区域生成实心的图形。
	自动调用closePath()
```

### 绘制矩形

​	rect(x, y, width, height)
​		绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。
​		当该方法执行的时候，moveTo()方法自动设置坐标参数（0,0）。
​		也就是说，当前笔触自动重置会默认坐标

### lineCap

​	lineCap 是 Canvas 2D API 指定如何绘制每一条线段末端的属性。
​	有3个可能的值，分别是：
​		butt  :线段末端以方形结束。 
​		round :线段末端以圆形结束
​		square:线段末端以方形结束，但是增加了一个宽度和线段相同，高度是线段厚度一半的矩形区域
​	默认值是 butt。	

### save

​	save() 是 Canvas 2D API 通过将当前状态放入栈中，保存 canvas 全部状态的方法

	保存到栈中的绘制状态有下面部分组成：
		当前的变换矩阵。
		当前的剪切区域。
		当前的虚线列表.
		以下属性当前的值： 
	        strokeStyle, 
	        fillStyle,  
	        lineWidth, 
	        lineCap, 
	        lineJoin...

### restore

​	restore() 是 Canvas 2D API 通过在绘图状态栈中弹出顶端的状态，将 canvas 恢复到最近的保存状态的方法。 
​	如果没有保存状态，此方法不做任何改变。	

### 基本模板

```
ctx.save();
关于样式的设置
ctx.beginPath();
关于路径
ctx.restore();
1、路径容器
	每次调用路径api时，都会往路径里做登记
	调用beginPath时，清空整个路径容器
2、样式容器
	每次调用样式api时，都会往样式容器里做登记
	调用save时，将样式容器里的状态压入样式栈
	调用restore是，将样式栈的栈顶状态弹出到样式容器里，进行覆盖
3、样式栈
	调用save时，将样式容器里的状态压入样式栈
	调用restore是，将样式栈的栈顶状态弹出到样式容器里，进行覆盖
```

## canvas绘制圆形

**角度与弧度的js表达式:radians=(Math.PI/180)*degrees。**

arc(x, y, radius, startAngle, endAngle, anticlockwise)
			画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，
			按照anticlockwise给定的方向（默认为顺时针）来生成。
			ture：逆时针
			false:顺时针

	x,y为绘制圆弧所在圆上的圆心坐标
	radius为半径
	startAngle以及endAngle参数用弧度定义了开始以及结束的弧度。这些都是以x轴为基准
	参数anticlockwise 为一个布尔值。为true时，是逆时针方向，否则顺时针方向。

arcTo
	arcTo(x1, y1, x2, y2, radius)
	根据给定的控制点和半径画一段圆弧
	肯定会从(x1 y1)  但不一定经过(x2 y2);(x2 y2)只是控制一个方向		

## 贝塞尔曲线

### 二次贝塞尔

​	quadraticCurveTo(cp1x, cp1y, x, y)
​		绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点。
​		起始点为moveto时指定的点

### 三次贝塞尔

​	bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
​		绘制三次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。
​		起始点为moveto时指定的点		

## canvas中的变换

	translate(x, y)
		我们先介绍 translate 方法，它用来移动 canvas的原点到一个不同的位置。
		translate 方法接受两个参数。x 是左右偏移量，y 是上下偏移量，
		在canvas中translate是累加的
	
	rotate(angle)
		这个方法只接受一个参数：旋转的角度(angle)，它是顺时针方向的，以弧度为单位的值。
		旋转的中心点始终是 canvas 的原点，如果要改变它，我们需要用到 translate 方法
		
		在canvas中rotate是累加的
		
	scale(x, y)
		scale 方法接受两个参数。x,y 分别是横轴和纵轴的缩放因子，它们都必须是正值。
		值比 1.0 小表示缩小，比 1.0 大则表示放大，值为 1.0 时什么效果都没有。
		缩放一般我们用它来增减图形在 canvas 中的像素数目，对形状，位图进行缩小或者放大。
		
		在canvas中scale是累称的

### 表盘

​	1.初始化
​		将圆心调整到画布的中间
​		由于canvas中画圆与旋转所参照的坐标系于正常坐标系有出入
​			将整个画布逆时针旋转90度
​		初始化一些样式数据
​			ctx.lineWidth = 8;
​		  	ctx.strokeStyle = "black";
​		  	ctx.lineCap = "round";

	2.外层空心圆盘
		圆盘颜色:#325FA2
		圆盘宽度:14
		圆盘半径:140
		
	3.时针刻度
		长度为20
		宽度为8
		外层空心圆盘与时针刻度之间的距离也为20
		
	4.分针刻度
		宽度为4
		长度为3
		
	5.时针
		宽度为14
		圆心外溢出80 收20
		
	6.分针
		宽度为10
		圆心外溢出112 收28
		
	7.秒针
		颜色:D40000
		宽度为6
		圆心外溢出83 收30
		
		---->中心实心圆盘
			半径为10
		---->秒针头
			96码开外半径为10的空心圆
			宽度为6


​		
​	