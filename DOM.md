# DOM
## DOM基本概念
DOM是JS操控HTML和CSS的桥梁

DOM（Document Object Model，文档对象模型）是JavaScript操作HTML文档的接口，使文档操作变得非常优雅、简便
DOM最大的特点就是将文档表示为节点树
![](vx_images/381075714238685.png =801x)

### nodeType常用属性值
节点的nodeType属性可以显示这个节点具体的类型
| nodeType值    |节点类型     |
| :-- | :-- |
| 1    |元素节点，例如`<p> `和`<div>`    |
|   3  |文字节点     |
|     8| 注释节点    |
|   9  | document节点    |
|    10 |DTD节点     |


### 访问元素节点
所谓“访问”元素节点，就是指“得到”、“获取”页面上的元素节点
对节点进行操作，第一步就是要得到它
访问元素节点主要依靠document对象

### 认识document对象
document对象是DOM中最重要的东西，几乎所有DOM的功能都封装在了document对象中
document对象也表示整个HTML对象，它是DOM节点树的根
document对象的nodeType属性值是9

#### 访问元素节点的常用方法
|                方法                |         功能          |
| :-------------------------------: | :------------------: |
|     document.getElementById()     |    通过id得到元素     |
|  document.getElementsByTagName()  | 通过标签名得到元素数组 |
| document.getElementsByClassName() |  通过类名得到元素数组  |
|     document.querySelector()      |   通过选择器得到元素   |
|    document.querySelectorAll()    | 通过选择器得到元素数组 |

#### getElementById()
通过id得到元素节点
HTML代码:
    
    <div id="box"> 我是一个盒子</div>
    
    <p id ="para">我是一个段落</p>

JS代码：

 ```
 var box = document.getElementById('box');
 var para = document.getElementById('para');
 ```
 注意事项
 如果页面上有相同id的元素，则只能得到第一个
 不管元素藏得位置有多深，都可以通过getElementById()查找到
 
### 延迟运行
在测试DOM代码时，通常JS代码一定要写到HTML节点的后面，否则JS无法找到相应HTML节点
可以使用window.onload=function(){}事件，使页面加载完毕后，再执行指定的代码

#### getElementByTagName()
getElementByTagName()方法的功能是通过标签名得到节点数组
注意事项
数组方便遍历，从而可以批量操控元素节点
即使页面上只有一个指定标签名的节点，也将得到长度为1 的数组
任何一个节点元素也可以调用getElementByTagName()方法，从而得到其内部的某种类的元素节点

	<body>
		<p>我是段落</p>
		<p>我是段落</p>
		<p>我是段落</p>
		<p>我是段落</p>
		<script type="text/javascript">
			//得到p标签的数组
			var ps =document.getElementsByTagName('p');
			console.log(ps);//[p, p, p, p]
		</script>
	</body>
	

#### getElementsByClassName()
getElementsByClassName()方法的功能是通过类名得到节点数组（class=''中的东西）
某个节点元素也可以调用getElementsByClassName()方法，从而得到其内部的某类名的元素节点

#### querySelector()&querySelectorAll()
querySelector()方法的功能是通过选择器得到元素
```
HTML代码
<div id ="box1">
    <p>我是段落</p>
    <p class="spec">我是段落</p>
    <p>我是段落</p>
</box>

JS代码：
var the_p = document.querrySelector('#box1.spec');
```
注意事项
querySelector()方法只能得到页面上一个元素，如果有多个元素符合条件，则只能得到第一个元素

		<div id="box">
			<p>我是段落</p>
			<p class="spec">我是段落</p>
			<p>我是段落</p>
			<p class="spec">我是段落1</p>
		</div>
		<script type="text/javascript">
			var the_p = document.querySelector('#box .spec');
			var the_p2 = document.querySelector('#box p:nth-child(1)');
			console.log(the_p);
			console.log(the_p2);
		</script>
		
![](vx_images/579952716246718.png =184x)

querySelectorAll()方法
功能是通过选择器得到元素数组
即使页面上只有一个符合选择器的节点，也将得到长度为1的数组

		<ul id ='list1'>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
		</ul>
		<ul id ='list2'>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
			<li>我是li</li>
		</ul>
		
		<script type="text/javascript">
			var lis_inlist1 = document.querySelectorAll('#list1 li');
			console.log(lis_inlist1);//NodeList(6) [li, li, li, li, li, li]
		</script>
		

### 节点的关系
![](vx_images/322773516239387.png =357x)

|     关系      |   考虑所有节点   |
| ------------- | --------------- |
| 子节点         | chileNodes      |
| 父节点         | parentNode      |
| 第一个子节点   | firstChild      |
| 最后一个子节点 | lastChild       |
| 前一个兄弟节点 | previousSibling |
| 后一个兄弟节点 | nextSibling     |

注意：文本节点也属于节点
DOM中，文本节点也属于节点，使用节点的关系时一定要注意

排除文本节点的干扰
|关系     |考虑所有节点     |只考虑元素节点     |
| :-: | :-: | :-: |
|子节点     |childNodes     |children     |
| 父节点    | parentNode    | 同    |
| 第一个子节点    | firstChild    | firstElementChild    |
|最后一个子节点     |lastChild     | lastElementChild    |
| 前一个兄弟节点    | previousSibling    | previousElementSibling    |
|后一个兄弟节点     |nextSibling     |nextElementSibling     |

		<div id="box">
			<p>我是段落A</p>
			<p id="para">我是段落B</p>
			<p>我是段落C</p>
		</div>
		<script type="text/javascript">
			var box =document.getElementById('box');
			var para = document.getElementById("para");
			//所有子节点
			console.log(box.childNodes);
			//所有的元素子节点（IE9开始兼容）
			console.log(box.children);
			
			//第一个子节点
			console.log(box.firstChild);
			console.log(box.firstChild.nodeType);
			//第一个元素子节点
			console.log(box.firstElementChild);
			
			//最后一个子节点
			console.log(box.lastChild);
			console.log(box.lastChild.nodeType);
			//最后一个元素子节点
			console.log(box.lastElementChild);
			
			//父节点
			console.log(para.parentNode);
			
			//前一个兄弟节点
			console.log(para.previousSibling);
			//前一个元素兄弟节点
			console.log(para.previousElementSibling);
			
			//后一个兄弟节点
			console.log(para.nextSibling);
			//后一个元素兄弟节点
			console.log(para.nextElementSibling);
		</script>
		
![](vx_images/434255416235942.png =373x) 

#### 书写常见的节点关系函数

	<body>
		<div id="box">
			<p>我是文本</p>
			<p>我是文本</p>
			<p>我是文本</p>
			<p id="fpara">我是段落fpara</p>
			<p id='para'>
				我是段落para
				<span>1</span>
				<span>2</span>
				<span>3</span>
			</p>
			<p>我是段落C</p>

		</div>
		<script type="text/javascript">
			var box = document.getElementById('box');
			var para = document.getElementById('para');

			//封装一个函数，这个函数可以返回元素的所有子元素节点（兼容IE6），类似children的功能
			function getChildren(node) {
				//结果数组
				var children = [];
				//遍历node这个节点的所有子节点，判断每一个子节点的nodeType属性是不是1
				//如果是1，就推入结果数组
				for (var i = 0; i < node.childNodes.length; i++) {
					if (node.childNodes[i].nodeType == 1) {
						children.push(node.childNodes[i]);
					}
				}
				return children;
			}
			console.log(getChildren(box));
			console.log(getChildren(para));


			//封装一个函数，这个函数可以返回元素的所有子元素节点（兼容IE6），类似previousElementSibling的功能
			function getElementPrevSibling(node) {
				var o = node;
				//使用while语句
				while (o.previousSibling != null) {
					if (o.previousSibling.nodeType == 1) {
						//结束循环，找到了
						return o.previousSibling;
					}

					//让o成为它的前一个节点
					o = o.previousSibling;
				}
				return null;
			}
			console.log(getElementPrevSibling(para));
			console.log(getElementPrevSibling(fpara));
			
			//封装第三个函数，这个函数可以返回元素的所有兄弟节点
			function getAllElementSibling(node){
				//前面的元素兄弟节点
				var prevs = [];
				
				//后面的元素兄弟节点
				var nexts = [];
				
				var o =node;
				//遍历node的前面的节点
				while(o.previousSibling!=null){
					if(o.previousSibling.nodeType ==1){
						prevs.unshift(o.previousSibling);
					}
					o = o.previousSibling;
				}
				o=node;
				//遍历node的后面节点
				while(o.nextSibling!=null){
					if(o.nextSibling.nodeType ==1){
						nexts.push(o.nextSibling);
					}
					o = o.nextSibling;
				}
				//将两个数组进行合并，然后返回
				return prevs.concat(nexts);
				
			}
			
			console.log(getAllElementSibling(para));
		</script>
	</body>
	
![](vx_images/155185820231696.png =360x)

### 节点操作
改变元素节点中的内容可以使用两个相关属性：
①innerHTML   ②innerText
innerHTML属性能以HTML语法设置节点中的内容
innerText属性只能以纯文本的形式设置节点中的内容

		<div id="box">
			
		</div>
		
		<script type="text/javascript">
			var oBox = document.getElementById('box');
			oBox.innerHTML =='笑笑'
			oBox.innerHTML = '<ul><li>笑笑</li><li>小一</li></ul>';
			
			
			oBox.innerText = '笑笑';
			oBox.innerText='<ul><li>笑笑</li><li>小一</li></ul>';
		</script>
		

### 改变节点的css样式
```
oBox.style.backgroundColor = 'red';
oBox.style.backgroundImage='url(images/1.jpg)';
oBox.style.fontSize ='32px';
```

### 改变元素节点的HTML属性
标准W3C属性，如src、href等，只需要直接打点进行更改即可
```
        oImg.src='images/2.jpg';
		<img src="../images/03-01.jpg" id="pic">
		<a href="https://www.baidu.com/"id="link">去百度</a>
		<script type="text/javascript">
			var oPic = document.getElementById('pic');
			var oLink = document.getElementById('link');
			oPic.src = '../images/03-02.jpg';
			oLink.href='https://www.runoob.com/';
			oLink.innerText ='去菜鸟教程';
		</script>
```

不符合W3C标准的属性，要使用setAttribute()和getAttribute()来设置、读取

## 节点的创建
document.createElement()方法用于创建一个指定tagname的HTML元素
```
var oDiv = document.createElement('div');
```
新创建出的节点是“孤儿节点”，这意味着它并没有被挂在DOM树上，我们无法看见它

必须继续使用appendChild()或insertBefore()方法将孤儿节点插入到DOM树上


任何已经在DOM树上的节点，都可以调用appendChild()方法，它可以将孤儿节点挂载到它的内部，成为它的最后一个子节点
```
父节点.appendChild(孤儿节点)；
```

任何已经在DOM树上的节点，都可以调用insertBefore()方法，它可以将孤儿节点挂载到它的内部，成为它的“标杆子节点”之前的节点
```
父节点.insertBefore(孤儿节点，标杆节点);
```

小练习：
请动态创建出一个20行12列的表格
<body>
		<table border="" cellspacing="" cellpadding="" id="mytable">
		</table>
		
		<script type="text/javascript">
			//小练习：请动态创建出一个20行12列的表格
			var mytable =document.getElementById('mytable');
			
			for(var i = 0 ; i<20;i++){
				//创建了新的tr标签
				var tr = document.createElement('tr');
				for(var j = 0; j<12;j++){
					//创建了新的td标签
					var td = document.createElement('td');
					//让tr追加td标签
					tr.appendChild(td);
				}
				//让mytable追加tr标签
				mytable.appendChild(tr);
			}

		</script>

请制作九九乘法表

		<table border="" cellspacing="" cellpadding="" id="mytable">
		</table>
		
		<script type="text/javascript">
			//请创建99乘法表
			var mytable =document.getElementById('mytable');
			
			for(var i = 0 ; i<=9;i++){
				//创建了新的tr标签
				var tr = document.createElement('tr');
				for(var j = 0; j<=i;j++){
					//创建了新的td标签
					var td = document.createElement('td');
					//设置td内部的文字
					td.innerText=i+'乘'+j+'等于'+(i*j);
					//让tr追加td标签
					tr.appendChild(td);
				}
				//让mytable追加tr标签
				mytable.appendChild(tr);
			}

		</script>

### 移动节点
如果将已经挂在到DOM树上的节点成为appendChild()或者insertBefore()的参数，这个节点将会被移动

```
新父节点.appendChild(已经有的父亲的节点);
新父节点.insertBefore(已经有父亲的节点,标杆子节点)；
```
这意味着一个节点不能同时位于DOM树的两个位置
```
	<body>
		<div id="box1">
			<p id="para">爱笑笑</p>
			
		</div>
		<div id="box2">
			<p>我是box2的原有p标签</p>
			<p>我是box2的原有p标签</p>
			<p>我是box2的原有p标签</p>
			<p>我是box2的原有p标签</p>
			<p>我是box2的原有p标签</p>
		</div>
		
		<script type="text/javascript">
			var box1 = document.getElementById('box1');
			var box2 = document.getElementById('box2');
			var para = document.getElementById('para');
			var ps_inbox2= box2.getElementsByTagName('p');
			// box2.appendChild(para);
			
			box2.insertBefore(para,ps_inbox2[0]);
			
		</script>
	</body>
```

### 删除节点
removeChild()方法从DOM中删除一个子节点
```
父节点.removeChild(要删除子节点)；
```
节点不能主动删除自己，必须由父节点删除它
```
		<div id="box">
			<p>我是p节点</p>
		</div>
		<script type="text/javascript">
			var box= document.getElementById('box');
			var the_first_p = box.getElementsByTagName('p')[0];
			box.removeChild(the_first_p);
		</script>
```

### cloneNode()方法可以克隆节点，克隆出的节点是“孤儿节点”
```
var 孤儿节点 = 老节点.cloneNode();
var 孤儿节点 = 老节点.cloneNode(true);
```
参数是一个布尔值，表示是否采用深度克隆：如果为true，则该节点的所有后代节点都会被克隆，如果为false,则只克隆该节点本身

		<div id="box1">
			<ul>
				<li>笑笑</li>
				<li>小一</li>
				<li>徐笑奕</li>
			</ul>
		</div>
		<div id="box2">
			
		</div>
		
		<script type="text/javascript">
			var box1 = document.getElementById('box1');
			var box2 =document.getElementById('box2');
			var theul =box1.getElementsByTagName('ul')[0];
			
			//克隆节点
			var new_ul = theul.cloneNode(true);
			box2.appendChild(new_ul);
			
