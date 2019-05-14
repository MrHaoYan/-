+ 指针this
1. 有new的指向实例对象
2. 没有的话,指向调用的对象
```
for (var i = 0; i < lis.length; i++) {
            lis[i].onclick = function(){
                // 获取imgUrl
                // 这个地方不能用lis[i],只能用this
                //lis[i]此时已循环到最后
                var imgUrl = this.children[0].src;
                console.log(imgUrl);
                imgEl.src = imgUrl;
                  console.log(i);
            }    
        }
```
+ nextSibling  (previousSibling上一个)
  + 获取 下一个兄弟节点  nextSibling  包括 文本节点 换行,空格,注释
+ nodeType  
  + 1 标签节点
  + 3 文本节点
  + 8 注释节点
     + 可用于判断节点类型且筛选
```
for (var i = 0; i < myChildren.length; i++) {
                if(myChildren[i].nodeType===1){
                    childrenArr.push(myChildren[i]);
                }  
            }
```
+ 求除了自己以外的所有节点
  1. 遍历所有节点,去掉 他自己          
```
 function getSiblings(el){
                var siblings = []; 
                var pNode = el.parentNode;
                // 所有孩子节点
                var children = pNode.children;
                for (var i = 0; i < children.length; i++) {
                    // 兼容ie8
                    if(children[i].nodeType == 1){
                        if(children[i]!=el){
                            siblings.push(children[i]);
                        }
                    } 
                }
                return siblings;
            }
```
  2. + 找到 前边的素有兄弟节点
     +  找到后边的所有兄弟及节点
         1. 获取后边的所有兄弟节点,倒着遍历
         2. lock 上锁
     + 合并
     + 获取前边的兄弟节点 
```
 function getPrevSiblings(el){
                var rs = []; 
                var pNode = el.parentNode;
                // 所有孩子节点
                var children = pNode.children;
                for (var i = 0; i < children.length; i++) {
                    // 兼容ie8
                    if(children[i].nodeType == 1){
                        if(children[i]!=el){
                            rs.push(children[i]);
                        }else{
                            break;
                        }
                    } 
                }
                return rs;
            }
```
```
function getNextSiblings(el){
                var rs = []; 
                var pNode = el.parentNode;
                // 所有孩子节点
                var children = pNode.children;
                var lock = false;
                for (var i = 0; i < children.length; i++) {
                    if(children[i]==el){
                        lock = true;
                        continue; // 跳出本次循环
                    }
                    if(lock){
                        // 兼容ie8
                        if(children[i].nodeType == 1){
                            rs.push(children[i]);
                        } 
                    }   
                }
                return rs;
            }
```
```
function getNextSiblings2(el){
                var nextArr = getNextSiblings(el);
                var prevArr = getPrevSiblings(el);
                var rs = [];
                rs = rs.concat(prevArr);
                rs = rs.concat(nextArr);
                return rs;
            }
```
+ 不插入节点 ,是不会在页面当中显示的
  +  父节点.appendChild();
  + 父节点.insertBefore(要插入的节点，参考节点)；
  + 同一个 节点 不能重复插入
  + 如果参考节点为null，那么他将在节点最后插入一个节点。
  + 删除节点  父节点.removeChild（子节点）
  + 不知道父级的情况下，可以这么写：`node.parentNode.removeChild(node)`
  + 复制节点 oldNode.cloneNode（true） 
  + 参数 true，深层复制，如果是false，只复制节点本身。
+ innerHTML插入可执行的标签，标签和样式会被解析，常用于动态生成页面元素
  + 每一次innerHTML 会覆盖之前的
+ innerText 插入文本内容，标签和样式会被当做文本内容处理。
+ 排他思想
  + 先全删除,然后重新添加
```
   for (var j = 0; j < lis.length; j++) {
                    // 去掉所用li的  active
                    delClass(lis[j],'active');
                }
                // 给当前点击的li 添加active
                addClass(this,'active');
            }   
        }
```
+ class类名添加函数
```
   function addClass(el,className){
        //获取之前的类名
        var oldClassStr = el.getAttribute('class');
        // console.log(oldClassStr);
        //strong danger
        //如果之前没有class,返回null
        if (!oldClassStr) {
            el.setAttribute('class',className);
        }else{
            //拼接前先判断有没有新增的这个className,如果有,没必要添加,没有的才需要添加
            // indexOf不可以使用在字符串当中
            oldClassArr = oldClassStr.split(' ');
            console.log(oldClassArr);
            if(oldClassArr.indexOf(className)===-1){
                //不存在重复
                var newClassStr = oldClassStr + ' ' +className;
                el.setAttribute('class',newClassStr);
            }
        }

    }
```
+ class类名删除函数
```
 function delClass(el,className){
        //获取之前的类名
        var oldClassStr = el.getAttribute('class');
        //console.log(oldClassStr);
        //strong danger
        if (oldClassStr) {
            //删除之前,应该判断有没有这个类名
            oldClassArr = oldClassStr.split(' ');
            if (oldClassArr.indexOf(className)!==-1) {
                // 获取需要删除元素的下标
                var index = oldClassArr.indexOf(className);
                oldClassArr.splice(index,1);
                var newClassStr = oldClassArr.join(' ');
                el.setAttribute('class',newClassStr);
                
            }
            
        }
    }
```
+ 配合for循环 动态生成任意数量的标签
```
for (var i = 0; i < imgArr.length; i++) {
        // 三元运算符写法
        str = str + '<li class="img-item'+(i==0?' active':'')+'"><img src="img/'+imgArr[i]+'" alt=""></li>'
         
     }
```
+ 小米轮播
  + 计数器
```
function swipeImg(isRight){
            if(isRight){
                count++;
                if(count===imgArr.length){
                    count = 0;
                }
            }else{
                count--;
                if(count===-1){
                    count = imgArr.length-1;
                }   
            }
            console.log(count)
            go(count);
            }
```
+ go函数(控制轮播图片路径和圆点样式的增删,且圆点传递的参数可传递到计数器)
```
  function go(num){
            count = num;//中间参数num,count和i作为实参
            imgEl.src = 'img/' + imgArr[num];
            for (var i = 0; i < dotChildren.length; i++) {
                delClass(dotChildren[i],'active');
            }
            addClass(dotChildren[num],'active');
        }
```
+ 给小圆点(分页器) 循环绑定事件
```
        for (var i = 0; i < dotChildren.length; i++) {
            dotChildren[i].index = i;
            // 点击的 小圆点的下标
            dotChildren[i].onclick = function(){
                // imgEl.src = 'img/' + imgArr[i]; 
                // 获取下标 i ?   
                console.log(this.index);//随着点击变化
                // dotChildren伪数组,具有length属性,但是不具有数组的方法,indexOf无法使用
                var index = this.index;
                imgEl.src = 'img/' + imgArr[index];
                for (var j = 0; j < dotChildren.length; j++) {
                    delClass(dotChildren[j],'active');
                }
                addClass(dotChildren[index],'active');
            }    
        }
```
+ arguments 是一个伪数组 
  + `console.log(arguments instanceof Array); `// false  不是数组
    + instanceof 用于判断  是不是某个构造函数的实例对象 
	+ 可以判断 是不是数组,是不是函数
+ `console.log(arguments.callee);`// 返回的是正在执行的函数本身。 也是在函数体内使用。 在使用函数递归调用时推荐使用arguments.callee代替函数名本身。 
```
function fb(n){
			if(n==1||n==2){
				return 1;
			}
			return arguments.callee(n-1)+arguments.callee(n-2);
		}
```
+ addEventListener
```
 boxEl.addEventListener('click',function(){
            alert('我是外部box');
        },false)
        // 可以注册多个事件
        // boxEl.addEventListener('click',function(){
        //     alert('edf');
        // })

        // 第一个参数: 字符串 事件类型  不带"on"
        // 第二个参数: 函数 (要执行的程序)
        // 第三个参数: 是否捕获执行,默认false   false/true
        innerBox.addEventListener('click',function(event){
            alert('我是inner-box');
            // 阻止冒泡!
            event.stopPropagation();
        })

        // 从里到外   冒泡
        // 从外到里   捕获
        // 思考 ,点击innerbox 只执行 innerbox的事件..(阻止冒泡)
```
+ removeEventListener //移除绑定
  +  删除时 ,捕获和冒泡必须是一致的
+ setTimeout()延迟执行 clearTimeout(); //清除延迟定时器的
+ setInterval()循环执行   clearInterval()  清除循环执行
