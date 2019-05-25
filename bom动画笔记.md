### 匀速动画
#### offset属性
+ offsetWidth/offsetHeight   检测盒子宽高  人为设定的宽高 + padding + border
+ offsetParent  获取到当前元素有定位的父盒子,没有直到body
+ inner.offsetParent  box没有定位  返回 body元素,box 有定位,返回 box 元素
  + 和style.left区别:
  1. style 只能获取行内样式,没有设置top/left 就返回 ""
  2. offsetLeft/offetTop 返回距离有定位的父盒子的左上距离,无论元素有没有定位
#### 匀速动画函数
```
function move(ele,target){
				
				// 60 fps
				var timer = setInterval(function (){
					// 起点 每次更新
					var start = ele.offsetLeft;
					// 步长 固定值
					console.log(start,target);
					var count = target > start ? 6 : -6;
					// 起点 + 步长 = 终点  停止动画
					// 终点可以被步长整除  可以使用 ===
					// 不能整除 证明 起点 + 步长 一定会 > 终点  需要知道终点和起点之间的距离,判断是否小于步长
					// 小于的情况下直接跳到终点
					// 距离
					var distance = target - start;
					// 取绝对值进行比较
					if(Math.abs(count) > Math.abs(distance)){
						clearInterval(timer);
						ele.style.left = target + "px";
					}else{
						// 运动
						ele.style.left = start + count + "px";						
					}
				},17)
}
```
##### 轮播主要内容
```
btns[0].onclick = function (){
				if(count === 0){
					ele.style.left = -(ele.children.length - 1) * w + "px";
					count = 5;
				}
				count --;//取值0-4
				move(ele,-count * w);
				
				// 清除激活小点的样式
				$(".act").className = "";
				dotts[count].className = "act";//取值0-4
			}
			
			btns[1].onclick = function (){
				
				// console.log(count);
				if(count === ele.children.length - 1){
					ele.style.left = "0px";
					count = 0;
					
				}
				count ++;//取值1-5
				move(ele,-count * w);
				
				// 清除激活小点的样式
				$(".act").className = "";
				if(count === ele.children.length - 1){
					// 临界值 最后一张  第一个小点激活
					dotts[0].className = "act";//取值0-4,count等于5时没有对应的点跳转到0
				}else
				{
					// 给当前激活小点添加样式
					dotts[count].className = "act";
				}
				
			}
			
			for(var i = 0 ; i < dotts.length; i ++){
				dotts[i].index = i;//给点添加下标
				dotts[i].onclick = function (){
					count = this.index;//当前下标对应的元素 i 值
					move(ele,-count * w);
					$(".act").className = "";
					this.className = "act";
				}
			}
```
+ jquery便捷操作封装
```
function $(str){
	var eleArr = null;
	if(str[0] === "."){
		eleArr = document.getElementsByClassName(str.slice(1));
		if(eleArr.length > 1){ return eleArr }else{ return eleArr[0]};
	}else if(str[0] === "#"){
		return document.getElementById(str.slice(1));
	}else{
		eleArr = document.getElementsByTagName(str);
		if(eleArr.length > 1 ){ return eleArr }else{ return eleArr[0] };
	}
}
```
#### 缓动动画函数
```
function slowly(ele, target) {
	var start, step;
	clearInterval(ele.timer);
	ele.timer = setInterval(function() {
		// 起点
		start = ele.offsetLeft;
		// 步长
		step = (target - start) / 10;
		// 判断步长临界值 (-1,1)
		if (Math.abs(step) < 1) {
			// 细分区间 (-1,0)  (0,1)
			step = step > 0 ? Math.ceil(step) : Math.floor(step);
		}
		// 判断终止条件
		if (start + step === target) {
			clearInterval(ele.timer);
		}
		// 运动
		ele.style.left = start + step + "px";
	}, 17)
}
```
### 事件
```
box.onclick = function (e){
    e = event || window.event;//谷歌等浏览器和IE浏览器获取事件对象的兼容写法
    var target = e.target || e.srcElement;
    //事件目标 指向触发事件的元素本身 兼容写法 谷歌等浏览器 e.target  IE浏览器 e.srcElement
    console.log("e.pageX=====>" + e.pageX);
    console.log("e.pageY=====>" + e.pageY);
   // 获取鼠标点击的相对于页面的位置,算入滚动条的距离
   console.log("e.clientX=====>" + e.clientX);	console.log("e.clientY=====>" + e.clientY);
	// 获取鼠标点击的相对于可视区域的位置,目前可见区域
    console.log("e.screenX=====>" + e.screenX); 	  console.log("e.screenY=====>" + e.screenY);
    // 获取鼠标点击的相对于屏幕的位置,整个屏幕
    console.log("e.offsetX===>" + e.offsetX);
	console.log("e.offsetY===>" + e.offsetY);
    //获取鼠标点击位置相对于元素的位置
}
box.onmousedown = function (e){
				e = event || window.event;
				// 点击的是鼠标的那个按键 只能在mousedown事件中知道鼠标按键类型
				console.log("点击的按键是===>",e.button);//0 1 2
			}
```
+ 阻止冒泡
```
$("img").onclick = function (e){
				e = event || window.event;
				e.stopPropagation ? e.stopPropagation() : e.cancelBubble = true;
			}
```
+ 事件委托
```
$("ul").onclick = function (e){
				e = event || window.event;
				// 获取目标元素
				var target = e.target || e.srcElement;
				if(target.tagName === "LI")//通过类名查找并且获取,委托
                {
					target.style.color = "red";
				}
			}
```
#### scroll属性
+ scrollWidth/Height 值  内容溢出时 值 = 内容宽/高 + padding
+ 内容未溢出 值 = 盒子宽高 + padding
```
// 封装函数获取被页面卷入的高度
			function sct(){
				return document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
			}
```
```
// 封装函数获取被页面卷入的左边距
			function scl(){
				return document.documentElement.scrollLeft || window.pageXOffset || document.body.scrollLeft;
			}
```
+ 缓动函数---起点终点不定(固定广告)
```
	var adv = $(".advance");
			// 1. 获取广告在页面未滚动时的原始高度 offsetTop
			var originY = adv.offsetTop;
			
			var timer = null;
			window.onscroll = function (){
				// 获取页面卷入高度  获取的值可能不是整数,变成整数
				var h = sct();
				// adv.style.top = originY + h + "px";
				var start,step;
				clearInterval(timer);
				timer = setInterval(function (){
					// 起点
					start = adv.offsetTop;
					step = (h + originY - start) / 10;
					if(Math.abs(step) < 1){
						step = step > 0 ? Math.ceil(step) : Math.floor(step);
					}
					if(start + step === h + originY){
						console.log("stop ...")
						clearInterval(timer);
					}
					adv.style.top = start + step + "px";
				},17)
			}
```
+ 需求变多,执行过程极其类似,   用 for 解决  [Array , Object]
+ 起点和终点只要知道,便可执行 for 解决需求   起点 ===> 样式名   终点 ===>  设置 ====>  写成对象的形式
+ 获取元素的样式(ele.style.xx只能获取行内样式,行内样式未写的时候获取空值)
```
function getStyle(ele, styleName) {
	if (ele.currentStyle) {
		return ele.currentStyle[styleName];
	} else {
		return window.getComputedStyle(ele, null)[styleName];
	}
}
```
```
function mulStyle(ele,target){
				clearInterval(ele.timer);
				ele.timer = setInterval(function (){
					// 声明是否成功的状态
					var status = true;
					for(var i in target){
						// 判断是否是层级
						if(i === "zIndex"){
							ele.style.zIndex = target[i];
							continue;
						}
						// 判断样式是否是透明度
						if(i === "opacity"){
							// 获取起点值
							var start = parseInt(getStyle(ele,i) * 100);//获取到的为字符串需转换为整数
							// 获取终点值
							var t = target[i] * 100;
						}else{
							// 获取起点值
							var start = parseInt(getStyle(ele,i));
							var t = target[i];
						}
						
						// 步长
						var step = (t - start) / 10;
						// 步长临界值
						if(Math.abs(step) < 1){
							step = step > 0 ? Math.ceil(step) : Math.floor(step);
						}
						// 判断是否到终点,改变status值
						if(start + step !== t){
							status = false;
						}
						// 开始动画
						if(i === "opacity"){
							ele.style[i] = (start + step) / 100;
						}else{
							ele.style[i] = start + step + "px";
						}
					}
					// 判断是否都到了终点
					if(status){
						console.log("stop ...");
						clearInterval(ele.timer);
					}
				},17)
			}
```
#### 旋转木马
+ 核心在于将各元素样式封装为对象数组,并对数组进行左右位移,调用多样式函数,将对应对象设为对应元素的目标样式实现样式的缓慢动画变更
```
	btn1.onclick = function (){
				arr.unshift(arr.pop());
				for(var i = 0; i < lis.length; i ++){
					mulStyle(lis[i],arr[i]);
				}
			}
			
			btn2.onclick = function (){
				// arr.push(arr[0]);
				// arr.shift();
				arr.push(arr.shift());
				for(var i = 0; i < lis.length; i ++){
					mulStyle(lis[i],arr[i]);
				}
			}
```
+ 多个类名增删
```
function addClass(ele) {
	// arguments 代表实参的集合
	// 获取旧的类名
	var old = ele.getAttribute("class");
	// arguments[0] === > ele
	// 从 第一位开始才是要添加类名
	if (old) {
		for (var i = 1; i < arguments.length; i++) {
			if (old.indexOf(arguments[i]) === -1) {
				old += " " + arguments[i];
				// old = old.concat(" " + arguments[i]);
				// console.log(old);
			} else {
				continue;
			}
		}
		ele.setAttribute("class", old);
	} else {
		// arguments === > [ele,"d1","d2","d3"]
		var str = "";
		for (var i = 1; i < arguments.length; i++) {
			str += arguments[i] + " ";
		}
		ele.setAttribute("class", str);
	}
}
```
```
function removeClass(ele) {
	// 获取旧的类名
	var old = ele.getAttribute("class");
	if (old) {
		var oldArr = old.split(" ");
		for (var i = 1; i < arguments.length; i++) {
			// 证明要删除的类名存在
			var index = oldArr.indexOf(arguments[i]);
			if (index !== -1) {
				oldArr.splice(index, 1);
			} else {
				continue;
			}
		}
		ele.setAttribute("class", oldArr.join(" "));
	}
}
```
#### 柱状图
+ 定时器控制循环
```
btns[1].onclick = function (){
				// 获取li的数组
				console.log(lis);
				// for(var j = 0; j < lis.length - 1; j ++){
				// 	for(var i = 0; i < lis.length - 1 - j; i ++){
				// 		if(lis[i].offsetHeight > lis[i+1].offsetHeight){
				// 			// parentNode.insertBefore(要插入的节点,参考节点)
				// 			lis[i].parentNode.insertBefore(lis[i+1],lis[i]);
				// 			var temp = lis[i+1].offsetLeft;
				// 			// lis[i+1].style.left = lis[i].offsetLeft + "px";
				// 			// lis[i].style.left = temp + "px";
				// 			// 添加动画
				// 			slowly(lis[i+1],lis[i].offsetLeft);
				// 			slowly(lis[i],temp);
				// 		}
				// 	}	
				// }
				var i = 0;	// 内环 i	控制每一圈的下标
				var j = 0;	// 外环 j	控制圈数
				var timer = setInterval(function (){
						if(lis[i].offsetHeight > lis[i+1].offsetHeight){
							// parentNode.insertBefore(要插入的节点,参考节点)
							lis[i].parentNode.insertBefore(lis[i+1],lis[i]);
							var temp = lis[i+1].offsetLeft;
							// lis[i+1].style.left = lis[i].offsetLeft + "px";
							// lis[i].style.left = temp + "px";
							// 添加动画
							slowly(lis[i+1],lis[i].offsetLeft);
							slowly(lis[i],temp);
						}
						i ++;
						if( i === lis.length - 1 - j){
							addClass(lis[i],"done");
							j ++;
							i = 0;
						}
						if(j === lis.length - 1){
							console.log("stop ...")
							clearInterval(timer);
						}
				},1000)
```