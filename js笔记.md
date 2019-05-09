 ### 变量名命名规则
+ 字母 数字 _ $ 
+ 不能以数字开头
+ 严格区分大小写
+ 不能使用关键字,保留字
+ 驼峰命名
+ 见名知意
### 数据类型
+ undefined 类型 只有一个值 undefined
+ 当一个变量声明了,但是没有被赋值  他就是undefined
```
    var c;
    console.log(c); // undefined  声明但是未被赋值
```
+ null指向一个空对象
```
console.log(typeof null); // object
```
+ NaN：是一个特殊的数字，表示Not a Number，非数值
```
    console.log("abc" / 18);    //结果是NaN
    console.log("abc" * "abcd");  //按理说，字符串相乘是没有结果的，但如果你非要让JS去算，它就一定会给你一个结果。结果是NaN
```
+ isNaN(); 任何不能被转换为数值的值，都会让这个函数返回 true。
```
		console.log(isNaN(123)); //FALSE
		console.log(isNaN('blue')); //true
		console.log(isNaN(NaN)); // true
```
+  typeof 可以判断数据类型
#### 数据类型转换
+ 转换为string
1. 加上一个空字符串 +''
2. toString
   + 和join区别在于
     + join可变更连接符
     + join仅适用数组转字符串
+ 转换为 number 类型  Number()
+ parseInt() 转换为整数
  + 转换规则：从第一个非空白字符（空格、换行、tab）开始转换，直到遇到一个非数字字符为止。
+  parseFloat() 转换成浮点数
   + 从第一个非空白字符（空格、换行、tab）开始转换，直到遇到一个非数字字符为止
   + 遇到的第一个小数点有效，第二个小数点就无效了
+ 转换为boolean 类型 Boolean()
  + 数字 --> 布尔。除了0和NaN，其余的都是true。
  +  字符串 ---> 布尔。除了空串，其余的都是true。
  + null和undefined都会转换为false。
  + 情况四：对象也会转换为true。
#### 运算符
+ ==存在隐式转换 先把字符串变成number 123,再比较
  + 等于 (只比较数值,不比较类型.比较之前会进行类型统一)
+ ===先比较数据类型,不一致 ,false,  类型一致 再比较数值
  + 严格相等 类型和数值都要相等才可
+ d = 10,不管是 d++ 还是 ++d 都实显现了+1
  + ++d 返回值是 +1之后的 11
  + d++ 返回值是 +1之前的 10
### 对象
#### Date对象
+ js当中的内置对象 Date
 ```
        //创建了 构造函数(Date) 的实例对象
		var date = new Date();
		console.log(date);
		// Sun May 05 2019 09:37:20 GMT+0800 (中国标准时间)
```
```
        var day = date.getDate();
		var month = date.getMonth()+1; // 0---11
		var year = date.getFullYear();
		var hour = date.getHours();
		var min = date.getMinutes();
		var seconds = date.getSeconds();
        //程序语言中 时间的最小单位为毫秒   1s = 1000 ms;
		var mm = date.getMilliseconds();
		// 周几
		var weekDay = date.getDay();
        // 时间戳  
		var stamp = date.getTime();
		console.log(stamp); // 距离 1970年1月1日 0 时0 分  的 毫秒数
```
#### Math对象
+ Math.ceil() 天花板函数  ,向上取整
  + `console.log(Math.ceil(2.3)); // 3`
+ Math.floor()  地板函数  向下取整
  + `console.log(Math.floor(2.9)); // 2`
+ Math.max()取最大值 Math.min()取最小值
  + console.log(Math.max(2,3,5,7)); // 7
  + console.log(Math.min(2,3,5,7)); // 2
+ Math.random()  范围 [0,1)
+ Math.pow(3,4)  //3的四次方
  + console.log(Math.pow(3,300000000000000000));// Infinity
  + console.log(10/0); // Infinity
+  Math.round()类似四舍五入
   + console.log(Math.round(2.499999999999999999999999999)); // 3
+ 如果要做的事情，只有一句话，那么可以省略大括号（在我这，一定要把大括号写完整
```
    if(a>20) alert('么么哒');
```
+ 表达式?如果表达式结果为true执行这里的代码:如果表达式结果为false执行冒号后面的代码;
  + `var rs = 5>3?5*3:5/3;`
  + 三元运算符可以理解为if..else的另外一种写法。
+ while和do...while
  + 功能类似
  + while是先判断后执行，而do...while是先执行后判断。
  + 即使条件不满足，do...while可以保证循环体至少执行一次，而while不能
+ break和continue
  + for循环嵌套,break只能退出当前的这个for循环
  + continue跳出当次循环,不影响之后的循环
### 数组
1. 合并数组 xx.concat()  并不会影响原数组
   + 合并好的数组,()内在后,xx在前
2. 字符串转数组, arr.split('分隔符','指定生成数组的长度')
3. 数组转字符串, arr.join('连接符号'); 参数不写,默认用逗号链接
4. 添加元素xx.push()从数组最后推入一个元素  改变了原数组 返回新数组的长度
   + xx.unshift()  从前边插入元素 改变了原数组 返回新数组的长度
5. 删除元素  删除前边的 第一个元素  xx.shift()
   + 删除 数组 最后一个元素  xx.pop()
   + 二者 都改变了原数组
   + 返回值  是删除的那个元素
### 函数
+ 形参个数 和  实参个数 不一致
  + 形参 比实参 数量多  计算错误
  +  实参 比 形参多,  
  + 通常情况下.要保证 实参和形参个数一致
+ return用法
  + 函数程序运行后的结果外部需要使用的时候，我们不能拿到，需要通过return返回。
  + 函数使用return语句后，这个函数会在执行完 return 语句之后停止并立即退出，也就是说return后面的所有其他代码都不会再执行。
  + 函数里面可以没有return。
  + 函数体外  拿不到  函数体内 声明的变量
#### 选择排序
```
function selectSort (arr){
			for (var i = 0; i < arr.length; i++) {
				var minIndex = i;
				for (var j = i+1; j < arr.length; j++) {
					if(arr[minIndex]>arr[j]){
						minIndex = j;
					}
				}
				var temp = arr[i];
				arr[i] = arr[minIndex];
				arr[minIndex] = temp;
			}
			// 排序完成了
			return arr;
		}
```
#### 冒泡排序
```
function bubbleSort (arr){
			for (var i = 0; i <arr.length; i++) {
				for (var j = 0; j < arr.length-i; j++) {
					if (arr[j]>arr[j+1]) {
					var temp = arr[j];	
                    arr[j] = arr [j+1];
                    arr[j+1] = temp;

					}
				}

			}
			return arr;
		}
```
#### 翻转数组
```
function reverse (arr){
			var newArr = [];
			for (var i = arr.length-1; i >= 0; i--) {
				newArr.push(arr[i]);
			}
			return newArr
		}
```
#### 阶乘和
```
function sumOFfactorial(num){
			var sum = 0;
			for (var i = 1; i <= num; i++) {
				sum = sum + getFactorial(i);
			}
			return sum;
		}
		function getFactorial (num){
			var factorial = 1;
			for (var i = 1; i <= num; i++) {
				factorial*=i;
			}
			// factorial*1*2*3*4*5
			return factorial;
		}
```
#### 质数判断
```
function isPrime (num){
			// 假设 是一个质数
			var isZhi = true;
			for (var i = 2; i < num; i++) {
				if (num%i===0) {
					isZhi = false;
				}
			}
			return isZhi?'是一个质数':'不是一个质数';
		}
```
+ 基本数据类型作为参数传递的时候,会在函数内部创建这个数据的副本,做的操作,并不会影响原理数据
+ 复杂数据(ex数组)作为参数传递的时候会影响外部的参数,因为归根结底原数据被修改了
#### Fibonacci数列
```
function Fibonacci (n){
			// 跳出条件
			if(n===1||n===2){
				return 1;
			}
			return f(n-1)+f(n-2);
		}
```
### 对象
1. 属性(特征) 方法(行为/动态)
2. 封装 信息
3. 对象属性值 任意的数据类型, 属性值是函数,我们称之为对象的方法
+ 对象的分类
  1. 内置对象   Date  Math  Number 
  2. 宿主对象 由JS的运行环境提供的对象，目前来讲主要指由浏览器提供的对象。
      + 比如BOM  DOM
  3. 开发者自己定义的对象
+ this指针
  + 构造函数当中的this指向 new出来的实例对象
  + 如果不通过new实例对象,那么this指向调用者!!!
+ xx.xx和xx{key}
  + xx.xx 这种形式 只能取原来具有的属性
  + 非常重要! xx.abc  abc是变量,就必须通过  xx[abc] 形式取值
### 数组高级api
+ array.reverse() 反转数组,会改变原数组
+ array.sort() 排序,改变原数组
  + 给数组排序，返回排序后的数组。如何排序看参数
    + 无参：按照数组元素的首字符对应的Unicode编码值从小到大排列数组元素。
    + 带参：必须为函数（回调函数--callback）。函数中带有两个参数，代表数组中的前后元素。如果计算后（a-b），返回值为负数，a排b前面。等于0不动,返回值为正数，a排b后面。
    ```
    array.sort(function(a,b){
            return a-b;
        })
    ```
+ indexOf()、lastIndexOf()   //如果没找到返回-1
  + 返回对应数值在数组中的下标
+ slice(start,end) 从当前数组中截取一个新的数组，不影响原来的数组，
  + slice(0); // 复制数组
  + 参数start从0开始,end从1开始 [start,end)
+ splice()
  + 删除或替换当前数组的某些项目，参数start,deleteCount,options(要替换的项目)
  + 修改原数组 返回值是删除或者替换掉的哪些元素
  + splice(0,2); // 不写替换元素,就实现了删除
### string方法
+ charAt()获取相应位置字符
  + 空格也 占位置
+ charCodeAt() 方法可返回指定位置字符的 Unicode 编码
+ indexOf() / lastIndexOf()
    + 返回字符在字符串中的位置(方法同数组类似)
+ concat() 连接字符串
+ slice()	  方法可提取字符串的某个部分，并以新的字符串返回被提取的部分
+ substr(起始位置,[取的个数])  截取字符串 返回截取的字符串
+ slice和substr区别
  + slice接收的是起始位置和结束位置(不包括结束位置)，而substr接收的则是起始位置和所要返回的字符串长度。
  + 
+ 转换大小写
```
        console.log(str.toUpperCase()); // HOW ARE YOU? AND YOU?
        console.log(str);
        console.log(str.toLowerCase()); // how are you? and you?
```
#### 字母出现次数
```
var arr = ["c","a","z","a","a","z","b"];
        // 存放字母
        var wordArr = [];
        // 存放字母个数
        var countArr= [];
        for (var i = 0; i < arr.length; i++) {
            if(wordArr.indexOf(arr[i])==-1){
                // 往里添加元素
                wordArr.push(arr[i]);
                countArr.push(1);
            }else{
                // 找元素对应下标
                var index = wordArr.indexOf(arr[i]);
                countArr[index]++;
            }    
        }
        console.log(wordArr);
        console.log(countArr);
        for (var i = 0; i < wordArr.length; i++) {
            console.log('字母'+wordArr[i]+'出现了'+countArr[i]+'次');      
        }
```
```
var arr1 = ["c","a","z","a","a","z","b"],
		count = {};
		for (var i = 0; i < arr1.length; i++) {
			var key = arr1[i]
			if (count[key]) {
				count[key]++;
			}else{                             
				count[key]=1;   
			}
		}
		console.log(count);//{c: 1, a: 3, z: 2, b: 1} 
```
#### 细节问题
```
 var arr = [1500,1200,2000,2100,2200,1800];
        // 第一种思路
        // 遍历 把小于等于2000 的添加到一个新数组里边,返回新数组
        // 第二种思路 遍历,删除
        for (var i = 0; i < arr.length; i++) {
            if(arr[i]>2000){
                // 执行删除
                arr.splice(i,1); // 删除  修改了原数组
                i--;
            }   
        }
        console.log(arr);
```

