### 选择器
+ 选择紧挨着的下一个元素
```
            .li3+li{
	 		color: blue;
	 	}
```
+ /*后面的所有兄弟元素*/
```	 	
         .li3~li{
	 		background-color: orange;
	 	}
```
+ /*子代选择器 直接孩子  不管孙子*/
```        
         .d1>.box{
            width: 300px;
        }
``` 
+ 选择相应下标的元素`$('li:eq(1)').css('background', 'red');`
+ // 选择序号大于index的元素`$('li:gt(5)').css('background', 'red');`
+ // 选择小于index的元素`$('li:lt(5)').css('background', 'blue');`
+ //index为奇数
    `$('li:odd').css('background', 'orange');`
+ // index为偶数`$('li:even').css('background', 'pink');`
+ //第一个元素`$('li:first').css('background', 'red');`
+ // 最后一个元素`$('li:last').css('background', 'red');`
+ `$(“a[href]”)  title  type ` 选择所有包含href属性的元素`$(“a[href]”). css(“background”,”red”)`
+ `$(“a[href=’baidu’]”)`选择href属性值为baidu的所有a标签`$(“a[href=’baidu]”). css(“background”,”red”)`
+ `$(“a[href!=’baidu’]”)`选择所有href属性不等baidu的所有元素，包括没有href的元素`$(“a[href!=’baidu’]”). css(“background”,”red”)`
+ `$(“a[href^=’web’]”)`选择所有以web开头的元素`$(“a[href^=’web’]”). css(“background”,”red”)`
+ `$(“a[href$=’cn’]”)`选择所有以cn结尾的元素`$(“a[href$=’cn’]”). css(“background”,”red”)`
+ `$(“a[href*=’i’]”)`选择所有包含i这个字符的元素，可以是中英文`$(“a[href*=’i’]”). css(“background”,”red”)`
+ `$(“a[href][title=’内容’]”)`选择所有符合指定属性规则的元素，都符合才会被选中`$(“a[href][title=’内容’]”). css(“background”,”red”)`
### 筛选
+ // 查找指定元素的所有后代元素（子子孙孙） find(selector)
`$('.box').find('div').css('color','red')`
+ // 查找指定元素的直接子元素（亲儿子元素） children()
`$('.box').children().css('color','orange');`
+ 设置样式`$('.box').css('width','200px');`
+ 获取样式`console.log($('.box').css('height'));`
+ // 设置多个样式
```
        $('.box').css({
            width:'300px',
            height:'400px',
            backgroundColor:'green'
        })
```
+ 属性设置
```
 console.log($('.box').attr('class')); // getAttribute()
        $('.box').attr('class','danger'); // setAttribute()
        removeAttr()
```
+ 内容设置
```
        // 获取文本内容
        alert($('.box').text());
        // 设置文本内容
        $('.box').text('天气很好');
        // 获取   带标签
        alert($('ul').html());
        // 设置   可识别标签
        $('ul').html('<p>今天天气很好</p>');
          获取输入框的内容
        $('.btn1').click(function(){
            alert($('input').val());
        })
        设置输入框得内容
        $('.btn2').click(function(){
            $('input').val('呵呵呵呵');
        })
```
+ 类名设置
```
        addClass() - 向被选元素添加一个或多个类
        $('p').addClass('danger strong');
        removeClass() - 从被选元素删除一个或多个类
        $('p').removeClass('strong');
        toggleClass() - 对被选元素进行添加/删除类的切换操作  (有则删除,无则添加)
        $('p').toggleClass('em');
        hasClass()- 判断是否存在类,参数必须，
        console.log($('p').hasClass('strong')); // true false
```
+ 节点
```
       // 后面的  兄弟节点 
        console.log($('.li5').siblings());
        console.log($('.li5').next());
        console.log($('.li5').nextAll());  
        // 后面的所有兄弟  直到li9 这个节点结束 (不包括结束节点)
        console.log($('.li5').nextUntil($('.li9')));
        // 前边的  prev() / prevAll() /prevUntil()
        // parent() 父亲节点  /parents()
        console.log($('.inner-box').parent());
        // 所有的 父类节点
        console.log($('.inner-box').parents());
        // 不包括结束节点
        console.log($('.inner-box').parentsUntil($('body')));
```
```
        // $('.box').html($spanNode);
        // var node = $('.box').html('<li>我是li</li>');
        
        // 从后
        // 追加节点 append
        // 在元素的最后一个子元素后面追加元素：
        $('.box').append($spanNode);
        // 如果是页面中存在的元素，那么调用append()后，
        // 会把这个元素放到相应的目标元素里面去；但是，原来的这个元素，就不存在了。
        $('li').append($spanNode);
        // 如果是给多个目标追加元素，
        // 那么方法的内部会复制多份这个元素，然后追加到多个目标里面去。

        $('.box').append($spanNode);
//         appendTo()
// 作用：把$(selector)追加到node中去 $(selector).appendTo(node);
        $liNode.appendTo($('.box'));
        // 从前边
//         prepend()
// 作用：在元素的第一个子元素前面追加内容或节点
// after()
// 作用：在被选元素之后，作为兄弟元素插入内容或节点
// $(selector).after(node);
$('.box').after($('<div>w box</div>'));

 
// before()
// 作用：在被选元素之前，作为兄弟元素插入内容或节点
// $(selector).before(node);

$('.box').before($('<div>before box</div>'));
```
```
 $('.box').empty(); // 清空选中节点的所有子节点(包括内容和节点)
        
        $('.box2').html('');

        $('.box3').remove(); // 清空  包括自己


        // 复制元素
        console.log($('.box4').clone());
        $('body').append($('.box4').clone());
```
+ 表单
```
  // 获取表单当中  单选框   和 多选框的状态
        $('.btn1').click(function(){
            console.log($('.like').prop('checked'));
            console.log('单选框状态',$('.sex').prop('checked'));
            设置单选框的状态
    $('.sex').prop('checked',true)
     $('.sex').prop('checked',false)
        })
```
```
            $("input[type='checkbox']").prop("checked");
            //用于遍历 form表单中的多选框和单选框的选中状态
            // $('.btn1').click(function()  {
            //     alert($('.like').prop('checked'));
            //     alert($('.sex').prop('checked'));
            // })
```
+ 动画
```
//         作用：让匹配的元素展示出来
// 	$(xx).show(2000)
// 	$(xx).show()		slow：600ms、normal：400ms、fast：200ms
// 	$(xx).show(2000,function(){});
// 	$(xx).show()
 $('.box').hide(2000); 隐藏
 $('.box').slideDown(2000)滑入
 $('.box').slideUp(2000);滑出
 $(xx).slideToggle(speed,callback);  滑入滑出切换
$('.box').fadeIn(2000);淡入
 $('.box').fadeOut(1000);淡出
 $('.box').fadeToggle(1000);  淡入淡出切换
 $('.box').fadeTo(2000,.7);  改变透明度到某个值


 // $(selector).animate(styles,speed,easing,callback)
        // 第一个参数表示：要执行动画的CSS属性（必选）
 	// 第二个参数表示：执行动画时长（可选）
    //  第三个参数: 可选。规定在不同的动画点中设置动画速度的 easing 函数。
    //  内置的有  swing  linear
	// 第四个参数表示：动画执行完后立即执行的回调函数（可选）
    $('.box').click(function(){
        $('.box').animate({
            width:'200px',
            height:'200px',
            fontSize:'50px',
            left:'1000px',
            top:'100px'
        },2000,'swing',function(){
            // $('.box').animate({
            //     left:'100px',
            //     top:0,
            //     fontSize:'20px'
            // },1000)
        })
        //  box的 第一个动画 执行完,才会执行第二个
        $('.box').animate({
            left:'100px',
            top:0,
            fontSize:'20px'
        },1000)
    })

//     stop(stopAll,goToEnd);
// stopAll  是否全部停止，默认false 停止队列中所有的动画
// goToEnd  是否将停止的动画  默认 false 停止在当前动画的最后一个状态  

    $('.btn').click(function(){
        $('.box').stop(true);
    })
```
+ bom相关
```
//         高度和宽度操作
// 	height()    取值类型为num  可以直接参与运算
// 	height(200)
// 	width()
// 	width(100)
        console.log($('.box').height()); // 100 盒子高度 ,不包括 padding  border
        $('.box').height(200); 

        console.log($('.box').width()); // 100 盒子宽度 ,不包括 padding  border
        $('.box').width(200); 
//         offset() 
// 作用：获取或设置元素相对于文档的位置
// $(selector).offset();
// $(selector).offset({left:100, top: 150});
        
        console.log('box相对于文档的位置 left',$('.box').offset().left); // 30
        console.log('box相对于文档的位置 top',$('.box').offset().top); // 30
        $('.box').offset({
            left:60,
            top:60
        })
        console.log('innerbox相对于文档的位置 left',$('.inner-box').offset().left); // 30
//         position() 
// 作用：获取相对于其最近的具有定位的父元素的位置。
// 	$(selector).position();
// 注意：只能获取，不能设置。
console.log('innerbox position位置 left',$('.inner-box').position().left);
console.log('innerbox position位置 top',$('.inner-box').position().top);
// scrollTop() 
// 作用：获取或者设置元素垂直方向滚动的位置
// 	$(selector).scrollTop();
// 		$(selector).scrollTop(100);

// scrollLeft() 
// 作用：获取或者设置元素水平方向滚动的位置
// $(selector).scrollLeft(100);
$('.top').click(function(){
    console.log($(document.documentElement).scrollTop());
    // $(document.documentElement).scrollTop(0);
    $(document.documentElement).animate({
        scrollTop:0
    })
})
```
+ 手风琴
```
<script>  
        var currentLi = null;
        var timer = null;  
        $('.li-item').mouseenter(function(){
            // 这里边 this  指向当前的dom元素
            // currentLi = this;
            var self = this;//指向当前li
            clearTimeout(timer);
            // 延迟 hover  ,停留200ms  才会触发 动画
            // 每进入一张新的图片,都会清掉之前的timer
            timer = setTimeout(function(){
                currentLi = self;
                // 这里边 this指向会发生变化
                $(self).siblings().animate({
                    width:'100px'
                });
                $(self).animate({
                    width:'700px'
                });
            },200)    
        })
        $('ul').mouseleave(function(){
            // 这里边 this  指向当前的dom元素  
            clearTimeout(timer);
            $(currentLi).animate({
                width:'200px'
                //哪个才是需要收缩的li? 已激活的那个  指针需写在激活里面
            })
            $(currentLi).siblings().animate({
                width:'200px'
            })
        })
    </script>
```
+ 表格需要注意的点
  + 部分点击事件需写在行内,以确保新生成的表格可调用点击事件
  + 事件传参可以采用指针或者其他的变量以确保对当前dom元素生效`</button><button class="edit" onclick="edit(this)">编辑</button>`
  + 通过布尔值进行条件判断
  + shift() prop()方法的使用
  + 函数封装,重复性代码优化
  + 事件仅对直接作用dom对象生效
  ```
  $('.mask').click(function(event) {
         	if (event.target==this) {
         		cancel();
         	}
  ```
+ on方法
```
        $('.box').on('mouseenter',function(){
            alert('不凡学院')
        })

        // off 方式 解绑事件
        $('button').click(function(){
            $('.box').off('mouseenter');
        })
```
+ 事件委托
```
        // 事件委托 
        // $('ul').on('click','li',function(){
        //     alert($(this).text());
        // })
         //  利用 event 实现
        $('ul').click(function(event){
            // 实际点击的是谁  event.target
            alert($(event.target).text());
        })
```
+ 事件触发
```
$('button').click(function(){
            // $('.box').click();
            $('.box').trigger('click');
            // $('.box').triggerHandler('click');
        })
```
```
 $('.box').click(function(event){
            console.log('我是外部盒子');
            console.log(event)
            console.log('this',this);
            // currentTarget   this  指向一样 事件绑定的对象
            // target  实际触发的对象
            console.log('target',event.target);
            console.log('currentTarget',event.currentTarget);
        })

        // 按键问题
       $('input').keyup(function(event){
        //    keycode 获取点击的 按键  回车===13
            console.log(event.keyCode);
            $('p').text($(this).val());
            // 敲回车背景色变成绿色
            if(event.keyCode == 13){
                $('p').css('background-color','green');
            } 
       })
```
+ 表单
  + 表单最外层,action为提交地址`<form action="http://www.baidu.com" method="get">`
  + 次外层,表单框线`<fieldset></fieldset>`
  + `<legend></legend>`类似表头或标题
  + 具备上传文件功能`<input name="avatar" type="file">	<br>`
  + 下拉框
  ```
  <select name="exp">
    <option value="-1">无</option>
    <option selected value="1">1~3</option>//已选中的
    <option value="2">3~5</option>
                </select><br>
    ```
+ 隐藏表单,页面不显示` <input type="hidden" name="idCard" value="41011111111">`
+ 只读`<input type="text" name="userid" readonly value="1001011">`
+ 灰色显示,状态不可用`<input type="text" name="userid2" disabled value="1001011">`
+ name属性用于给表单(单选/多选)分组,在单选分组内 会出现互斥
```
<label>
        男:<input name="sex" checked type="radio" value="0"> 
    </label>
    <label>
        女:<input name="sex" type="radio" value="1"> <br>
    </label>//增加焦点区域便于点选
```
+ 多行文本`<textarea name="desc"  cols="30" rows="10"></textarea>`
+ 链式编程

  + `$(this).css('width','80px').css('font-size','40px');` 
    + 链式编程原理：return this;  调用”任何”一个方法都是返回了对象本身
    + 通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 this。
+ 大部分情况下是不需要使用each方法的，因为jQuery的隐式迭代特性。
+ 如果要对每个元素做不同的处理，这时候就用到了each方法
```
$('li').each(function(index,ele){
                // ele  当前正在遍历的 dom对象
                // index 当前正在便利的dom对象   的下标
                console.log('index=====>',index);
                console.log('ele=====>',ele);
                // 下标大于3 的 绑定点击事件
                if(index>3){
                    ele.onclick = function(){
                        alert('点击事件')
                    }
                }
            })
```
+ 序号问题解决方案
```
    var deltr =function(index)
    {     

        var _len = $("#tab tr").length;
        $("tr[id='"+index+"']").remove();//删除当前行
        for(var i=index+1,j=_len;i<j;i++)
        	//当前行删除后对后续的表格进行遍历,i代表删除表格的下一行表格,j代表表格总长度
        {   


            var nextTxtVal = $("#desc"+i).val();
            //获取删除行的下一行的输入框内容
            $("tr[id=\'"+i+"\']").replaceWith("<tr id="+(i-1)+" align='center'>"
            	//删除行的下一行和删除行的信息(id,序号,name,下一行文本框内容,onclick事件触发)进行替换
                                +"<td>"+(i-1)+"</td>"
                               +"<td>Dynamic TR"+(i-1)+"</td>"
                                +"<td><input type='text' name='desc"+(i-1)+"' value='"+nextTxtVal+"' id='desc"+(i-1)+"'/></td>"
                                +"<td><a href=\'#\' onclick=\'deltr("+(i-1)+")\'>删除</a></td>"
                            +"</tr>");
       }    
        
    }
