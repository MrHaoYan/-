#### 标签
 + rowspan 单元格所占据的行
 + colspan 单元格所占据的列
 + cellspacing 单元格 间距 
 + cellpadding 单元格文本  和单元格边框的间距
 + 表单
        代码
       ```<form action="">用户名: <input type="text"> <br> 密码: <input type="text"></form>```
 + 内联框架
         代码
         ```<iframe src="https://www.baidu.com/" width="800" height="400" frameborder="10"></iframe>```
#### css属性
+ 十六进制 #66AFE4
	 3. rgb(red,green,blue) 0-255
	0 1 2 3 4 5 6 7 8 9 a   b  c  d  e  f
	0 1 2 3 4 5 6 7 8 9 10 11 12 13 14  15
	十六进制  ==> rgb
	66==> 6*16 + 6 == 102
	AF==> a*16 +f == 175
	E4==> e*16 + 4== 14*16 +4  ==228 
	rgba(102,175,228,.5) 带透明度的
+ 单行文本居中方法
 + 单行文本 垂直居中的办法  line-height == 盒子 的高度
+ 行内元素
 + 不会自动换行 
 + 设置宽高 无效-
+ 行内块元素
+ 不会自动换行
 + 设置宽高 有效

+ 第一个值  水平方向 left center right
+ 第二个值  垂直方向 top center  bottom
+ background-position: right center;
+ 垂直方向不写  默认为center
+ background-position: center;
+ 第一个值  距离左边的像素
+ 第二个值   距离上边的像素
+ background-position: 10px 100px;
#### 常见问题
+ margin问题
 + 垂直方向上的 margin 会出现重叠现象,谁大 谁生效
 + 两个盒子发生嵌套的时候，给子类设置maring会给父类造成一种崩塌现象，子类的margin-top没有效果，而直接作用到父类
 + 解决办法
  + 给父类  增加  overflow:hidden;
  + 给父类盒子 加一个 极小的padding
 + display:none; 隐藏,不占据文档位置
 + visibility: hidden;隐藏,占据文档位置
 + 块级元素和行内元素都可以浮动，当一个行内元素浮动以后将会自动变为一个块级元素.
当一个块级元素浮动以后，宽度会默认被内容撑开，所以当漂浮一个块级元素时我们都会为其指定一个宽度。
+ 浮动的影响
 + 元素浮动以后即完全脱离文档流，这时不会再影响父元素的高度。也就是浮动元素不会撑开父元素
 + 如何解决
 + 代码如下
 ```.main+
			/*height: 600px;*/
			background-color: pink;
			/*清除浮动的影响*/
			/*overflow: hidden;*/
		}
 ```
 ```.clr{
			/*清除浮动的影响,父元素下设置一个空盒子*/
			/*clear: both;*/
		}
```
#### 使用技巧
##### 块状垂直居中.
 + 不知道父盒子高度的情况下,可以用transform
 + html代码如下
 ```.son{
			top:50%;
			transform: translateY(-50%);
		}```
 + css代码如下
 ```.son{
			top:50%;
			trans+orm: translateY(-50%);
		}```

+ 同理水平方向用translateX()

##### 分液器

 + 按钮有种水波扩散的效果.
 + 对box里的a标签设置分液器如下.

 ```.box{
			height: 50px;
			width: 50px;
			background-color:pink;
		}
		a{
			display: block;
			width: 8px;
			height: 8px;
			background-color:yellow;
			border: 3px solid transparent;
			border-radius: 50%; 
			background-clip: content-box;
		}
		a:hover{
			border-color: yellow;
			background-color: white;
		}```
#### 对transform的匀速运动.

 + 对一个盒子hover,如长宽或位置发生变化,都可以匀速处理.
 + html代码如下.

```<div class="box">
		<div class="son"></div>
	</div>```
 +css代码如下.
  ```.box{
			width: 800px;
			height: 200px;
			background-color:pink;
		}
		.son{
			width: 200px;
			height: 200px;
			background-color: yellow;
		}
		.box:hover .son{
			transform: translateX(600px);
			transition: all 4s ease;
		}```

+ z-index可以指定一个整数作为参数，值越大元素显示的优先级越高，也就是z-index值较大的元素会显示在网页的最上层.

+ 对span设置text-indent没有起作用，是因为text-indent只能给块级元素设置。
但是如果让span{display:block}转换为块级元素，就会换行，还得通过浮动来控制，增加了麻烦。所以改css为span{display:inline-block;}。

+ 对span设置text-indent没有起作用，是因为text-indent只能给块级元素设置。
但是如果让span{display:block}转换为块级元素，就会换行，还得通过浮动来控制，增加了麻烦。所以改css为span{display:inline-block;}。

