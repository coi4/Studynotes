课程路线：

![屏幕截图 2023-10-13 092351](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-13%20092351.png)

> web：全球广域网，万维网，能够通过浏览器访问的网站

- web网站的开发模式（主流）

  ![image-20231013094039043](https://gitee.com/coi4/test/raw/master/img/image-20231013094039043.png)

  ![屏幕截图 2023-10-13 092139](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-13%20092139.png)

## 一、前端Web开发

![](https://gitee.com/coi4/test/raw/master/img/image-20231013122748302.png)

不同的浏览器，内核不同，对于相同的前端代码解析的效果会存在差异。

![image-20231013122513342](https://gitee.com/coi4/test/raw/master/img/image-20231013122513342.png)

### 1、HTML-CSS

HTML：超文本标记语言

> 超文本：超越了文本的限制，比普通文本更强大。除了文字信息，还可以定义图片、音频、视频等内容。
>
> 标记语言：由标签构成的语言

![image-20231013123620004](https://gitee.com/coi4/test/raw/master/img/image-20231013123620004.png)

CSS：层叠样式表，用于控制页面的样式（表现）

文档查阅：w3school网

#### 1.1、使用软件

VScode（官网下载）——提供了非常强大的插件库（下载插件）

* 建议以后安装所有与开发相关的软件，尽量安装在一个**没有中文，不带空格的目录**下

#### 1.2、基础标签&样式

第一步：!回车

注释：<！--             -->

alt+B：打开默认浏览器

写完要保存

##### 1.2.1、标题

###### 1.2.1.1、标题排版

> * 图片标签：<img> < img src="…" width="…" height="…">
>   * src ：指定图像的url（./ : 当前目录, ../ : 上级目录）
>   * width：图像的宽度
>   * height：图像的高度
> * 标题标签：<h1-h6>
> * 水平线标签：<hr>
> * 没有语义的布局标签：<span>(一行可以显示多个(组合行内元素)，宽度和高度默认由内容撑开)

###### 1.2.1.2、标题样式

```
<font color=""></font>
```

css引入方式：

> * 行内样式：写在标签的style属性中（不推荐）![image-20231013190027052](https://gitee.com/coi4/test/raw/master/img/image-20231013190027052.png)
> * 内嵌样式：写在style标签中（可以写在页面任何位置，但通常约定写在head标签中）![image-20231013190047693](https://gitee.com/coi4/test/raw/master/img/image-20231013190047693.png)
> * 外联样式：写在一个单独的.css文件中（需要通过 link 标签在网页中引入）![image-20231013190120228](https://gitee.com/coi4/test/raw/master/img/image-20231013190120228.png)

颜色表示：

> * 关键字: red、green . . .
> * rgb表示法：rgb(255,0,0)、rgb(134,100,89) 
> * 十六进制: #ff0000、#cccccc、#ccc

颜色属性：

> * color: 设置文本内容的颜色

css选择器：

选择器：选取需设置样式的元素（标签）；业务场景不同，选择的标签的需求也多种多样

优先级（id>类>元素）

> - 元素选择器：![image-20231013191645825](https://gitee.com/coi4/test/raw/master/img/image-20231013191645825.png)
> - id选择器：![image-20231013191719278](https://gitee.com/coi4/test/raw/master/img/image-20231013191719278.png)
> - 类选择器：![image-20231013191739471](https://gitee.com/coi4/test/raw/master/img/image-20231013191739471.png)

###### 1.2.1.3、超链接

标签：    ![image-20231013193540926](https://gitee.com/coi4/test/raw/master/img/image-20231013193540926.png)

> * href：指定资源访问的url
> * target：指定在何处打开资源链接
>   * _self:默认值，在当前页面打开
>   * _blank: 在空白页面打开

##### 1.2.2、正文

###### 1.2.2.1、正文排版

标签：

> * 视屏标签：<video>
>   * src：规定视频的url
>   * controls：显示播放控件
>   * width
>   * height
> * 音频标签：<audio>
>   * src
>   * controls
> * 段落标签：<p>
> * 文本加粗标签：<b>/<strong>（强调）
> * 倾斜：i/em
> * 下划线：u/ins
> * 删除线：s/del
> * 换行：<br>

css属性：

> line-height：设置行高px
>
> text-indent：定义第一个行内容的缩进加px
>
> text-align：规定元素中的文本的水平对齐方式right/left/center
>
> font-size：字体大小 （注意：记得加px）
>
> text-decoration：规定添加到文本的修饰，none表示定义标准的文本

注意：在HTML中无论输入多少个空格，只会显示一个。 可以使用空格占位符：

```
&nbsp;
```

![img](https://gitee.com/coi4/test/raw/master/img/_-1759569315__25d7024d5d02f80281234f84065d6079_817726398_Screenshot_20231013_203921_0_xg_0.jpg)

###### ？1.2.2.2、页面布局

使页面离边界有一定距离

- 盒子：页面中所有的元素（标签），都可以看做是一个 盒子，由盒子将页面中的元素包含在一个矩形区域内，通过盒子的视角更方便的进行页面布局

- 盒子模型组成：内容区域（content）、内边距区域（padding）、边框区域（border）、外边距区域（margin）

  ![image-20231013200311560](https://gitee.com/coi4/test/raw/master/img/image-20231013200311560.png)

标签：

> 实际开发网页中，会大量频繁的使用 div 和 span 这两个没有语义的布局标签。
>
> * div标签：
>   * 一行只显示一个（独占一行）
>   * 宽度默认是父元素的宽度，高度默认由内容撑开
>   * 可以设置宽高（width、height）
> * span标签：
>   * 一行可以显示多个
>   * 宽度和高度默认由内容撑开
>   * 不可以设置宽高（width、height）

css属性：

> width：
>
> height
>
> border：设置边框的属性，如：1px solid #000；
>
> padding：内边距
>
> margin：外边距
>
> 如果只需要设置某一个方位的边框、内边距、外边距，可以在属性名后加上 –位置，如：padding-top、padding-left、padding-right …

#### 1.3、表格、表单标签

##### 1.3.1、表格标签

场景：在网页中以表格形式整齐展示数据

标签：

> * 《table》:定义表格整体，可包裹多个tr
>   * border
>   * width
>   * cellspacing：规定单元之间的空间
> * 《tr》：表格的**行**，可包含多个《td》
> * 《td》：表格单元格，可包裹内容，如果是表头单元格，可换成《th》

##### 1.3.2、表单标签

场景：在网页中主要负责数据采集功能，如 注册、登录等数据采集

![image-20231013202317086](https://gitee.com/coi4/test/raw/master/img/image-20231013202317086.png)

标签：

```
<form>
```

表单项：

```
<input>:定义表单项，通过type属性控制输入形式
<select>：定义下拉列表
<textarea>：定义文本域；属性：cols+“”，row=“10”
<option>：定义列表项
<label>:选项用+value=“”多重复记录
```

属性：

```
action：表单数据提交的url地址
method：表单提交方式，常见为GET、POST
       GET：表单数据拼接在url后，url中能携带的表单数据大小有限制
       POST：表单数据是在请求体（消息体）中携带的，大小没有限制
checked:初始化选中（ture/false）
```

input的type属性：

+name=“”

```
text：定义单行的输入字段
password：定义密码字段
radio：定义单项按钮
checkbox：定义复选框
file：定义文件上传按钮
date/datetime-local/time：定义日期/时间/日期时间
number：定义数字输入框
emial：定义邮件输入框
hidden：定义隐藏框
submit/reset/button：定义提交按钮/重置按钮/可点击按钮+value=“”显示按钮文字
```

### 2、Javascript

> * JavaScript（js）：是一门跨平台、面向对象的脚本语言。是用来控制网页行为的，它能**使网页可交互**。
> * 在 1995 年由 Brendan Eich 发明，并于 1997 年成为 ECMA 标准。
> * ECMAScript6 (ES6) 是最主流的 JavaScript 版本（发布于 2015 年)。
> * ECMA：ECMA国际（前身为欧洲计算机制造商协会），制定了标准化的脚本程序设计语言 ECMAScript，这种语言得到广泛应用。而JavaScript是遵守ECMAScript的标准的。

#### 2.1、引入方式

> * 内部脚本：将JS代码定义在html页面的<script></script>中
>   * 建议：将<script></script>放在<body>的底部
>
> * 外部脚本：将JS代码定义在js文件中，通过<script></script>标签引入src
>   - 注意：通过<script>标签引入外部js文件时，标签不可以自闭合，必须是双标签
>   - js文件中不包含<script>标签

#### 2.2、基础语法

##### 2.2.1、书写语法

注释、代码块与java差不多，结尾分号可有可无

输出语句：

```
window.alert():写入警告框
document.write():写入HTML输出
console.log():写入浏览器控制台
```

![image-20231013234736718](https://gitee.com/coi4/test/raw/master/img/image-20231013234736718.png)

##### 2.2.2、变量

* 声明：
  * var：声明变量，全局作用域/函数作用域，允许重复声明
  *  let：声明变量，块级作用域，不允许重复声明
  *  const：声明常量，一旦声明，常量的值不能改变
* 弱类型语言，变量可以存放不同类型的值 ![image-20231013235056438](https://gitee.com/coi4/test/raw/master/img/image-20231013235056438.png)
* 变量名规则：
  * 组成字符可以是任何字母、数字、下划线（_）或美元符号（$）
  * 数字不能开头
  * 建议使用驼峰命名

##### 2.2.3、数据类型、运算符、流程控制语句

使用 typeof 运算符可以获取数据类型![image-20231013235549932](https://gitee.com/coi4/test/raw/master/img/image-20231013235549932.png)

* 原始类型：
  * number：数字（整数、小数、NaN(Not a Number)）
  * string：字符串，单双引皆可
  * boolean：布尔。true，false
  *  null：对象为空
  *  undefined：当声明的变量未初始化时，该变量的默认值是 undefined
* 引用类型：
* 运算符：与Java差不多，但js中== 会进行类型转换，=== 不会进行类型转换，类型不一致，返回false
* 类型转换：
  * 字符串 转 数字：parselnt（“12A45”）//12
  * 其他类型转为boolean
  * 0，null，undefined，“”，NaN理解成false
* 流程控制语句：if…else if …else…、switch、for 、while、do … while![image-20231013235837647](https://gitee.com/coi4/test/raw/master/img/image-20231013235837647.png)

#### 2.3、函数

* 通过function关键字定义![image-20231014001128874](https://gitee.com/coi4/test/raw/master/img/image-20231014001128874.png)

* 形参不需要类型，返回值也不需要
* 调用：函数名称![image-20231014001232779](https://gitee.com/coi4/test/raw/master/img/image-20231014001232779.png)
* 方式二：![image-20231014001337032](https://gitee.com/coi4/test/raw/master/img/image-20231014001337032.png)

#### 2.4、对象

##### 2.4.1、Array

用于定义数组，可以存储任意的类型的数据。

* 定义：![image-20231014001639020](https://gitee.com/coi4/test/raw/master/img/image-20231014001639020.png)
* 访问：![image-20231014001707607](https://gitee.com/coi4/test/raw/master/img/image-20231014001707607.png)
* 属性：
  
  * length：设置或返回数组中元素的数量
* 方法：
  * forEach（）：遍历数组中的每个有值的元素，并调用一次传入的函数
  
    ```
    arr.forEach(function(e){
    {
    console.log(e)
    })
    
    arr.forEach((e)=>{
    console.log(e)
    })
    ```
  
    
  
  * push（）：将新元素添加到数组的末尾，并返回新的长度
  
  * splice（）：从数组中删除元素
  
    ```
    arr.splice(2,2)
    //元素3和4被删除（从索引2的位置开始删，删两个）
    ```
  
    

**箭头函数**(ES6)**：**是用来简化函数定义语法的。具体形式为: (…) => { … } ，如果需要给箭头函数起名字： var xxx = (…) => { … }

##### 2.4.2、String

* 字符串创建对象方式：![image-20231014002422733](https://gitee.com/coi4/test/raw/master/img/image-20231014002422733.png)
* 属性：
  * length：字符串的长度
* 方法：
  * charAt（）：返回在指定位置的字符
  * indexOf（）：检索字符串（返回索引）
  * trim（）：去除字符串两边的空格
  * substring（）：提取字符串中两个指定的索引号之间的字符，含头不含尾

##### 2.4.3、JSON

js自定义对象
- 定义：![image-20231014002829508](https://gitee.com/coi4/test/raw/master/img/image-20231014002829508.png)![image-20231014003054755](https://gitee.com/coi4/test/raw/master/img/image-20231014003054755.png)

  ```
  function可简化成：
  eat(){
  alert("用膳")
  }
  ```

  

- 调用：![image-20231014002917772](https://gitee.com/coi4/test/raw/master/img/image-20231014002917772.png)![image-20231014003040432](https://gitee.com/coi4/test/raw/master/img/image-20231014003040432.png)

json，js对象标记法

是通过 JavaScript 对象标记法书写的文本

经常用来作为前后台交互的数据载体，xml文档的替代

- json基础语法
  - 定义：![image-20231014004049944](https://gitee.com/coi4/test/raw/master/img/image-20231014004049944.png)
  - JSON字符串转为js对象：![image-20231014004218782](https://gitee.com/coi4/test/raw/master/img/image-20231014004218782.png)
  - js对象转为JSON字符串：![image-20231014004235181](https://gitee.com/coi4/test/raw/master/img/image-20231014004235181.png)

##### 2.4.4、BOM

浏览器对象模型，允许JavaScript与浏览器对话， JavaScript 将浏览器的各个组成部分封装为对象。要操作浏览器的部分功能，可通过操作BOM对象的相关属性或者函数来完成

- 对象：

![image-20231014004601098](https://gitee.com/coi4/test/raw/master/img/image-20231014004601098.png)

```
var i=0;
setlnterva(function(){
i++;
console.log("定时器执行了“+i"次“)
}，2000)；
//每隔一段时间弹出
```

![image-20231014004629085](https://gitee.com/coi4/test/raw/master/img/image-20231014004629085.png)

##### 2.4.5、DOM

将html的每一个标签都封装成一个对象

主要作用：

- 改变HTMl元素内容
- 改变HTML元素的样式
- 对HTMLDOM事件作出反应
- 添加和删除HTML元素

从而达到动态改变页面效果目的

![image-20231014004734693](https://gitee.com/coi4/test/raw/master/img/image-20231014004734693.png)

* 获取Element

  ```
  //根据id属性值获取，返回单个Element对象
  document.getElementByld()
  //根据标签名称获取，返回Element对象数组
  document.getElementsByTagName()
  //根据name属性值获取，返回Element对象数组
  document.getElementsByName()
  //根据class属性值获取，返回Element对象数组
  document.getElementByClassName()
  ```

* 操作Element对象的属性，查文档知可通过div标签对象的innerHTML属性修改标签内容

  ```
  var divs=document.getElementsByClassName('cls')
  var div1=divs[0];
  div1.innerHTML="传智教育666"
  ```

###### 2.4.5.1、案例

> 1.点亮灯泡
>
> 2.将所有的div标签的标签体内容后面加上：very good
>
> 3.使所有的复选框呈现被选中的状态

```
var img=document.geElementtById("h1");
img.arc="";

var divs=document.getElementByTagName("div");
for(let i=0;i<divs.length;i++){
const div=divs[i]
div.innerHTML+=<font color='red'>very good</font>
}

var ins=document.getElementByName("hobby");
for(var i=0;i<check.lenth;i++){
const check=ins[i]
check.checked=ture;
}
```



#### 2.5、事件监听

事件：HTML事件是发生在HTML元素上的 “事情”,如按钮被点击、鼠标移动到元素上、按下键盘按键

事件监听：JavaScript可以在事件被侦测到时 执行代码。

##### 2.5.1、事件绑定

* 方式一：通过 HTML标签中的事件属性进行绑定

  ```
  <input type="button" onclick="on()" value="按钮1">
  
  <script>
      function on(){
          alert('我被点击了!');
      }
  </script>
  ```

* 方式二：通过 DOM 元素属性绑定

  ```
  <input type="button" id="btn" value="按钮2">
  
  <script>
      document.getElementById('btn').onclick=function(){
          alert('我被点击了!');
      }
  </script>
  
  ```


##### 2.5.2、常见事件

| 事件名      | 说明                     |
| ----------- | ------------------------ |
| onclick     | 鼠标单击事件             |
| onblur      | 元素失去焦点             |
| onforce     | 元素获得焦点             |
| onload      | 某个页面或图像被完成加载 |
| onsubmit    | 当表单提交时触发该事件   |
| onkeydown   | 某个键盘的键被按下       |
| onmouseover | 鼠标被移到某元素之上     |
| onmouseout  | 鼠标从某元素移开         |

##### 2.5.3、案例

> 1.点击 “点亮”按钮 点亮灯泡，点击“熄灭”按钮 熄灭灯泡。
>
> 2.输入框鼠标聚焦后，展示小写；鼠标离焦后，展示大写。
>
> 3.点击 “全选”按钮使所有的复选框呈现被选中的状态，点击 “反选”按钮使所有的复选框呈现取消勾选的状态

```
<input type="button" value="点亮" onclick="on()">
function on(){
var img=document.getElementById("light")
img.arc="";
}

 <input type="text" id="" value="" onfocus="lower()" onblur="upper()">
 function lower(){
 var input=document.getElementById("")
 input.value=input.value.toLowerCase();
 }
 function upper(){
 var input=document.getElementById("")
 input.value=input.value.toUpperCase();
 }
 
 <input type="button" value="全选" onclick="checkAll()">
 function checkAll(){
 var hobbys=document.getElementByName("");
 for(let i=0;i<hobbys.length;i++){
 const check=hobbys[i];
 check.checked=ture;
 }
 }
```



### 3、Vue

- Vue 是一套前端框架，**免除原生JavaScript中的DOM操作**，简化书写。
- 基于MVVM(Model-View-ViewModel)思想，**实现数据的双向绑定，将编程的关注点放在数据上**。
- 框架：是一个半成品软件，是一套可重用的、通用的、软件基础代码模型。基于框架进行开发，更加快捷、更加高效。
- Model：数据模型，特指前端中通过请求从后台获取的数据
- View：视图，展示数据的页面

#### 3.1、快速入门

* 新建HTML页面，引入Vue.js文件![image-20231014084842793](https://gitee.com/coi4/test/raw/master/img/image-20231014084842793.png)

* 在JS代码区域，创建Vue核心对象，定义数据模型![image-20231014084857191](https://gitee.com/coi4/test/raw/master/img/image-20231014084857191.png)

  * 创建vue对象时，常用的属性
    * el：指定哪些标签受Vue管理，app是受管理标签的属性值
    * data：定义数据模型
    * methods：定义函数

* 编写视图![image-20231014084909143](https://gitee.com/coi4/test/raw/master/img/image-20231014084909143.png)

  ![image-20231014085022665](https://gitee.com/coi4/test/raw/master/img/image-20231014085022665.png)

#### 3.2、常用指令

指令：HTML 标签上带有 v- 前缀 的特殊属性，不同指令具有不同含义。例如：v-if，v-for…

![image-20231014085151619](https://gitee.com/coi4/test/raw/master/img/image-20231014085151619.png)

![image-20231014085332792](https://gitee.com/coi4/test/raw/master/img/image-20231014085332792.png)

![image-20231014085353025](https://gitee.com/coi4/test/raw/master/img/image-20231014085353025.png)

![image-20231014085532805](https://gitee.com/coi4/test/raw/master/img/image-20231014085532805.png)

通过v-bind或者v-model绑定的变量，必须在数据模型中声明。

![image-20231014085627762](https://gitee.com/coi4/test/raw/master/img/image-20231014085627762.png)

![image-20231014085816932](https://gitee.com/coi4/test/raw/master/img/image-20231014085816932.png)

![image-20231014085828655](https://gitee.com/coi4/test/raw/master/img/image-20231014085828655.png)

v-if指令，不满足条件的标签代码直接没了，而v-show指令中，不满足条件的代码依然存在，只是添加了css样式来控制标签不去显示。

![image-20231014085901058](https://gitee.com/coi4/test/raw/master/img/image-20231014085901058.png)

##### 3.2.1、案例

![image-20231014090031014](https://gitee.com/coi4/test/raw/master/img/image-20231014090031014.png)

#### 3.3、生命周期

生命周期：指一个对象从创建到销毁的整个过程。

生命周期的八个阶段：每触发一个生命周期事件，会自动执行一个生命周期方法(钩子)。

![image-20231014090404446](https://gitee.com/coi4/test/raw/master/img/image-20231014090404446.png)

![image-20231014090422774](https://gitee.com/coi4/test/raw/master/img/image-20231014090422774.png)

mounted：挂载完成，Vue初始化成功，HTML页面渲染成功。（发送请求到服务端，加载数据）

```
mounted(){

}
```



### 4、vue-Element

#### 4.1、Ajax

异步的JS和xml

![屏幕截图 2023-10-14 170512](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-14%20170512.png)

作用：

- 数据交换：通过Ajax可以给服务器发送请求，并获取服务器响应的数据。
- 异步交互：可以在不重新加载整个页面的情况下，与服务器交换数据并更新部分网页的技术，如：搜索联想、用户名是否可用的校验等等。

##### 4.1.2、Axios

Axios是对原生的Ajax进行封装，简化书写，快速开发

Axios官网：https://www.axios-http.cn

###### 4.1.2.1、快速入门

![image-20231014171105734](https://gitee.com/coi4/test/raw/master/img/image-20231014171105734.png)

> method属性：用来设置请求方式的
>
> data属性：作为请求体被发送的数据；如果是post请求，数据需要作为data属性的值
>
> then（）需要传递一个匿名函数。该匿名函数被称为回调函数，意思是该匿名函数在发送请求时不会被调用，而是在成功响应后调用的函数。而该回调函数中result参数是对相应的数据进行封装的对象，通过result.data可以获取到相应的数据
>

- 请求方式：

  ```
  axios.get(url[,config])
  axios.delete(url[,cinfig])
  axios.post(url [,data[config]])
  axios.put(url [,data[config]])
  ```

  ![屏幕截图 2023-10-14 171533](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-14%20171533.png)

###### 4.1.2.2、案例

> 1.数据准备的url： http://yapi.smart-xwork.cn/mock/169327/emp/list
>
> 2.在页面加载完成后，自动发送异步请求，加载数据，渲染展示页面(性别：1 代表男，2 代表女)。

```
1.创建文件，提前准备基础代码，包括表格以及vue.js和axios.js文件的引入
2.在vue的mounted钩子函数中发送Ajax请求获取数据
3.拿到数据，绑定给vue的data属性
4.标签上通过v-for遍历数据，展示数据
```

```
<table border="1" cellspacing="0" width="60%">

<script>
new vue{
    el:#app,
    data:{
        emps:[]
    },
    mounted(){
         axios.get("").then(result=>{
             console.log(result.data);
                  this.emps=result.data.data;
         })
    }
}
```



#### 4.2、前后端分离开发

为了保证前后端数据格式一致，都需要遵循**接口文档**进行开发；接口文档示可以查询今天提供**资料/接口文档示例**里面的资料；接口文档的内容是后台开发者根据产品经理提供的产品原型和需求文档所撰写出来的，产品原型示例可以参考今天提供**资料/页面原型**里面的资料。

![image-20231014174021330](https://gitee.com/coi4/test/raw/master/img/image-20231014174021330.png)

![image-20231014174103993](https://gitee.com/coi4/test/raw/master/img/image-20231014174103993.png)

> 1. 需求分析：首先我们需要阅读需求文档，分析需求，理解需求。
> 2. 接口定义：查询接口文档中关于需求的接口的定义，包括地址，参数，响应数据类型等等
> 3. 前后台并行开发：各自按照接口文档进行开发，实现需求
> 4. 测试：前后台开发完了，各自按照接口文档进行测试
> 5. 前后段联调测试：前段工程请求后端工程，测试功能

YApi

* 用来撰写接口文档的平台
*  http://yapi.smart-xwork.cn/

功能：

- API接口管理：根据需求撰写接口，包括接口的地址，参数，响应等等信息。
- Mock服务：模拟真实接口，生成接口的模拟测试数据，用于前端的测试。

YApi对于接口的配置步骤：

![img](https://gitee.com/coi4/test/raw/master/img/3AB2FAEBDF9D07F563EC9DA6DBFC96BB.png)

![img](https://gitee.com/coi4/test/raw/master/img/B29261740D95CCCB20A45C6E7AD190C6.png)

![img](https://gitee.com/coi4/test/raw/master/img/9308E91B771CB28390DE7CE1A6DC2C32.png)

![img](https://gitee.com/coi4/test/raw/master/img/D280C4BFF9FA26F469972625012318E0.png)

![img](https://gitee.com/coi4/test/raw/master/img/B5E47BE00D93EDDE82241FE23877754A.png)

![img](https://gitee.com/coi4/test/raw/master/img/82FA6CD1BB464155226D484214F69AF7.png)

![img](https://gitee.com/coi4/test/raw/master/img/072878AA68774DC7FBC4016FA1EEB1A6.png)

![img](https://gitee.com/coi4/test/raw/master/img/94081DB275419F90E5A6F5A7297427B0.png)

![img](https://gitee.com/coi4/test/raw/master/img/E409C5AAB728E57D69F442149A4F04C3.png)

#### 4.3、前端工程化

在企业级的前端项目开发中，把前端开发所需的工具、技术、流程、经验等进行规范化、标准化。

![image-20231014174727460](https://gitee.com/coi4/test/raw/master/img/image-20231014174727460.png)

> - 模块化：将js和css等，做成一个个可复用模块
> - 组件化：我们将UI组件，css样式，js行为封装成一个个的组件，便于管理
> - 规范化：我们提供一套标准的规范的目录接口和编码规范，所有开发人员遵循这套规范
> - 自动化：项目的构建，测试，部署全部都是自动完成

##### 4.3.1、环境准备

* 介绍： Vue-cli 是Vue官方提供的一个**脚手架**，用于**快速生成一个 Vue 的项目模板**。
* Vue-cli提供了如下功能：
  * 统一的目录结构
  * 本地调试
  * 热部署
  * 单元测试
  * 集成打包上线
* 依赖环境：NodeJS 

1. 安装NodeJS
2. 安装vue-cli

##### 4.3.2、Vue项目简介

1. Vue项目创建

   - 命令行：![image-20231014175441977](https://gitee.com/coi4/test/raw/master/img/image-20231014175441977.png)

   - 图形化界面：通过命令先进入到图形化界面，然后再进行vue工程的创建![image-20231014175455923](https://gitee.com/coi4/test/raw/master/img/image-20231014175455923.png)

     ![img](https://gitee.com/coi4/test/raw/master/img/059ED6DA44D41237AC4538C1257E0358.png)

     ![img](https://gitee.com/coi4/test/raw/master/img/1839514B5FA442961731E22F3CD41376.png)

     ![img](https://gitee.com/coi4/test/raw/master/img/7D6225A34ADF75634F5B2483C6774CD5.png)

     ![img](https://gitee.com/coi4/test/raw/master/img/04EB6FD6E9D54021EAF5064B2B09F802.png)

     ![img](https://gitee.com/coi4/test/raw/master/img/12A197476C396E6DA131F52BFDCDE0C7.png)

2. 目录构建

   - 基于Vue脚手架创建出来的工程，有标准的目录结构，如下：

     ![image-20231014175637792](https://gitee.com/coi4/test/raw/master/img/image-20231014175637792.png)

![image-20231014175655859](https://gitee.com/coi4/test/raw/master/img/image-20231014175655859.png)

​    3.启动

- 方式一：

![img](https://gitee.com/coi4/test/raw/master/img/95B9C3F3EE2DAABACB7CD9DEAADDB81F.png)

修改：热更新---只要保存更新的代码，直接打开浏览器，不需要做任何刷新，页面呈现内容发生变化

![img](https://gitee.com/coi4/test/raw/master/img/B430680B37882D25521449101348CF4F.png)

- 方式二：

![img](https://gitee.com/coi4/test/raw/master/img/023AEF0BEE08A327EC83036371728142.png)

  4.配置端口

8080端口，经常被占用，可以去修改默认的8080端口。修改vue.config.js文件的内容，添加如下代码：

![img](https://gitee.com/coi4/test/raw/master/img/2B717804129E7709FD498A93C0E11695.png)

关闭服务器，重新启动

 5.NPM脚本窗口调试：

![img](https://gitee.com/coi4/test/raw/master/img/15B8A35E26009E22A16A2525E51E3874.png)

重新启动VS Code，

![img](https://gitee.com/coi4/test/raw/master/img/EBC3ACE9B35DF3FA71EB64579A9855A4.png)

##### 4.3.3、Vue项目开发流程

index.html文件默认引入入口函数main.js文件

![image-20231014180856789](https://gitee.com/coi4/test/raw/master/img/image-20231014180856789.png)

> import：导入指定文件，并重新起名（import App from  '. /App.vue')导入当前目录下的App.vue文件并起名为App
>
> $mount('#app'):将vue对象创建的dom对象挂在id=app的标签区域中，作用与之前的le属性一致
>
> router：路由
>
> render：主要使用视图的渲染的
>
> template：模板部分，主要是HTML代码，用来展示页面主体结构的
>
> script：js代码区域，主要是通过js代码来控制模板的数据来源和行为的
>
> style：css样式部分，主要通过css样式控制模板的页面效果的

Vue的组件文件以 .vue结尾，每个组件由三个部分组成：<template> 、<script>、<style> 。

#### 4.4、Vue组件库Element

ElementUI主要用于开发美观的页面（后台开发者只需要学会从ElementUI的官网拷贝组件到我们自己的页面中，并做一些修改即可）

Element：是饿了么团队研发的，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库；用于快速构建网页。

组件：组成网页的部件，例如 超链接、按钮、图片、表格、表单、分页条等等。

官网：[https://element.eleme.cn/#/zh-CNListener](https://element.eleme.cn/)

##### 4.4.1、快速入门

1. 安装ElementUI组件库 （在当前工程的目录下），在命令行执行指令：	![image-20231014181410153](https://gitee.com/coi4/test/raw/master/img/image-20231014181410153.png)

   ![img](https://gitee.com/coi4/test/raw/master/img/FF0AD4B6A9582D9FAE648563CD0ABD1C.png)

2. 在main.js中引入ElementUI组件库：代码--![image-20231014181508376](https://gitee.com/coi4/test/raw/master/img/image-20231014181508376.png)

   ![img](https://gitee.com/coi4/test/raw/master/img/B2CC8286E237AEB2EF37EB81F929BBBB.png)

3. 按照vue项目的开发规范，在src/views目录下创建一个vue组件文件，名称后缀为.vue，并在组件文件中编写：

   - ```
     <template>
     </template>
     <script>
     export default{
     
     }
     </script>
     <style>
     </style>
     ```

   - ![img](https://gitee.com/coi4/test/raw/master/img/373E14AE4D38212F9E1CB2DBEAD44508.png)

4. 访问官网，复制组件代码，调整

   - ![img](https://gitee.com/coi4/test/raw/master/img/94C3713091E1A46FCFDAAB50EE0C54EB.png)
   - ![img](https://gitee.com/coi4/test/raw/master/img/C04FCC0A6C01DFEB806C8F18A5BCC4CF.png)

5. 在需要默认访问的根组件src/App.vue中引入自定义组件：

   - ![img](https://gitee.com/coi4/test/raw/master/img/FD157F518D919AB035D40ADE848BD189.png)

##### 4.4.2、常见组件

* Table 表格：用于展示多条结构类似的数据，可对数据进行排序、筛选、对比或其他自定义操作

  * 如果官方有除了template部分之外的style和script都需要复制
  * ![img](https://gitee.com/coi4/test/raw/master/img/22C44E3778AB37B5DC0E66DE46B35A25.png)
  * 组件属性详解：ElementUI通过属性将数据模型绑定到视图
    * ![img](https://gitee.com/coi4/test/raw/master/img/1012966AE3F5D2E9D958CC71790FDDA8.png)
    * data: 主要定义table组件的数据模型
    * prop: 定义列的数据应该绑定data中定义的具体的数据模型
    * label: 定义列的标题
    * width: 定义列的宽度

* Pagination 分页：当数据量过多时，使用分页分解数据

  * 属性详解：

    * background: 添加北京颜色，也就是上图蓝色背景色效果。
    * layout: 分页工具条的布局，其具体值包含`sizes`, `prev`, `pager`, `next`, `jumper`, `->`, `total`, `slot` 这些值
    * ![img](https://gitee.com/coi4/test/raw/master/img/4A35BCCFBF970851B2BC7066CC52FFBD.png)
    * total: 数据的总数量

  * 事件详解：

    * size-change ： pageSize 改变时会触发 （每页条数）

    * current-change ：currentPage 改变时会触发（当前页）

    * ```
      //template：
      <!-- Pagination分页 -->
      <el-pagination
                     @size-change="handleSizeChange"
                     @current-change="handleCurrentChange"
                     background
                     layout="sizes,prev, pager, next,jumper,total"
                     :total="1000">
      </el-pagination>
      
      //script：methods与data同级
      methods: {
            handleSizeChange(val) {
              console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
              console.log(`当前页: ${val}`);
            }
          },
      ```

* Dialog 对话框：在保留当前页面状态的情况下，**告知用户并承载相关操作**。

  * 属性详解：
    * visible.sync ：是否显示 Dialog 
    * 点击按钮，触发事件，修改属性值为true
    * 默认为true，需要在data中声明为false

* From 表单：由输入框、选择器、单选框、多选框等控件组成，用以**收集、校验、提交数据**

##### 4.4.3、案例

- 根据页面原型完成员工管理页面开发，并通过Axios完成数据异步加载。

![image-20231014182505745](https://gitee.com/coi4/test/raw/master/img/image-20231014182505745.png)

- > 1. 制作类似格式的页面
  >
  >    即上面是标题，左侧栏是导航，右侧是数据展示区域
  >
  > 2. 右侧需要展示搜索表单
  >
  > 3. 右侧表格数据是动态展示的，数据来自于后台
  >
  > 4. 实际示例效果如下图所示：
  >
  >    服务端数据获取地址：http://yapi.smart-xwork.cn/mock/169327/emp/list

  ![image-20231014182555721](https://gitee.com/coi4/test/raw/master/img/image-20231014182555721.png)

  - 创建页面，完成页面的整体布局规划

  - 布局中各个部分的组件实现

  - 列表数据的异步加载，并渲染展示

  - ![img](https://gitee.com/coi4/test/raw/master/img/BB5DD259C404A36E9730B39297D26F71.png)

  - ```
    1.创建vue文件，套模板（有需要的话在App.vue引入组件改成创建的组件）
    2.观察整体布局，在ElementUI中找到相应布局组件，调整样式css（在container内标签内）
    3.顶部：header，调整样式，
      左侧：aside，在布局组件中找到案例组件，替换文字
      右侧：表格组件，拷贝数据模型；prop属性不乱写，绑定后台数据用
      表单：找模型，增删，完成绑定（v-model：data中添加searchForm：{}）
      时间：
      分页工具：
    4.异步数据加载：用axios发送Ajax请求
    在vue中，对于axios的使用：
    ①如上图安装axios；npm install axios
    ②重启项目，导入axios；import axios 'axios'
    发送请求；
     mounted(){
            axios.get("http://yapi.smart-xwork.cn/mock/169327/emp/list")
            .then(resp=>{
                this.tableData=resp.data.data; //响应数据赋值给数据模型
            });
        }
    修复：
    性别：
    进入表单组件，对比效果和功能实现代码；template用于自定义列的内容，slot-scope属性通过row获取当前行的数据；
    
     <el-table-column prop="gender"    label="性别" width="140">
         <template slot-scope="scope">
        	 {{scope.row.gender==1?"男":"女"}}
         </template>
     </el-table-column>
     
     图片：
     <el-table-column prop="image"     label="图像" width="180">
        <template slot-scope="scope">
            <img :src="scope.row.image" width="100px" height="70px">
        </template>
    </el-table-column>
    ```

    ```
    <template>
        <div>
            <!-- 设置最外层容器高度为700px,在加上一个很细的边框 -->
            <el-container style="height: 700px; border: 1px solid #eee">
                <el-header style="font-size:40px;background-color: rgb(238, 241, 246)">tlias 智能学习辅助系统</el-header>
                <el-container>
                    <el-aside width="230px"  style="border: 1px solid #eee">
                         <el-menu :default-openeds="['1', '3']">
                            <el-submenu index="1">
                                <template slot="title"><i class="el-icon-message"></i>系统信息管理</template>
                              
                                <el-menu-item index="1-1">部门管理</el-menu-item>
                                <el-menu-item index="1-2">员工管理</el-menu-item>
                              
                         
                            </el-submenu>
                         </el-menu>
                    </el-aside>
                    <el-main>
                        <!-- 表单 -->
                        <el-form :inline="true" :model="searchForm" class="demo-form-inline">
                            <el-form-item label="姓名">
                                <el-input v-model="searchForm.name" placeholder="姓名"></el-input>
                            </el-form-item>
                            <el-form-item label="性别">
                                <el-select v-model="searchForm.gender" placeholder="性别">
                                <el-option label="男" value="1"></el-option>
                                <el-option label="女" value="2"></el-option>
                                </el-select>
                            </el-form-item>
                              <el-form-item label="入职日期">
                                 <el-date-picker
                                    v-model="searchForm.entrydate"
                                    type="daterange"
                                    range-separator="至"
                                    start-placeholder="开始日期"
                                    end-placeholder="结束日期">
                                </el-date-picker>
                            </el-form-item>
                            <el-form-item>
                                <el-button type="primary" @click="onSubmit">查询</el-button>
                            </el-form-item>
                        </el-form>
                        <!-- 表格 -->
                        <el-table :data="tableData">
                            <el-table-column prop="name"      label="姓名" width="180"></el-table-column>
                            <el-table-column prop="image"     label="图像" width="180">
                                <template slot-scope="scope">
                                    <img :src="scope.row.image" width="100px" height="70px">
                                </template>
                            </el-table-column>
                            <el-table-column prop="gender"    label="性别" width="140">
                                <template slot-scope="scope">
                                    {{scope.row.gender==1?"男":"女"}}
                                </template>
                            </el-table-column>
                            <el-table-column prop="job"       label="职位" width="140"></el-table-column>
                            <el-table-column prop="entrydate" label="入职日期" width="180"></el-table-column>
                            <el-table-column prop="updatetime" label="最后操作时间" width="230"></el-table-column>
                            <el-table-column label="操作" >
                                <el-button type="primary" size="mini">编辑</el-button>
                                <el-button type="danger" size="mini">删除</el-button>
                            </el-table-column>
                        </el-table>
    
                        <!-- Pagination分页 -->
                        <el-pagination
                            @size-change="handleSizeChange"
                            @current-change="handleCurrentChange"
                            background
                            layout="sizes,prev, pager, next,jumper,total"
                            :total="1000">
                        </el-pagination>
                    </el-main>
                </el-container>
            </el-container>
        </div>
    </template>
    
    <script>
    import axios  'axios'
    export default {
         data() {
          return {
            tableData: [
               
            ],
            searchForm:{
                name:'',
                gender:'',
                entrydate:[]
            }
          }
        },
        methods:{
            onSubmit:function(){
                console.log(this.searchForm);
            },
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
                console.log(`当前页: ${val}`);
            }
        },
        mounted(){
            axios.get("http://yapi.smart-xwork.cn/mock/169327/emp/list")
            .then(resp=>{
                this.tableData=resp.data.data;
            });
        }
    }
    </script>
    
    <style>
    
    </style>
    
    ```

#### 4.5、Vue路由

![image-20231014182808578](https://gitee.com/coi4/test/raw/master/img/image-20231014182808578.png)

* 介绍： Vue Router 是 Vue 的官方路由插件。
* 组成：
  * VueRouter：路由器类，根据路由请求在路由视图中动态渲染选中的组件
  * <router-link>：请求链接组件，浏览器会解析成<a>
  * <router-view>：动态视图组件，用来渲染展示与路由路径对应的组件

1. 安装（创建Vue项目时已选择）![image-20231014183150672](https://gitee.com/coi4/test/raw/master/img/image-20231014183150672.png)

2. 定义路由

   - src/router/index.js文件中定义路由表
   
      ```
      import Vue  'vue'
      import VueRouter  'vue-router'
      
      Vue.use(VueRouter)
      
      const routes = [
        {
          path: '/emp',  //地址hash
          name: 'emp',
          component:  () => import('../views/tlias/EmpView.vue')  //对应的vue组件
        },
        {
          path: '/dept',
          name: 'dept',
          component: () => import('../views/tlias/DeptView.vue')
        }
      ]
      
      const router = new VueRouter({
        routes
      })
      
      export default router
      
      ```
   
      
   
   ![image-20231014183349241](https://gitee.com/coi4/test/raw/master/img/image-20231014183349241.png)

##### 4.5.1、案例

通过Vue的路由VueRouter完成左侧菜单栏点击切换效果

![image-20231014183515951](https://gitee.com/coi4/test/raw/master/img/image-20231014183515951.png)

```
//EmpView.vue（员工管理页面组件）和DeptView.vue（部门管理页面组件）中修改：
<el-menu-item index="1-1">
    <router-link to="/dept">部门管理</router-link>
</el-menu-item>
<el-menu-item index="1-2">
    <router-link to="/emp">员工管理</router-link>
</el-menu-item>
```

```
//App.vue 中修改成：
<router-view></router-view>
```

最后路由配置中加入：

```
{
    path: '/',
    redirect:'/emp' //表示重定向到/emp即可
  },
```

#### 4.6、打包部署

工程开发好进行发布：

1. 前端工程打包
2. 通过nginx服务器发布前端工程

##### 4.6.5、打包

![image-20231014184037307](https://gitee.com/coi4/test/raw/master/img/image-20231014184037307.png)

##### 4.6.6、部署

- 介绍：Nginx是一款轻量级的Web服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。其特点是占有内存少，并发能力强，在各大型互联网公司都有非常广泛的使用。
- 官网：https://nginx.org/
- 压缩文件拷贝到**无中文的目录下**，直接解压即可
- ![image-20231014184150729](https://gitee.com/coi4/test/raw/master/img/image-20231014184150729.png)

将打包好的 dist 目录下的文件，复制到nginx安装目录的html目录下。

双击 nginx.exe 文件即可，Nginx服务器默认占用 80 端口号，如果80端口号被占用，可以在nginx.conf中修改端口号。(netstat –ano | findStr 80)

## 二、后端Web开发

### 1、maven

#### 1.1概述

##### 1.1.1、介绍

Maven是apache旗下的一个开源项目，是一款用于**管理和构建java项目的工具**，基于项目对象模型(POM)的概念，通过一小段描述信息来管理项目的构建。官网：http://maven.apache.org/

> Apache 软件基金会，成立于1999年7月，是目前世界上最大的最受欢迎的开源软件基金会，也是一个专门为支持开源项目而生的非盈利性组织。开源项目：[https://www.apache.org/index.html#projects-list](https://www.apache.org/index.html)

maven作用：

- 依赖管理---方便快捷的管理项目依赖的资源(jar包)，避免版本冲突问题
- 统一项目结构---![image-20231016133307767](https://gitee.com/coi4/test/raw/master/img/image-20231016133307767.png)
- 项目构建---标准跨平台（Linux、Windows、MacOS）的自动化项目构建方式![image-20231016133356333](https://gitee.com/coi4/test/raw/master/img/image-20231016133356333.png)

Maven模型：

- 项目对象模型(POM)
- 依赖管理模型（Dependency)
- 构建生命周期/阶段

需要jar包时，直接把jar包复制到项目下的lib目录

坐标：由<groupld>、<artifactld>、<version>组成，**定位用**

![img](https://gitee.com/coi4/test/raw/master/img/D08C9A3612C0E4ECB927F97960EF45AC.png)

![image-20231016133824370](https://gitee.com/coi4/test/raw/master/img/image-20231016133824370.png)

![image-20231016133908793](https://gitee.com/coi4/test/raw/master/img/image-20231016133908793.png)

> 仓库：用于存储资源，管理各种jar包（开发中所有依赖）和插件。
>
> - 本地仓库：自己计算机上的一个目录
> - 中央仓库：由Maven团队维护的全球唯一的。 仓库地址：https://repo1.maven.org/maven2/
> - 远程仓库(私服)：一般由公司团队搭建的私有仓库。

##### 1.1.2、安装

**解压**到E：\develop下

在自己计算机**上新一个目录**（本地仓库、存jar包）

![img](https://gitee.com/coi4/test/raw/master/img/177508FE9D8661A9A0D83E1EAD0BF18F.png)

复制53行到55行，**改路径**

160行添加子标签，只能**配置一个mirror**！

```
<mirror>  
    <id>alimaven</id>  
    <name>aliyun maven</name>  
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>          
</mirror>
```

![img](https://gitee.com/coi4/test/raw/master/img/3559297FE0498DCBD3710CCE9349BDFB.png)

**配置变量：**

1. 在系统变量处新建一个变量MAVEN_HOME

   此电脑--属性--高级系统设置--环境变量

   ![img](https://gitee.com/coi4/test/raw/master/img/6248122E4D4CB20F1B51AF7394DE1610.png)

2. 在Path中进行配置

   ![img](https://gitee.com/coi4/test/raw/master/img/DDF418E2A46A4884711D9D54608A597F.png)

* bin目录 ： 存放的是可执行命令。（mvn 命令重点关注）
* conf目录 ：存放Maven的配置文件。（settings.xml配置文件后期需要修改）
* lib目录 ：存放Maven依赖的jar包。（Maven也是使用java开发的，所以它也依赖其他的jar包）



![image-20231016134249776](https://gitee.com/coi4/test/raw/master/img/image-20231016134249776.png)

![image-20231016134315972](https://gitee.com/coi4/test/raw/master/img/image-20231016134315972.png)

#### 1.2、IDEA集成maven

##### 1.2.1、**配置maven环境**

当前工程：

> Maven home path ：指定当前Maven的安装目录
>
> User settings file ：指定当前Maven的settings.xml配置文件的存放路径
>
> Local repository ：指定Maven的本地仓库的路径 (如果指定了settings.xml, 这个目录会自动读取出来, 可以不用手动指定)

![image-20231016134626520](https://gitee.com/coi4/test/raw/master/img/image-20231016134626520.png)

![img](https://gitee.com/coi4/test/raw/master/img/BE1542D3D62B92A78B90DA4C5714FFBE.png)

全局：

![image-20231016134719577](https://gitee.com/coi4/test/raw/master/img/image-20231016134719577.png)

打开 All settings , 选择 Build,Execution,Deployment  =>  Build Tools  =>  Maven

##### 1.2.2、创建项目

1. **创建模块**，选择Maven，点击Next!![image-20231016163335573](https://gitee.com/coi4/test/raw/master/img/image-20231016163335573.png)

2. **填写**模块名称，坐标信息，点击finish，创建完成![image-20231016163351114](https://gitee.com/coi4/test/raw/master/img/image-20231016163351114.png)

3. 编写 HelloWorld，并运行

   > 坐标：
   >
   > - Maven 中的坐标是资源的唯一标识，通过该坐标可以唯一定位资源（插件、依赖、当前项目）位置。
   > - 使用坐标来定义项目或引入项目中需要的依赖。
   > - 主要组成：
   >   - groupId：定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima）
   >   - artifactId：定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service）
   >   - version：定义当前项目版本号
   >
   > ![image-20231016165803936](https://gitee.com/coi4/test/raw/master/img/image-20231016165803936.png)

> Maven项目的目录结构:
>
> maven-project01
> 	|---  src  (源代码目录和测试代码目录)
> 		    |---  main (源代码目录)
> 			           |--- java (源代码java文件目录)
> 			           |--- resources (源代码配置文件目录)
> 		    |---  test (测试代码目录)
> 			           |--- java (测试代码java目录)
> 			           |--- resources (测试代码配置文件目录)
> 	|--- target (编译、打包生成文件存放目录)

**POM用来描述当前的maven项目**；使用pom.xml实现

> pom文件详解：
>
> - <project> ：pom文件的根标签，表示当前maven项目
> - <modelVersion> ：声明项目描述遵循哪一个POM模型版本
>   - 虽然模型本身的版本很少改变，但它仍然是必不可少的。目前POM模型版本是4.0.0
> - 坐标 ：<groupId>、<artifactId>、<version>
>   - 定位项目在本地仓库中的位置，由以上三个标签组成一个坐标
> - <packaging> ：maven项目的打包方式，通常设置为jar或war（默认值：jar）

##### 1.2.3、导入项目

* 方式一：

  

  ![img](https://gitee.com/coi4/test/raw/master/img/F339B17890FE05F58046252FA05DEEA1.png)

![image-20231016165735672](https://gitee.com/coi4/test/raw/master/img/image-20231016165735672.png)

如果没有Maven面板，选择 View  =>  Appearance  =>  Tool Window Bars

![image-20231016163941044](https://gitee.com/coi4/test/raw/master/img/image-20231016163941044.png)

- 方式二：![image-20231016164016959](https://gitee.com/coi4/test/raw/master/img/image-20231016164016959.png)

![](https://gitee.com/coi4/test/raw/master/img/image-20231016164029416.png)

![image-20231016164100156](https://gitee.com/coi4/test/raw/master/img/image-20231016164100156.png)

#### 1.3、依赖管理

依赖：指当前项目运行所需要的jar包，一个项目中可以引入多个依赖。

##### 1.3.1、依赖配置

用logback来记录日志：

1. 在 pom.xml 中**编写 <dependencies> 标签**

2. 在 <dependencies> 标签中 **使用 <dependency> 引入坐标**

3. **定义坐标**的 groupId，artifactId，version

4. 点击**刷新**按钮，引入最新加入的坐标

   ![image-20231016164522330](https://gitee.com/coi4/test/raw/master/img/image-20231016164522330.png)

注：

- 如果引入的依赖，在本地仓库不存在，将会连接远程仓库/中央仓库，然后下载依赖。（这个过程会比较耗时，耐心等待）
- **如果不知道依赖的坐标信息**，可以到https://mvnrepository.com/中搜索。

1. 利用中央仓库搜索依赖坐标
2. **利用IDEA：alt+enter**
3. 熟练上手maven后，快速导入依赖

##### 1.3.2、依赖传递

在pom.xml文件中只添加了logback-classic依赖，但由于maven的依赖具有传递性，所以会自动把所依赖的其他jar包也一起导入

依赖具有传递性

- 直接依赖：在当前项目中通过依赖配置建立的依赖关系
- 间接依赖：被依赖的资源如果依赖其他资源，当前项目间接依赖其他资源
- 排除依赖：主动断开依赖的资源，被排除的资源无需指定版本。
  - ![image-20231016170258679](https://gitee.com/coi4/test/raw/master/img/image-20231016170258679.png)

##### 1.3.3、依赖范围

依赖的jar包，默认情况下，可以在任何地方使用。可以**通过 <scope>…</ scope > 设置其作用范围。**

**作用范围：**

- 主程序范围有效。（main文件夹范围内）
- 测试程序范围有效。（test文件夹范围内）
- 是否参与打包运行。（package指令范围内）

![image-20231016170427415](https://gitee.com/coi4/test/raw/master/img/image-20231016170427415.png)

这个依赖就只能作用在测试环境，其他环境下不能使用

![image-20231016170511623](https://gitee.com/coi4/test/raw/master/img/image-20231016170511623.png)

##### 1.3.4、生命周期

为了对所有的maven项目构建过程进行抽象和统一。

在Maven的设计中，**实际任务（如源代码编译）都交由插件来完成**

Maven中有3套相互独立的生命周期：

- clean：清理工作。
- default：核心工作，如：编译、测试、打包、安装、部署等。
- site：生成报告、发布站点等。

每套生命周期包含一些阶段（phase），阶段是有顺序的，后面的阶段依赖于前面的阶段。

在同一套生命周期中，当运行后面的阶段时，前面的阶段都会运行。

生命周期阶段：

![image-20231016170757964](https://gitee.com/coi4/test/raw/master/img/image-20231016170757964.png)

![image-20231016170856974](https://gitee.com/coi4/test/raw/master/img/image-20231016170856974.png)

![img](https://gitee.com/coi4/test/raw/master/img/7F2106A16CC0A315521942319ACF1DB6.png)

执行指定生命周期的两种方式：

- 在idea中，右侧的maven工具栏，选中对应的生命周期，双击执行。

- 在命令行中，通过命令执行。

  ![img](https://gitee.com/coi4/test/raw/master/img/BB98E7E871CC230798507449265D5DC0.png)
  
  ![image-20231016171059517](https://gitee.com/coi4/test/raw/master/img/image-20231016171059517.png)

#### 1.4、其他

给idea配置完maven仓库信息后，在idea中依然搜索不到仓库中的jar包。这是因为仓库中的jar包索引尚未更新到idea中。这个时候我们就需要更新idea中maven的索引了，具体做法如下：

 打开设置----搜索maven----Repositories----选中本地仓库-----点击Update

初始情况下，我们的本地仓库是没有任何jar包的，此时会从私服去下载（如果没有配置，就直接从中央仓库去下载），可能由于网络的原因，jar包下载不完全，这些不完整的jar包都是以lastUpdated结尾。此时，maven不会再重新帮你下载，需要你**删除这些以lastUpdated结尾的文件**，然后maven才会再次自动下载这些jar包。

操作步骤：

1. 定义批处理文件del_lastUpdated.bat  (直接创建一个文本文件，命名为del_lastUpdated，后缀名直接改为bat即可 )

2. 在上面的bat文件上**右键---》编辑** 。修改文件：

   ```
   set REPOSITORY_PATH=E:\develop\apache-maven-3.6.1\mvn_repo
   rem 正在搜索...
   
   del /s /q %REPOSITORY_PATH%\*.lastUpdated
   
   rem 搜索完毕
   pause
   ```

   

3. 修改完毕后，双击运行即可删除maven仓库中的残留文件。

### 2、SpringBootWeb入门

spring官网：[spring.io](https://spring.io/)

点击projects看开源项目

**Spring Boot** **可以帮助我们非常快速的构建应用程序、简化开发、提高效率**

#### 2.1、入门

> 需求：使用 SpringBoot 开发一个web应用，浏览器发起请求 /hello后，给浏览器返回字符串 "Hello World ~"。 

步骤：

1. **创建springboot工程**，并**勾选web开发相关依赖**。

   ![img](https://gitee.com/coi4/test/raw/master/img/B5C7B8A99BC6FA8EB71D65741C49D1DA.png)

   ![img](https://gitee.com/coi4/test/raw/master/img/2C2E4DBD0B0DBAEB134527770FB5652F.png)

2. **定义HelloController类**，添加方法 hello，并添加注解。

   - 在com.itheima包下创建子包controller

   - 在controller包下创建一个类：HelloController

   - ```java
     package com.itheima.controller;
     import org.springframework.web.bind.annotation.*;
     
     @RestController
     public class HelloController {
     
         @RequestMapping("/hello")
         public String hello(){
             System.out.println("Hello World ~");
             return "Hello World ~";
         }
         
     }    
     ```

     

3. **运行测试**

运行SpringBoot自动生成的引导类：SpringbootWebQuickstart1Application

打开浏览器，输入：`http://localhost:8080/hello`

#### 2.2、HTTP协议

查看http协议的数据传输格式：点击`F12`打开开发者工具，点击`Network`来查看

##### 2.2.1、概述

Hyper Text Transfer Protocol，超文本传输协议，**规定了浏览器和服务器之间数据传输的规则**。

特点：

- 基于TCP协议：面向连接，安全
- 基于请求-响应模型的：一次请求对应一次响应
- HTTP协议是无状态的协议：对于事务处理没有记忆能力。每次请求-响应都是独立的。

缺点：多次请求间不能共享数据。（京东购物，加入购物车和去购物车清算是两次请求，不记录加入购物车的是何商品）

优点：速度快

##### 2.2.2、请求协议

**浏览器访问服务器的几种方式**：

| 请求方式 | 请求说明                                                     |
| :------: | :----------------------------------------------------------- |
| **GET**  | 获取资源。<br/>向特定的资源**发出请求**。例：http://www.baidu.com/s?wd=itheima |
| **POST** | 传输实体主体。<br/>向指定资源**提交数据进行处理请求**（例：上传文件），数据被包含在请求体中。 |
| OPTIONS  | 返回服务器针对特定资源所支持的HTTP请求方式。<br/>因为并不是所有的服务器都支持规定的方法，为了安全有些服务器可能会禁止掉一些方法，例如：DELETE、PUT等。那么OPTIONS就是**用来询问服务器支持的方法**。 |
|   HEAD   | 获得报文首部。<br/>HEAD方法类似GET方法，但是不同的是HEAD方法**不要求返回数据**。通常用于**确认**URI的**有效性及资源更新时间等。** |
|   PUT    | 传输文件。<br/>PUT方法用来**传输文件**。类似FTP协议，文件内容包含在请求报文的实体中，然后**请求保存到URL指定的服务器位置。** |
|  DELETE  | 删除文件。<br/>请求服务器删除Request-URI所标识的资源         |
|  TRACE   | 追踪路径。<br/>**回显服务器收到的请求**，主要用于测试或诊断  |
| CONNECT  | 要求用隧道协议连接代理。<br/>HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器 |

GET方式的请求协议：

**请求行**：请求数据第一行(请求方式、资源路径、协议，之间使用空格)

- 请求方式：GET
- 资源路径：/brand/findAll?name=OPPO&status=1
  - 请求路径：/brand/findAll
  - 请求参数：name=OPPO&status=1
    * 请求参数是以key=value形式出现
    * 多个请求参数之间使用`&`连接
  - 请求路径和请求参数之间使用`?`连接 
  - 协议/版本：HTTP/1.1			

**请求头**：第二行开始，格式key：value

- | Host            | **请求的主机名**                                             |
  | --------------- | ------------------------------------------------------------ |
  | User-Agent      | 浏览器版本，例如Chrome浏览器的标识类似Mozilla/5.0 ... Chrome/79，IE浏览器的标识类似Mozilla/5.0 (Windows NT ...) like Gecko |
  | Accept          | 表示**浏览器能接收的资源类型**，如text/*，image/*或者*/*表示所有； |
  | Accept-Language | 表示**浏览器偏好的语言**，服务器可以据此返回不同语言的网页； |
  | Accept-Encoding | 表示**浏览器可以支持的压缩类型**，例如gzip,  deflate等。     |
  | Content-Type    | 请求主体的数据类型。                                         |
  | Content-Length  | 请求主体的大小（单位：字节）。                               |

**请求体**：存放请求参数

请求方式-GET: **请求参数在请求行中**，没有请求体，如：/brand/findAll?name=OPPO&status=1；**GET请求大小是有限制的**。

POST方式的请求协议：

![img](https://gitee.com/coi4/test/raw/master/img/C6C048399C98F6FF15FD2EFBE6CC8741.png)

请求行：

- 请求方式：POST
- 资源路径：/brand
- 协议/版本：HTTP/1.1

请求头：

请求体：请求体和请求头之间是有一个空行隔开（作用：用于标记请求头结束）

请求方式-POST: **请求参数在请求体中**，POST请求大小是**没有限制的**。

##### 2.2.3、响应协议

**响应行**：响应数据第一行(协议、状态码、描述)

* 协议/版本：HTTP/1.1
* 响应状态码：200
* 状态码描述：OK

**响应头**：第二行开始，格式key：value

- | Content-Type     | 表示该响应内容的类型，例如text/html，application/json。      |
  | ---------------- | ------------------------------------------------------------ |
  | Content-Length   | 表示**该响应内容的长度**（字节数）。                         |
  | Content-Encoding | 表示该响应压缩算法，例如gzip。                               |
  | Cache-Control    | **指示客户端应如何缓存**，例如max-age=300表示可以最多缓存300秒。 |
  | Set-Cookie       | 告诉浏览器为当前页面所在的域设置cookie。                     |

**响应体**：最后一部分，存放响应数据

响应体和响应头之间有一个空行隔开（作用：用于标记响应头结束）

响应状态码：

| 1xx  | 响应中-临时状态码，表示请求已经接收，告诉客户端应该继续请求或者如果它已经完成则忽略它。 |
| ---- | ------------------------------------------------------------ |
| 2xx  | 成功-表示请求已经被成功接收，处理已完成。                    |
| 3xx  | 重定向-重定向到其他地方；让客户端再发起一次请求以完成整个处理。 |
| 4xx  | 客户端错误-处理发生错误，责任在客户端。如: 请求了不存在的资源、客户端未被授权、禁止访问等。 |
| 5xx  | 服务器错误-处理发生错误，责任在服务端。如：程序抛出异常等。  |

| 200  | 客户端请求成功。                                        |
| ---- | ------------------------------------------------------- |
| 404  | 请求资源不存在，般是URL输入有误，或者网站资源被删除了。 |
| 500  | 服务器发生不可预期的错误。                              |

参考: 资料/SpringbootWeb/响应状态码.md

##### 2.2.4、协议解析

在开发中真正用到的Web服务器，我们不会自己写的，都是使用目前比较流行的web服务器。如：**Tomcat**

#### 2.3、Web服务器-Tomcat

![img](https://gitee.com/coi4/test/raw/master/img/466F1A10EE762BF32E0E2EB3A4A9199F.png)

Web服务器是一个软件程序，**对HTTP协议的操作进行封装**，不用程序员自己写代码去解析http协议规则，简化web程序开发；部署web项目，对外提供网上信息浏览服务。

Web服务器软件**使用步骤**：

![img](https://gitee.com/coi4/test/raw/master/img/A10A0FFDBFE0AF154EEBBFD7E28FBA82.png)

![img](https://gitee.com/coi4/test/raw/master/img/7479E5E0A9AFA173D33EDBCAF73E1014.png)

![img](https://gitee.com/coi4/test/raw/master/img/C39E87B25354D231037F52B4952A25DA.png)

![img](https://gitee.com/coi4/test/raw/master/img/4502D84948E673D875178752F6565F0C.png)

浏览器输入：`http://localhost:8080/demo/index.html`

Tomcat是Apache 软件基金会一个核心项目，是一个开源免费的轻量级Web服务器，支持Servlet/JSP少量JavaEE规范。

Tomcat 也被称为 Web容器、Servlet容器。Servlet程序需要依赖于 Tomcat才能运行 

官网：https://tomcat.apache.org/

##### 2.3.1、基本使用

1. **下载**：官网下载，地址 https://tomcat.apache.org/download-90.cgi

   ![img](https://gitee.com/coi4/test/raw/master/img/EA893743547914F8EF602FA9F2BC35B1.png)

   Tomcat软件类型说明：

   - tar.gz文件，是linux和mac操作系统下的压缩版本
   - zip文件，是window操作系统下压缩版本（我们选择zip文件）

2. **安装**：绿色版，直接解压即可

   develop目录下

   ![image-20231016231222301](https://gitee.com/coi4/test/raw/master/img/image-20231016231222301.png)

   bin：目录下有两类文件，一种是以`.bat`结尾的，是Windows系统的可执行文件，一种是以`.sh`结尾的，是Linux系统的可执行文件。

   webapps：就是以后项目部署的目录

3. **卸载**：直接删除目录即可

4. **启动**：双击：bin\startup.bat （黑窗口不关闭，正在运行）

   Tomcat的默认端口为8080，所以在浏览器的地址栏输入：`http://127.0.0.1:8080` 即可**访问tomcat服务器**

   > 127.0.0.1 也可以使用localhost代替。如：`http://localhost:8080`

   - 控制台中文乱码：修改conf/ logging.properties

     ![image-20231016231125811](https://gitee.com/coi4/test/raw/master/img/image-20231016231125811.png)

5. **关闭**：

   - 直接×掉运行窗口：强制关闭（不建议）

   - bin\shutdown.bat：正常关闭
   - Ctrl+C：正常关闭（没反应多按几次）

6. 配置Tomcat端口号（conf/server.xml）

   - ![image-20231016231450166](https://gitee.com/coi4/test/raw/master/img/image-20231016231450166.png)
   - HTTP协议默认端口号为80，如果将Tomcat端口号改为80，则将来访问Tomcat时，将不用输入端口号

​     7. Tomacat**部署项目**：将项目放置到 webapps     目录下， 即部署完成

常见问题：

- 启动窗口一闪而过：检查JAVA_HOME环境变量是否正确配置

- 端口号冲突：换Tomcat端口号

  ![image-20231016231316078](https://gitee.com/coi4/test/raw/master/img/image-20231016231316078.png)

##### 2.3.2、入门程序解析

Spring官方骨架，可以理解为Spring官方为程序员提供一个搭建项目的模板。

Spring官方骨架访问：https://start.spring.io/

![img](https://gitee.com/coi4/test/raw/master/img/037DEA5F5B86AF0FA8CD69E3AA8F03B0.png)

![img](https://gitee.com/coi4/test/raw/master/img/E56B9F89EE832E96DBE28B016560D8A3.png)

![img](https://gitee.com/coi4/test/raw/master/img/DDCCE581AE5CF18663FE54C4C41D59DA.png)

![img](https://gitee.com/coi4/test/raw/master/img/8A800764C29AA7EDCA3D4D057CEEF05F.png)

![img](https://gitee.com/coi4/test/raw/master/img/98A4BEF0B70F226C7A69A4597322F3CF.png)

![img](https://gitee.com/coi4/test/raw/master/img/EA1F27271C26B5A21B8BEF92A81C039E.png)

![img](https://gitee.com/coi4/test/raw/master/img/061A0CBD3CC7BB8C9C0F5B385EE1B481.png)

不论使用IDEA创建SpringBoot项目，还是直接在官方网站**利用骨架生成SpringBoot项目**，项目的结构和pom.xml文件中内容是相似的。

**起步依赖：**

spring-boot-starter-xxx这类的依赖，都为起步依赖。

- spring-boot-starter-web：包含了web应用开发所需要的常见依赖。
- spring-boot-starter-test：包含了单元测试所需要的常见依赖。
- 官方提供的starter：[https://docs.spring.io/spring-boot/docs/2.7.4/reference/htmlsingle/#using.build-systems.starters](https://docs.spring.io/spring-boot/docs/2.7.4/reference/htmlsingle/)
- 每一个起步依赖，都用于开发一个特定的功能
- 每一个SpringBoot工程，都有一个父工程。依赖的版本号，在父工程中统一管理。

![image-20231016231835952](https://gitee.com/coi4/test/raw/master/img/image-20231016231835952.png)

![image-20231016232023503](C:/Users/4u/AppData/Roaming/Typora/typora-user-images/image-20231016232023503.png)

内嵌Tomcat服务器：

- 基于Springboot开发的web应用程序，内置了tomcat服务器，当启动类运行时，会自动启动内嵌的tomcat服务器。

#### 2.4、请求响应

![img](https://gitee.com/coi4/test/raw/master/img/3BDC18F870375432768BF83E0D60FE6E.png)

测试自己所开发的程序：浏览器输入地址（GET请求），POST请求需要自己编写前端代码（麻烦）——使用专业接口测试工具（Postman）

##### 2.4.1、请求

**Postman**是一款功能强大的网页调试与发送网页HTTP请求的Chrome插件。

作用：常**用于进行接口测试**

![image-20231017145723391](https://gitee.com/coi4/test/raw/master/img/image-20231017145723391.png)

**安装**：`Postman-win64-8.3.1-Setup.exe`

无需升级

![img](https://gitee.com/coi4/test/raw/master/img/A7BCB4406B515157C3BCD70656EA0E02.png)

![img](https://gitee.com/coi4/test/raw/master/img/B4B01401B460B5BFDEBF28AAA84D56F8.png)

**如果我们需要将测试的请求信息保存下来，就需要创建一个postman的账号，然后登录之后才可以。**

登录之后可以创建工作空间：

![img](https://gitee.com/coi4/test/raw/master/img/AE8D3C7E5DA7FB1B88A3D33B7BEBD2AC.png)

![img](https://gitee.com/coi4/test/raw/master/img/3ABA1C89D4F7B9F336C586B7ABE685DA.png)

![img](https://gitee.com/coi4/test/raw/master/img/20C4CEDEC900669BF87AB318B4AA5E16.png)

**创建请求**：

![img](https://gitee.com/coi4/test/raw/master/img/D7C31B25397A2BE1B9216DCE011331E2.png)

![img](https://gitee.com/coi4/test/raw/master/img/F65480FA8FE010D79DF07BD27DDABA4E.png)

![img](https://gitee.com/coi4/test/raw/master/img/E40047FE4777321FC875C7A591E36A65.png)

![img](https://gitee.com/coi4/test/raw/master/img/B89BA4BB7A8CAF51BBB5723BC7BEED12.png)

![img](https://gitee.com/coi4/test/raw/master/img/F1252F1C9C960E59487E32AAFFF81993.png)

![img](https://gitee.com/coi4/test/raw/master/img/96BC9C8F07B5675EF7A3D5640EB43A5A.png)

![img](https://gitee.com/coi4/test/raw/master/img/8A543571889648CD86BBB1F84B67A817.png)

简单参数：在向服务器发起请求时，向服务器传递的是一些普通的请求数据（url地址传参，地址参数名与形参变量名相同，定义形参即可接收参数）。

- 原始方式获取请求参数（仅做了解）：

  - Controller方法形参中声明HttpServletRequest对象
  - 调用对象的getParameter(参数名)

- **SpringBoot接收简单参数**

  - 保证**请求参数名和Controller方法中的形参名保持一致**，就可以获取到请求参数中的数据值

  - ![image-20231019230326286](https://gitee.com/coi4/test/raw/master/img/image-20231019230326286.png)

  - ```java
    @RestController
    public class RequestController {
        // http://localhost:8080/simpleParam?name=Tom&age=10
        // 第1个请求参数： name=Tom   参数名:name，参数值:Tom
        // 第2个请求参数： age=10     参数名:age , 参数值:10
        
        //springboot方式
        @RequestMapping("/simpleParam")
        public String simpleParam(String name , Integer age ){//形参名和请求参数名保持一致
            System.out.println(name+"  :  "+age);
            return "OK";
        }
    }
    ```

- 若不一致，使用@RequestParam注解

  - ```java
    @RestController
    public class RequestController {
        // http://localhost:8080/simpleParam?name=Tom&age=20
        // 请求参数名：name
    
        //springboot方式
        @RequestMapping("/simpleParam")
        public String simpleParam(@RequestParam("name") String username , Integer age ){
            System.out.println(username+"  :  "+age);
            return "OK";
        }
    }
    ```

  - 方法形参名称与请求参数名称不匹配，通过该注解完成映射

  - 该注解的required属性默认是true，代表请求参数必须传递，不传递将报错

简单参数做为数据传递方式时，**前端传递了多少个请求参数，后端controller方法中的形参就要书写多少个**

实体参数：

- 简单实体对象（（POJO数据类型））：请求参数名与形参对象属性名相同，定义POJO接收即可；
- 复杂实体对象（**嵌套**POJO类型参数)：（POJO对象中嵌套了其他的POJO类![image-20231104212444248](https://gitee.com/coi4/test/raw/master/img/image-20231104212444248.png)）请求参数名与形参对象属性名相同，按照对象层次结构关系即可接收嵌套POJO属性参数。![image-20231104212539250](https://gitee.com/coi4/test/raw/master/img/image-20231104212539250.png)

多个值提交：

数组集合参数：

- 数组参数：请求参数名与形参数组名称相同且请求参数为多个，定义数组类型形参即可接收参数（参数名一致才能封装到一个数组中）

  - ```Java
    @RestController
    public class RequestController {
        //数组集合参数
        @RequestMapping("/arrayParam")
        public String arrayParam(String[] hobby){
            System.out.println(Arrays.toString(hobby));
            return "OK";
        }
    }
    ```

  - SpringMVC![image-20231104212736955](https://gitee.com/coi4/test/raw/master/img/image-20231104212736955.png)

  - postman测试：可xxxxxxxxxxxxx?hobby=game,java

- 集合参数：请求参数名与形参集合名称相同且请求参数为多个，@RequestParam 绑定参数关系

  - ```Java
    @RestController
    public class RequestController {
        //数组集合参数
        @RequestMapping("/listParam")
        public String listParam(@RequestParam List<String> hobby){
            System.out.println(hobby);
            return "OK";
        }
    }
    ```
    
  - SpringMVC![image-20231104212857113](https://gitee.com/coi4/test/raw/master/img/image-20231104212857113.png)

日期参数：

- 日期参数：使用 @DateTimeFormat 注解完成日期参数格式转换 ，pattern属性设置日期格式

  - ```java
    @RestController
    public class RequestController {
        //日期时间参数
       @RequestMapping("/dateParam")
        public String dateParam(@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") LocalDateTime updateTime){
            System.out.println(updateTime);
            return "OK";
        }
    }
    ```

Json参数：

- JSON参数：JSON数据键名与形参对象属性名相同，定义POJO类型形参即可接收参数，需要使用 @RequestBody 标识

  - ```java
    @RestController
    public class RequestController {
        //JSON参数
        @RequestMapping("/jsonParam")
        public String jsonParam(@RequestBody User user){
            System.out.println(user);
            return "OK";
        }
    }
    ```

  - ![image-20231019232256878](https://gitee.com/coi4/test/raw/master/img/image-20231019232256878.png)

路径参数：

- 路径参数：通过请求URL直接传递参数，使用{…}来标识该路径参数，需要使用 @PathVariable 获取路径参数

  - ```java
    @RestController
    public class RequestController {
        //路径参数
        @RequestMapping("/path/{id}")
        public String pathParam(@PathVariable Integer id){
            System.out.println(id);
            return "OK";
        }
    }
    ```

传递多个路径参数：

- ```java
  @RestController
  public class RequestController {
      //路径参数
      @RequestMapping("/path/{id}/{name}")
      public String pathParam2(@PathVariable Integer id, @PathVariable String name){
          System.out.println(id+ " : " +name);
          return "OK";
      }
  }
  ```

```java
@RestController
public class ResponseController {
    //响应字符串
    @RequestMapping("/hello")
    public String hello(){
        System.out.println("Hello World ~");
        return "Hello World ~";
    }
    //响应实体对象
    @RequestMapping("/getAddr")
    public Address getAddr(){
        Address addr = new Address();//创建实体类对象
        addr.setProvince("广东");
        addr.setCity("深圳");
        return addr;
    }
    //响应集合数据
    @RequestMapping("/listAddr")
    public List<Address> listAddr(){
        List<Address> list = new ArrayList<>();//集合对象
        
        Address addr = new Address();
        addr.setProvince("广东");
        addr.setCity("深圳");

        Address addr2 = new Address();
        addr2.setProvince("陕西");
        addr2.setCity("西安");

        list.add(addr);
        list.add(addr2);
        return list;
    }
}
```

##### 2.4.2、响应

@Response Body注解：

类型：方法注解、类注解

位置：Controller方法上/类上

作用：将方法返回值直接响应，如果返回值类型是 实体对象/集合 ，将会转换为JSON格式响应

说明：@RestController = @Controller + @ResponseBody ;

统一响应结果：Result（code、msg、data）

- 把资料中result类复制到pojo包下

- 修改controller

  - ```Java
    @RestController
    public class ResponseController { 
        //响应统一格式的结果
        @RequestMapping("/hello")
        public Result hello(){
            System.out.println("Hello World ~");
            //return new Result(1,"success","Hello World ~");
            return Result.success("Hello World ~");
        }
    
        //响应统一格式的结果
        @RequestMapping("/getAddr")
        public Result getAddr(){
            Address addr = new Address();
            addr.setProvince("广东");
            addr.setCity("深圳");
            return Result.success(addr);
        }
    
        //响应统一格式的结果
        @RequestMapping("/listAddr")
        public Result listAddr(){
            List<Address> list = new ArrayList<>();
    
            Address addr = new Address();
            addr.setProvince("广东");
            addr.setCity("深圳");
    
            Address addr2 = new Address();
            addr2.setProvince("陕西");
            addr2.setCity("西安");
    
            list.add(addr);
            list.add(addr2);
            return Result.success(list);
        }
    }
    ```

###### 2.4.2.1、案例

> 加载并解析emp.xml文件中的数据，完成数据处理，并在页面展示。
>
> 获取员工数据，返回统一响应结果，在页面渲染展示
>
> ![image-20231017151042799](https://gitee.com/coi4/test/raw/master/img/image-20231017151042799.png)

```
1.在pom.xml文件中引入dom4j的依赖，用于解析XML文件
2.引入资料中提供的解析XML的工具类XMLParserUtils、对应的实体类Emp、XML文件 emp.xml
3.引入资料中提供的静态页面文件，放在resources下的static目录下
4.编写Controller程序，处理请求，响应数据
```

![image-20231019234228568](https://gitee.com/coi4/test/raw/master/img/image-20231019234228568.png)

```java
@RestController
public class EmpController {
    @RequestMapping("/listEmp")
    public Result list(){
        //1. 加载并解析emp.xml
        String file = this.getClass().getClassLoader().getResource("emp.xml").getFile();
        //System.out.println(file);
        List<Emp> empList = XmlParserUtils.parse(file, Emp.class);

        //2. 对数据进行转换处理 - gender, job
        empList.stream().forEach(emp -> {
            //处理 gender 1: 男, 2: 女
            String gender = emp.getGender();
            if("1".equals(gender)){
                emp.setGender("男");
            }else if("2".equals(gender)){
                emp.setGender("女");
            }

            //处理job - 1: 讲师, 2: 班主任 , 3: 就业指导
            String job = emp.getJob();
            if("1".equals(job)){
                emp.setJob("讲师");
            }else if("2".equals(job)){
                emp.setJob("班主任");
            }else if("3".equals(job)){
                emp.setJob("就业指导");
            }
        });
        //3. 响应数据
        return Result.success(empList);
    }
}
```

##### 2.4.3、分层解耦

三层架构：数据访问；逻辑处理；接受请求、响应数据

![屏幕截图 2023-10-19 235234](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-19%20235234.png)

![image-20231020001356560](https://gitee.com/coi4/test/raw/master/img/image-20231020001356560.png)

> controller：控制层，**接收**前端发送的**请求**，对请求进行处理，并**响应数据**。
>
> service：业务逻辑层，**处理具体的业务逻辑**。
>
> dao：数据访问层(Data Access Object)（持久层），负责**数据访问操作**，包括数据的增、删、改、查。

- 前端发起的请求，由Controller层接收（Controller响应数据给前端）

  - ```java
    @RestController
    public class EmpController {
        //业务层对象
        private EmpService empService = new EmpServiceA();
    
        @RequestMapping("/listEmp")
        public Result list(){
            //1. 调用service层, 获取数据
            List<Emp> empList = empService.listEmp();
    
            //3. 响应数据
            return Result.success(empList);
        }
    }
    ```

- Controller层调用Service层来进行逻辑处理（Service层处理完后，把处理结果返回给Controller层）

  - ```java
    //业务逻辑接口（制定业务标准）
    public interface EmpService {
        //获取员工列表
        public List<Emp> listEmp();
    }
    ```

  - ```java
    //业务逻辑实现类（按照业务标准实现）
    public class EmpServiceA implements EmpService {
        //dao层对象
        private EmpDao empDao = new EmpDaoA();
    
        @Override
        public List<Emp> listEmp() {
            //1. 调用dao, 获取数据
            List<Emp> empList = empDao.listEmp();
    
            //2. 对数据进行转换处理 - gender, job
            empList.stream().forEach(emp -> {
                //处理 gender 1: 男, 2: 女
                String gender = emp.getGender();
                if("1".equals(gender)){
                    emp.setGender("男");
                }else if("2".equals(gender)){
                    emp.setGender("女");
                }
    
                //处理job - 1: 讲师, 2: 班主任 , 3: 就业指导
                String job = emp.getJob();
                if("1".equals(job)){
                    emp.setJob("讲师");
                }else if("2".equals(job)){
                    emp.setJob("班主任");
                }else if("3".equals(job)){
                    emp.setJob("就业指导");
                }
            });
            return empList;
        }
    }
    ```

- Serivce层调用Dao层（逻辑处理过程中需要用到的一些数据要从Dao层获取）

  - ```java
    //数据访问层接口（制定标准）
    public interface EmpDao {
        //获取员工列表数据
        public List<Emp> listEmp();
    }
    ```

  - ```java
    //数据访问实现类
    public class EmpDaoA implements EmpDao {
        @Override
        public List<Emp> listEmp() {
            //1. 加载并解析emp.xml
            String file = this.getClass().getClassLoader().getResource("emp.xml").getFile();
            System.out.println(file);
            List<Emp> empList = XmlParserUtils.parse(file, Emp.class);
            return empList;
        }
    }
    ```

- Dao层操作文件中的数据（Dao拿到的数据会返回给Service层）

需要什么对象，就直接new一个就可以了。——耦合

分层解耦：

- 内聚：软件中各个功能模块内部的功能联系。
- 耦合：衡量软件中各个层/模块之间的依赖、关联的程度。
- 软件设计原则：高内聚低耦合。

> **控制反转：** Inversion Of Control，简称IOC。**对象的创建控制权由程序自身转移到外部**（容器），这种思想称为控制反转。@Component
>
> **依赖注入：** Dependency Injection，简称DI。容器为应用程序提供**运行时，所依赖的资源**，称之为依赖注入。@Autowired
>
> Bean对象：**IOC容器中创建、管理的对象**，称之为bean。

IOC&DI入门：

①. Service层 及 Dao层的实现类，交给IOC容器管理。

②. 为Controller及Service注入运行时，依赖的对象。

③. 运行测试。

IOC：

- Bean声明：要把某个对象交给IOC容器管理，需要在对应的类上加上如下注解之一

  - | 注解        | 说明                 | 位置                                                |
    | ----------- | -------------------- | --------------------------------------------------- |
    | @Component  | 声明bean的基础注解   | 不属于以下三类时，用此注解                          |
    | @Controller | @Component的衍生注解 | 标注在**控制器类**上                                |
    | @Service    | @Component的衍生注解 | 标注在**业务类**上                                  |
    | @Repository | @Component的衍生注解 | 标注在**数据访问类**上（由于与mybatis整合，用的少） |

  - 声明bean的时候，可以通过**value属性指定bean的名字**，如果没有指定，默认为类名首字母小写。

    ![img](https://gitee.com/coi4/test/raw/master/img/3D714C6ADD4BB06578B9B59A3251935F.png)

  - 使用以上四个注解都可以声明bean，但是在springboot集成web开发中，声明控制器bean只能用@Controller。

- Bean组件扫描：
  - 前面声明bean的四大注解，要想生效，还需要被组件扫描注@ComponentScan扫描。
  - @ComponentScan注解虽然没有显式配置，但是实际上已经包含在了启动类声明注解 
  - @SpringBootApplication 中，默认扫描的范围是启动类所在包及其子包。
    - **将我们定义的controller，service，dao这些包呢，都放在引导类所在包com.itheima的子包下**，这样我们定义的bean就会被自动的扫描到

DI：

- Bean注入：

  - @Autowired注解，默认是按照**类型**进行，如果存在多个相同类型的bean，将会报出错误：

  - 通过以下几种方案来解决：

    @Primary：当存在多个相同类型的Bean注入时，加上@Primary注解，来确定默认的实现。![img](https://gitee.com/coi4/test/raw/master/img/D612742A82CF6CC212DC73A133D00E73.png)

    @Qualifier：![img](https://gitee.com/coi4/test/raw/master/img/2A5D40E76F1D7E9D58CBE6643817A08C.png)

    @Resource：![img](https://gitee.com/coi4/test/raw/master/img/49A7F1EADE93800D0E75809E1AC9D326.png)

> 面试题：
>
> @Resource与@Autowired区别
>
> - @Autowired 是spring框架提供的注解，而@Resource是JDK提供的注解。
> - @Autowired 默认是按照类型注入，而@Resource默认是按照名称注入。

### 3、MySQL

替代xml文件；

数据库：DataBase（DB），是存储和管理数据的仓库。

数据库管理系统：DataBase Management System (DBMS)，操纵和管理数据库的大型软件。

SQL：Structured Query Language，操作关系型数据库的**编程语言**，定义了一套操作关系型数据库统一标准。

程序员给数据库管理系统(DBMS)发送SQL语句，再由数据库管理系统操作数据库当中的数据。

| Oracle     | 收费的大型数据库，Oracle公司的产品。                         |
| ---------- | ------------------------------------------------------------ |
| MySQL      | 开源免费的中小型数据库。Sun公司收购了MySQL，Oracle收购Sun公司。 |
| SQL Server | MicroSoft公司收费的中型的数据库。C#、.net等语言常使用。      |
| PostgreSQL | 开源免费中小型的数据库。                                     |
| DB2        | IBM公司的大型收费数据库产品。                                |
| SQLite     | 嵌入式的微型数据库。如：作为Android内置数据库                |
| MariaDB    | 开源免费的中小型的数据库。                                   |

只要我们学会了SQL语句，就可以通过SQL语句来操作Mysql，也可以通过SQL语句来操作Oracle或SQL Server

#### 3.1、数据库设计

##### 3.1.1、概述

###### 3.1.1.1、安装配置

官网下载地址：https://dev.mysql.com/downloads/mysql/

![image-20231017235609375](https://gitee.com/coi4/test/raw/master/img/image-20231017235609375.png)

安装步骤查看文档！

MySQL连接：

- 语法：![image-20231017235730669](https://gitee.com/coi4/test/raw/master/img/image-20231017235730669.png)
- 密码在-p回车之后，在命令行中输入密码，然后回车

![image-20231017235741703](https://gitee.com/coi4/test/raw/master/img/image-20231017235741703.png)

###### 3.1.1.2、数据模型

关系型数据库（RDBMS）: 建立在关系模型基础上，由多张相互连接的二维表组成的数据库。

![image-20231017235845114](https://gitee.com/coi4/test/raw/master/img/image-20231017235845114.png)

> 在Mysql数据库服务器当中存储数据，你需要：
>
> 1. 先去创建数据库（可以创建多个数据库，之间是相互独立的）
> 2. 在数据库下再去创建数据表（一个数据库下可以创建多张表）
> 3. 再将数据存放在数据表中（一张表可以存储多行数据）

###### 3.1.1.3、SQL

SQL：一门操作关系型数据库的编程语言，定义操作所有关系型数据库的统一标准。

- SQL语句可以单行或多行书写，以分号结尾。![img](https://gitee.com/coi4/test/raw/master/img/A3977129E92590FE1C98B6A085FAD61E.png)
- SQL语句可以使用空格/缩进来增强语句的可读性。
- MySQL数据库的SQL语句不区分大小写。
- 注释：
  1. 单行注释：-- 注释内容 或 # 注释内容(MySQL特有)
  2. 多行注释： /* 注释内容 */

| **分类** | **全称**                    | **说明**                                                   |
| -------- | --------------------------- | ---------------------------------------------------------- |
| DDL      | Data Definition  Language   | 数据**定义**语言，用来定义数据库对象(数据库，表，字段)     |
| DML      | Data Manipulation  Language | 数据**操作**语言，用来对数据库表中的数据进行增删改         |
| DQL      | Data Query Language         | 数据**查询**语言，用来查询数据库中表的记录                 |
| DCL      | Data Control  Language      | 数据**控制**语言，用来创建数据库用户、控制数据库的访问权限 |

![image-20231018000129324](https://gitee.com/coi4/test/raw/master/img/image-20231018000129324.png)

![image-20231020004518796](https://gitee.com/coi4/test/raw/master/img/image-20231020004518796.png)

##### 3.1.2、数据库设计-DDL

###### 3.1.2.1、数据库

DDL 英文全称是 Data Definition Language，数据定义语言，用来定义数据库对象(数据库、表)。

查询：

- 查询所有数据库：show databases;
- 查询**当前**数据库：select database();

使用：

- 使用数据库：use 数据库名 ;
- 我们要操作某一个数据库，必须要切换到对应的数据库中。

创建：

- 创建数据库：create database [ if not exists ]  数据库名 ;

删除：

- 删除数据库：drop database [ if exists ]  数据库名 ;

上述语法中的database，也可以替换成 schema。如：create schema db01;

命令行操作不方便：

DataGrip是JetBrains旗下的一款数据库管理工具，是管理和开发MySQL、Oracle、PostgreSQL的理想解决方案。

官网：[ https://www.jetbrains.com/zh-cn/datagrip/](https://www.jetbrains.com/zh-cn/datagrip/)

安装： 参考资料中提供的《DataGrip安装手册》

IDEAL也可！

![image-20231018000742510](https://gitee.com/coi4/test/raw/master/img/image-20231018000742510.png)

![image-20231018000753073](https://gitee.com/coi4/test/raw/master/img/image-20231018000753073.png)

![image-20231018000802533](https://gitee.com/coi4/test/raw/master/img/image-20231018000802533.png)

###### 3.1.2.2、表（创建、查询、修改、删除）

创建：

```
create table 表名(

 字段1 字段类型 [ 约束 ] [ comment 字段1注释 ] ,

 ......

 字段n 字段类型 [ 约束 ]  [ comment 字段n注释 ] 

) [ comment 表注释 ] ;
```

案例：

![image-20231020010347416](https://gitee.com/coi4/test/raw/master/img/image-20231020010347416.png)

```mysql
create table tb_user (
    id int primary key auto_increment comment 'ID,唯一标识', #主键自动增长
    username varchar(20) not null unique comment '用户名',
    name varchar(10) not null comment '姓名',
    age int comment '年龄',
    gender char(1) default '男' comment '性别'
) comment '用户表';
```

id有重复值：

约束：

- 概念：约束是作用于表中字段上的规则，用于限制存储在表中的数据。

- 目的：保证数据库中数据的正确性、有效性和完整性。

- | **约束** | **描述**                                         | **关键字**  |
  | -------- | ------------------------------------------------ | ----------- |
  | 非空约束 | 限制该字段值不能为null                           | not null    |
  | 唯一约束 | 保证字段的所有数据都是唯一、不重复的             | unique      |
  | 主键约束 | 主键是一行数据的唯一标识，要求非空且唯一         | primary key |
  | 默认约束 | 保存数据时，如果未指定该字段值，则采用默认值     | default     |
  | 外键约束 | 让两张表的数据建立连接，保证数据的一致性和完整性 | foreign key |

数据类型

- MySQL中的数据类型有很多，主要分为三类：数值类型、字符串类型、日期时间类型。

- ```sql
  示例: 
      年龄字段 ---不会出现负数, 而且人的年龄不会太大
  	age tinyint unsigned
  	
  	分数 ---总分100分, 最多出现一位小数
  	score double(4,1)
  示例： 
      用户名 username ---长度不定, 最长不会超过50
  	username varchar(50)
  	
  	手机号 phone ---固定长度为11
  	phone char(11)
  示例: 
  	生日字段  birthday ---生日只需要年月日  
  	birthday date
  	
  	创建时间 createtime --- 需要精确到时分秒
  	createtime  datetime
  ```

- 参照 [《MySQL](../资料/04. MySQL数据类型/MySQL数据类型.xlsx)[数据类型](../资料/04. MySQL数据类型/MySQL数据类型.xlsx)[》](../资料/04. MySQL数据类型/MySQL数据类型.xlsx)

>  根据页面原型/需求创建表(设计合理的数据类型、长度、约束)
>
> ![image-20231018001332872](https://gitee.com/coi4/test/raw/master/img/image-20231018001332872.png)
>
> create_time：记录的是当前这条数据插入的时间。 update_time：记录当前这条数据最后更新的时间。

```
设计一张表，基本的流程如下：

1. 阅读页面原型及需求文档

2. 基于页面原则和需求文档，确定原型字段(类型、长度限制、约束)

3. 再增加表设计所需要的业务基础字段(id主键、插入时间、修改时间)
```

查询：

- 查询当前数据库所有表：show tables;
- 查询表结构：desc 表名;
- 查询建表语句：show create table 表名;![img](https://gitee.com/coi4/test/raw/master/img/A84FB6E50E871D12AA20D26E868E09BC.png)

修改：

- 添加字段：alter table 表名 add 字段名 类型(长度) [comment 注释] [约束];
- 修改字段类型：alter table 表名 modify 字段名 新数据类型(长度);
- 修改字段名和字段类型：alter table 表名 change 旧字段名 新字段名 类型 (长度) [comment 注释] [约束];
- 删除字段：alter table 表名 drop column 字段名;
- 修改表名： rename table 表名 to 新表名;

删除：

- 删除表：drop table [ if exists ] 表名;
- ![image-20231018001703830](https://gitee.com/coi4/test/raw/master/img/image-20231018001703830.png)
- 在删除表时，表中的全部数据也会被删除。

##### 3.1.3、多表设计

###### 3.1.3.1、概述

项目开发中，在进行数据库表结构设计时，会根据业务需求及业务模块之间的关系，分析并设计表结构，由于业务之间相互关联，所以各个表结构之间也存在着各种联系，基本上分为三种：

- 一对多(多对一n)
- 多对多
- 一对一

###### 3.1.3.2、一对多

一对多关系实现：**在数据库表中多的一方，添加字段，来关联一的一方的主键**。

> 根据 页面原型 及 需求文档 ，完成部门（一）及员工（多）模块的表结构设计。
>
> ![image-20231018101830524](https://gitee.com/coi4/test/raw/master/img/image-20231018101830524.png)
>
> ![image-20231018101841943](https://gitee.com/coi4/test/raw/master/img/image-20231018101841943.png)

部门数据可以直接删除，然而还有部分员工归属于该部门下，此时就出现了数据的不完整、不一致问题。

目前上述的两张表，在数据库层面，并未建立关联，所以是无法保证数据的一致性和完整性的。——外键

外键语法：

```
-- 创建表时指定

create table 表名(

 字段名  数据类型,

 ...

 [constraint]  [外键名称] foreign key (外键字段名)  references  主表 (字段名) 

);

-- 建完表后，添加外键

alter table 表名 add constraint 外键名称 foreign key (外键字段名) references 主表(字段名);

alter table tb_emp  
add  constraint  fk_dept_id  foreign key (dept_id)  references  tb_dept(id);
```

![image-20231018102104570](https://gitee.com/coi4/test/raw/master/img/image-20231018102104570.png)

外键约束：

- 物理外键
  - 使用 foreign key 定义外键关联另外一张表。
  - 缺点：
    - 影响增、删、改的效率（需要检查外键关系）。
    - 仅用于单节点数据库，不适用与分布式、集群场景。
    - 容易引发数据库的死锁问题，消耗性能。
- 逻辑外键（推荐）
  - 在业务层逻辑中，解决外键关联。
  - 通过逻辑外键，就可以很方便的解决上述问题。

###### 3.1.3.3、一对一

> 案例: 用户 与 身份证信息 的关系
>
> 关系: 一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他字段放在另一张表中，以提升操作效率
>
> 实现: **在任意一方加入外键，关联另外一方的主键**，并且设置外键为唯一的(UNIQUE)
>
> ![image-20231018102414947](https://gitee.com/coi4/test/raw/master/img/image-20231018102414947.png)

###### 3.1.3.4、多对多

> 案例: 学生 与 课程的关系
>
> 关系: 一个学生可以选修多门课程，一门课程也可以供多个学生选择
>
> 实现: **建立第三张中间表，中间表至少包含两个外键，分别关联两方主键**
>
> ![image-20231018102625280](https://gitee.com/coi4/test/raw/master/img/image-20231018102625280.png)

###### 3.1.3.5、案例

> 参考资料中提供的 《[苍穹外卖](https://app.mockplus.cn/app/share-e928208474edd220b75e9faff1380e4ashare-VaH7dpoIaqRr/preview/BlJ_BHC42AEaa/tKNB7Tamh14B54?allowShare=1&cps=expand&ha=1)[_](https://app.mockplus.cn/app/share-e928208474edd220b75e9faff1380e4ashare-VaH7dpoIaqRr/preview/BlJ_BHC42AEaa/tKNB7Tamh14B54?allowShare=1&cps=expand&ha=1)[管理后台](https://app.mockplus.cn/app/share-e928208474edd220b75e9faff1380e4ashare-VaH7dpoIaqRr/preview/BlJ_BHC42AEaa/tKNB7Tamh14B54?allowShare=1&cps=expand&ha=1)》 页面原型，设计分类管理、菜品管理、套餐管理模块的表结构。

```
1.阅读页面原型及需求文档，分析各个模块涉及到的表结构，及表结构之间的关系。
2.根据页面原型及需求文档，分析各个表结构中具体的字段及约束。
```

示例：

> 思考：套餐与菜品之间是什么关系？
>
> - 思考逻辑：一个套餐下可以有多个菜品吗？反过来再想一想，一个菜品可以出现在多个套餐中吗？
>
> 答案：多对多关系。一个套餐下会有多个菜品，而一个菜品也可以出现在多个套餐中。
>
> 设计表原则：创建第三张中间表，建立两个字段分别关联菜品表的主键和套餐表的主键。

```mysql
-- 套餐菜品关联表
create table setmeal_dish
(
    id         int unsigned primary key auto_increment comment '主键ID',
    setmeal_id int unsigned     not null comment '套餐id ',    -- 逻辑外键
    dish_id    int unsigned     not null comment '菜品id',     -- 逻辑外键
    copies     tinyint unsigned not null comment '份数'
) comment '套餐菜品关联表';
```

#### 3.2、数据库操作

##### 3.2.1、操作-DML

DML英文全称是Data Manipulation Language(数据操作语言)，用来对数据库中表的数据记录进行增、删、改操作。

- 添加数据（INSERT）
- 修改数据（UPDATE）
- 删除数据（DELETE）

insert语法：

- 指定字段添加数据：insert into 表名 (字段名1, 字段名2) values (值1, 值2);
- 全部字段添加数据：insert into 表名 values (值1, 值2, ...);
- 批量添加数据（指定字段）：insert into 表名 (字段名1, 字段名2) values (值1, 值2), (值1, 值2);
- 批量添加数据（全部字段）：insert into 表名 values (值1, 值2, ...), (值1, 值2, ...);

注：

1. 插入数据时，指定的字段顺序需要与值的顺序是一一对应的。
2. 字符串和日期型数据应该包含在引号中。
3. 插入的数据大小，应该在字段的规定范围内。

UPDATE语法：

- 修改数据：update 表名 set 字段名1 = 值1 , 字段名2 = 值2 , .... [ where 条件 ] ;
- 修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据。
- 在修改数据时，一般需要同时修改公共字段update_time，将其修改为当前操作时间。

DELETE语法：

- 删除数据：delete from 表名 [ where 条件 ]

注：

1. DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据。
2. DELETE 语句不能删除某一个字段的值(如果要操作，可以使用UPDATE，将该字段的值置为NULL)。
3. 当进行删除全部数据操作时，会提示询问是否确认删除所有数据，直接点击Execute即可。 

##### 3.2.2、操作-DQL

DQL英文全称是Data Query Language(数据查询语言)，用来查询数据库表中的记录。

关键字：SELECT

![image-20231018002353491](https://gitee.com/coi4/test/raw/master/img/image-20231018002353491.png)

![image-20231018100823359](https://gitee.com/coi4/test/raw/master/img/image-20231018100823359.png)

基本查询：

- 查询多个字段：select 字段1, 字段2, 字段3 from  表名;

- 查询所有字段（通配符）：select *  from  表名;

- 设置别名：select 字段1 [ as 别名1 ] , 字段2 [ as 别名2 ]  from  表名;

  - 别名中有特殊字符时，使用''或""包含

- 去除重复记录：select distinct 字段列表 from  表名;

  - 查询已有的员工关联了哪几种职位(不要重复)

    - ```mysql
      select distinct job from tb_emp;
      ```

      

- *号代表查询所有字段，在实际开发中尽量少用（不直观、影响效率）。

条件查询（where）：

- 条件查询：select 字段列表 from  表名  where  条件列表 ;

- | **比较运算符**       | **功能**                                 |
  | -------------------- | ---------------------------------------- |
  | >                    | 大于                                     |
  | >=                   | 大于等于                                 |
  | <                    | 小于                                     |
  | <=                   | 小于等于                                 |
  | =                    | 等于                                     |
  | <> 或 !=             | 不等于                                   |
  | between ...  and ... | 在某个范围之内(含最小、最大值)           |
  | in(...)              | 在in之后的列表中的值，多选一             |
  | like 占位符          | 模糊匹配(_匹配单个字符, %匹配任意个字符) |
  | is null              | 是null                                   |

  - ```mysql
    select id, username, password, name, gender, image, job, entrydate, create_time, update_time
    from tb_emp
    where name = '杨逍'; -- 字符串使用''或""包含
    ```

- 查询为NULL的数据时，不能使用 `= null`

  - ```mysql
    select id, username, password, name, gender, image, job, entrydate, create_time, update_time
    from tb_emp
    where job is null ;
    ```

分组查询（group by）：

- 分组查询：select 字段列表 from  表名 [ where  条件 ] group  by 分组字段名 [ having 分组后过滤条件 ];

  - ```mysql
    select job, count(*)
    from tb_emp
    where entrydate <= '2015-01-01'   -- 分组前条件
    group by job                      -- 按照job字段分组
    having count(*) >= 2;             -- 分组后条件
    ```

- where与having的区别（面试题）

  - 执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤。
  - 判断条件不同：where不能对聚合函数进行判断，而having可以。

- 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义。

- 执行顺序: where > 聚合函数 > having 。

- 聚合函数

  - 将一列数据作为一个整体，进行**纵向**计算。

  - 语法：select 聚合函数(字段列表) from  表名 ;

  - null值不参与所有聚合函数运算。

  - 统计数量可以使用：count(*)  count(字段)  count(常量)，推荐使用count(*)。

  - | **函数** | **功能** |
    | -------- | -------- |
    | count    | 统计数量 |
    | max      | 最大值   |
    | min      | 最小值   |
    | avg      | 平均值   |
    | sum      | 求和     |

排序查询（order by）：

- 排序查询：select 字段列表 from  表名  [ where  条件列表 ] [ group by 分组字段 ] order by 字段1 排序方式1 , 字段2 排序方式2 … ;

  - ```mysql
    select id, username, password, name, gender, image, job, entrydate, create_time, update_time
    from tb_emp
    order by entrydate ASC; -- 按照entrydate字段下的数据进行升序排序
    
    select id, username, password, name, gender, image, job, entrydate, create_time, update_time
    from tb_emp
    order by  entrydate; -- 默认就是ASC（升序）
    ```

- 排序方式：

  - ASC：升序（默认值）
  - DESC：降序

- 如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序。

分页排序（limit）：

- 分页查询：select 字段列表 from  表名 limit 起始索引, 查询记录数 ;

  - ```mysql
    -- 查第3页
    select id, username, password, name, gender, image, job, entrydate, create_time, update_time
    from tb_emp
    limit 10 , 5; -- 从索引10开始，向后取5条记录
    ```

- 起始索引从0开始，起始索引 = （查询页码 - 1）* 每页显示记录数。

- 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT。

- 如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10。

- > 根据需求完成员工管理的条件分页查询
  >
  > ![image-20231018100521378](https://gitee.com/coi4/test/raw/master/img/image-20231018100521378.png)
  >
  > 根据需求，完成员工信息的统计
  >
  > ![image-20231018100620414](https://gitee.com/coi4/test/raw/master/img/image-20231018100620414.png)
  >
  > ![image-20231018100631012](https://gitee.com/coi4/test/raw/master/img/image-20231018100631012.png)

```mysql
select id, username, password, name, gender, image, job, entrydate, create_time, update_time
from tb_emp
where name like '张%' and gender = 1 and entrydate between '2000-01-01' and '2015-12-31'
order by update_time desc
limit 0 , 10;
```

```mysql
-- if(条件表达式, true取值 , false取值)
select if(gender=1,'男性员工','女性员工') AS 性别, count(*) AS 人数
from tb_emp
group by gender;
```

```mysql
-- case 表达式 when 值1 then 结果1  when 值2  then  结果2 ...  else  result  end
select (case job
             when 1 then '班主任'
             when 2 then '讲师'
             when 3 then '学工主管'
             when 4 then '教研主管'
             else '未分配职位'
        end) AS 职位 ,
       count(*) AS 人数
from tb_emp
group by job;
```

##### 3.2.3、多表查询

###### 3.2.3.1、概述

指从多张表中查询数据

笛卡尔积: 笛卡尔乘积是指在数学中，两个集合(A集合 和 B集合)的所有组合情况。(在多表查询时，需要消除无效的笛卡尔积)

![image-20231018103319032](https://gitee.com/coi4/test/raw/master/img/image-20231018103319032.png)

分类：

- 连接查询

  - 内连接：相当于查询A、B交集部分数据![image-20231018103735922](https://gitee.com/coi4/test/raw/master/img/image-20231018103735922.png)

    - ```mysql
      select tb_emp.name , tb_dept.name -- 分别查询两张表中的数据
      from tb_emp , tb_dept -- 关联两张表
      where tb_emp.dept_id = tb_dept.id; -- 消除笛卡尔积
      ```

    - ```mysql
      select emp.name , dept.name
      from tb_emp emp inner join tb_dept dept
      on emp.dept_id = dept.id;
      ```

  - 外连接![image-20231018103803856](https://gitee.com/coi4/test/raw/master/img/image-20231018103803856.png)

    - 左外连接：查询左表所有数据(包括两张表交集部分数据)
      - 以left join关键字左边的表为主表，查询主表中所有数据，以及和主表匹配的右边表中的数据
    - 右外连接：查询右表所有数据(包括两张表交集部分数据)

- 子查询

  - 概述：![image-20231018103917095](https://gitee.com/coi4/test/raw/master/img/image-20231018103917095.png)

  - 分类

    - 标量子查询：子查询返回的结果为单个值

      - 单个值（数字、字符串、日期等），最简单的形式

      - 常用的操作符：=  <>  >   >=   <  <=   

      - ```mysql
        select * from tb_emp where dept_id = (select id from tb_dept where name = '教研部');
        ```

    - 列子查询：子查询返回的结果为一列

      - 一列（可以是多行）

      - 常用的操作符：in 、not in等

      - ```mysql
        select * from tb_emp where dept_id in (select id from tb_dept where name = '教研部' or name = '咨询部');
        ```

    - 行子查询：子查询返回的结果为一行

      - 一行（可以是多列）。

      - 常用的操作符：= 、<> 、in 、not in

      - ```mysql
        select * from tb_emp where (entrydate,job) = (select entrydate , job from tb_emp where name = '韦一笑');
        ```

    - 表子查询：子查询返回的结果为多行多列

      - 多行多列，常作为临时表

      - 常用的操作符：in

      - ```mysql
        select e.*, d.* from (select * from emp where entrydate > '2006-01-01') e ， dept d where e.dept_id = d.id ;
        ```

###### 3.2.3.2、案例

> 1.查询价格低于 10元 的菜品的名称 、价格 及其 菜品的分类名称
>
> 2.查询所有价格在 10元(含)到50元(含)之间 且 状态为"起售"的菜品名称、价格及其分类名称 (即使菜品没有分类 , 也要将菜品查询出来)
>
> 3.查询每个分类下最贵的菜品, 展示出分类的名称、最贵的菜品的价格 .
>
> 4.查询各个分类下 菜品状态为 "起售" , 并且 该分类下菜品总数量大于等于3 的 分类名称
>
> 5.查询出 "商务套餐A" 中包含了哪些菜品 （展示出套餐名称、价格, 包含的菜品名称、价格、份数）
>
> 6.查询出低于菜品平均价格的菜品信息 (展示出菜品名称、菜品价格)

```mysql
/*查询技巧：
     明确1：查询需要用到哪些字段
        菜品名称、菜品价格 、 菜品分类名
     明确2：查询的字段分别归属于哪张表
        菜品表：[菜品名称、菜品价格]
        分类表：[分类名]
     明确3：如查多表，建立表与表之间的关联
        菜品表.caategory_id = 分类表.id
     其他：（其他条件、其他要求）
        价格 < 10
*/
select d.name , d.price , c.name
from dish AS d , category AS c
where d.category_id = c.id
      and d.price < 10;
```

```mysql
select d.name , d.price, c.name
from dish AS d left join category AS c on d.category_id = c.id
where d.price between 10 and 50
      and d.status = 1;
```

```mysql
select c.name , max(d.price)
from dish AS d , category AS c
where d.category_id = c.id
group by c.name;
```

```mysql
/*查询技巧：
     明确1：查询需要用到哪些字段
        分类名称、菜品总数量
     明确2：查询用到的字段分别归属于哪张表
        分类表：[分类名]
        菜品表：[菜品状态]
     明确3：如查多表，建立表与表之间的关联
        菜品表.caategory_id = 分类表.id
     其他：（其他条件、其他要求）
        条件：菜品状态 = 1 (1表示起售)
        分组：分类名
        分组后条件： 总数量 >= 3
*/
select c.name , count(*)
from dish AS d , category AS c
where d.category_id = c.id
      and d.status = 1 -- 起售状态
group by c.name  -- 按照分类名分组
having count(*)>=3; -- 各组后筛选菜品总数据>=3
```

```mysql
select s.name, s.price, d.name, d.price, sd.copies
from setmeal AS s , setmeal_dish AS sd , dish AS d
where s.id = sd.setmeal_id and sd.dish_id = d.id
      and s.name='商务套餐A';
```

```mysql
-- 1.计算菜品平均价格
select avg(price) from dish;    -- 查询结果：37.736842
-- 2.查询出低于菜品平均价格的菜品信息
select * from dish where price < 37.736842;

-- 合并以上两条SQL语句
select * from dish where price < (select avg(price) from dish);
```

##### 3.2.4、事务

###### 3.2.4.1、介绍&操作

事务：是一组操作的集合，它是一个不可分割的工作单位。事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作 要么同时成功，要么同时失败。

默认MySQL的事务是自动提交的，也就是说，当执行一条DML语句，MySQL会立即隐式的提交事务。

手动提交事务控制：

![image-20231018105720200](https://gitee.com/coi4/test/raw/master/img/image-20231018105720200.png)

> 手动提交事务使用步骤：
>
> - 第1种情况：开启事务  =>  执行SQL语句   =>  成功  =>  提交事务
> - 第2种情况：开启事务  =>  执行SQL语句   =>  失败  =>  回滚事务

###### 3.2.4.2、四大特性（面试题）

原子性（Atomicity）：事务是不可分割的最小单元，要么全部成功，要么全部失败

一致性（Consistency）：事务完成时，必须使所有的数据都保持一致状态

隔离性（Isolation）：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行；多个用户并发的访问数据库时，一个用户的事务不能被其他用户的事务干扰，多个并发的事务之间要相互隔离。一个事务的成功或者失败对于其他的事务是没有影响。

持久性（Durability）：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的；哪怕数据库发生异常，重启之后数据亦然存在。

#### 3.3、数据库优化

##### 3.3.1、索引

###### 3.3.1.1、介绍

索引（index）是帮助数据库 高效获取数据 的 数据结构 。

```mysql
-- 添加索引
create index idx_sku_sn on tb_sku (sn);  #在添加索引时，也需要消耗时间

-- 查询数据（使用了索引）
select * from tb_sku where sn = '100000003145008';
```

优点：

- 提高数据查询的效率，降低数据库的IO成本。
- 通过索引列对数据进行排序，降低数据排序的成本，降低CPU消耗。

缺点：

- 索引会占用存储空间。
- 索引大大提高了查询效率，同时却也降低了insert、update、delete的效率。

###### 3.3.1.2、结构

MySQL数据库支持的索引结构有很多，如：Hash索引、B+Tree索引、Full-Text索引等。我们平常所说的索引，如果没有特别指明，都是指默认的 B+Tree 结构组织的索引。

> 二叉查找树：左边的子节点比父节点小，右边的子节点比父节点大

B+Tree(多路平衡搜索树)：

- 每一个节点，可以存储多个key（有n个key，就有n个指针）。
- 节点分为：叶子节点、非叶子节点
  - 叶子节点，就是最后一层子节点，所有的数据都存储在叶子节点上
  - 非叶子节点，不是树结构最下面的节点，用于索引数据，存储的的是：key+指针
- 叶子节点形成了一颗双向链表，便于数据的排序及区间范围查询。
- ![image-20231018115527350](https://gitee.com/coi4/test/raw/master/img/image-20231018115527350.png)

###### 3.3.1.3、语法

创建索引：

###### ![image-20231018145804246](https://gitee.com/coi4/test/raw/master/img/image-20231018145804246.png)

```mysql
create index idx_emp_name on tb_emp(name);
```

查看索引：![image-20231018145911707](https://gitee.com/coi4/test/raw/master/img/image-20231018145911707.png)

删除索引：![image-20231018145922807](https://gitee.com/coi4/test/raw/master/img/image-20231018145922807.png)

主键字段，在建表时，会自动创建主键索引。

添加唯一约束时，数据库实际上会添加唯一索引。

### 4、Mybatis

Java程序操作数据库，现在主流的方式是：Mybatis。

MyBatis是一款优秀的 **持久层** 框架，用于简化JDBC的开发。

- 持久层：指的是就是数据访问层(dao)，是用来操作数据库的。
- 框架：是一个半成品软件，是一套可重用的、通用的、软件基础代码模型。在框架的基础上进行软件开发更加高效、规范、通用、可拓展。

MyBatis本是 Apache的一个开源项目iBatis, 2010年这个项目由apache迁移到了google code，并且改名为MyBatis 。2013年11月迁移到Github。

官网：https://mybatis.org/mybatis-3/zh/index.html 

#### 4.1、入门

##### 4.1.1、快速入门

使用Mybatis查询所有用户数据：

1. 准备工作(创建springboot工程、数据库表user、实体类User)![image-20231020190141984](https://gitee.com/coi4/test/raw/master/img/image-20231020190141984.png)
2. 引入Mybatis的相关依赖，配置Mybatis(数据库连接信息)在springboot项目中，可以编写application.properties文件![image-20231020190211082](https://gitee.com/coi4/test/raw/master/img/image-20231020190211082.png)
3. 编写SQL语句(注解/XML)springboot工程中，在引导类所在包下，在创建一个包 mapper。在mapper包下创建一个接口 UserMapper ，这是一个持久层接口（Mybatis的持久层接口规范一般都叫 XxxMapper）。![image-20231020190254622](https://gitee.com/coi4/test/raw/master/img/image-20231020190254622.png)
4. 单元测试![image-20231020190322245](https://gitee.com/coi4/test/raw/master/img/image-20231020190322245.png)

配置SQL提示：默认在mybatis中编写SQL语句是不识别的。可以做如下配置：

![image-20231018162122806](https://gitee.com/coi4/test/raw/master/img/image-20231018162122806.png)

![image-20231018162134355](https://gitee.com/coi4/test/raw/master/img/image-20231018162134355.png)

![image-20231018162142304](https://gitee.com/coi4/test/raw/master/img/image-20231018162142304.png)

产生原因：Idea和数据库没有建立连接，不识别表信息

解决方式：在Idea中配置MySQL数据库连接

##### 4.1.2、JDBC介绍（了解）

Mybatis框架，就是对原始的JDBC程序的封装。 

JDBC： ( Java DataBase Connectivity )，就是使用Java语言操作关系型数据库的一套API。

sun公司官方定义的一套操作所有关系型数据库的规范，即接口。

各个数据库厂商去实现这套接口，提供数据库驱动jar包。

我们可以使用这套接口（JDBC）编程，真正执行的代码是驱动jar包中的实现类。

缺点：硬编码、繁琐、资源浪费、性能降低

##### 4.1.3、数据库连接池

数据库连接池是个容器，负责分配、管理数据库连接(Connection)

它允许应用程序重复使用一个现有的数据库连接，而不是再重新建立一个

释放空闲时间超过最大空闲时间的连接，来避免因为没有释放连接而引起的数据库连接遗漏

优点：

- 资源重用
- 提升系统响应速度
- 避免数据库连接遗漏

标准接口：javax.sql.DataSource

- 官方(sun)提供的数据库连接池接口，由第三方组织实现此接口。

- 功能：获取连接

  - ```mysql
    public Connection getConnection() throws SQLException;
    ```

产品：C3P0、DBCP、Druid、Hikari

Druid（德鲁伊）

- Druid连接池是阿里巴巴开源的数据库连接池项目
- 功能强大，性能优秀，是Java语言最好的数据库连接池之一

切换Druid数据库连接池：

1. 在pom.xml文件中引入依赖

   - ```mysql
     <dependency>
         <!-- Druid连接池依赖 -->
         <groupId>com.alibaba</groupId>
         <artifactId>druid-spring-boot-starter</artifactId>
         <version>1.2.8</version>
     </dependency>
     ```

2. 在application.properties中引入数据库连接配置

   - ```mysql
     spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
     spring.datasource.url=jdbc:mysql://localhost:3306/mybatis
     spring.datasource.username=root
     spring.datasource.password=1234
     ```

官方地址：https://github.com/alibaba/druid/tree/master/druid-spring-boot-starter

##### 4.1.4、Lombok

Lombok是一个实用的Java类库，能通过注解的形式自动生成构造器、getter/setter、equals、hashcode、toString等方法，并可以自动化生成日志变量，简化和消除一些必须有但显得很臃肿的Java代码。

| **注解**            | **作用**                                                     |
| ------------------- | ------------------------------------------------------------ |
| @Getter/@Setter     | 为所有的属性提供get/set方法                                  |
| @ToString           | 会给类自动生成易阅读的  toString 方法                        |
| @EqualsAndHashCode  | 根据类所拥有的非静态字段自动重写 equals 方法和  hashCode 方法 |
| @Data               | 提供了更综合的生成代码功能（@Getter  + @Setter + @ToString + @EqualsAndHashCode） |
| @NoArgsConstructor  | 为实体类生成无参的构造器方法                                 |
| @AllArgsConstructor | 为实体类生成除了static修饰的字段之外带有各参数的构造器方法。 |

使用：

1. 在pom.xml文件中引入依赖

   - ```xml
     <!-- 在springboot的父工程中，已经集成了lombok并指定了版本号，故当前引入依赖时不需要指定version -->
     <dependency>
         <groupId>org.projectlombok</groupId>
         <artifactId>lombok</artifactId>
     </dependency>
     ```

2. 在实体类上添加注解

   - ```java
     import lombok.Data;
     
     @Data //getter方法、setter方法、toString方法、hashCode方法、equals方法
     @NoArgsConstructor //无参构造
     @AllArgsConstructor//全参构造
     public class User {
         private Integer id;
         private String name;
         private Short age;
         private Short gender;
         private String phone;
     }
     ```

Lombok会在编译时，自动生成对应的java代码。我们使用lombok时，还需要安装一个lombok的插件(idea自带)。

#### 4.2、基础操作

![image-20231018163145568](https://gitee.com/coi4/test/raw/master/img/image-20231018163145568.png)

准备：

- 准备数据库表 emp

- 创建一个新的springboot工程，选择引入对应的起步依赖（mybatis、mysql驱动、lombok）![img](https://gitee.com/coi4/test/raw/master/img/57E79C2BE381D00E1D4CA6C170A73E7D.png)

- application.properties中引入数据库连接信息

  - ```
    #驱动类名称
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
    #数据库连接的url
    spring.datasource.url=jdbc:mysql://localhost:3306/mybatis
    #连接数据库的用户名
    spring.datasource.username=root
    #连接数据库的密码
    spring.datasource.password=1234
    ```

- 创建对应的实体类 Emp（实体类属性采用驼峰命名）

  - ```
    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    public class Emp {
        private Integer id;
        private String username;
        private String password;
        private String name;
        private Short gender;
        private String image;
        private Short job;
        private LocalDate entrydate;     //LocalDate类型对应数据表中的date类型
        private Integer deptId;
        private LocalDateTime createTime;//LocalDateTime类型对应数据表中的datetime类型
        private LocalDateTime updateTime;
    }
    ```

- 准备Mapper接口 EmpMapper

  - ```
    /*@Mapper注解：表示当前接口为mybatis中的Mapper接口
      程序运行时会自动创建接口的实现类对象(代理对象)，并交给Spring的IOC容器管理
    */
    @Mapper
    public interface EmpMapper {
    
    }
    ```

![img](https://gitee.com/coi4/test/raw/master/img/421ED966754A2E8EFDBD22B435865275.png)

删除：

根据主键删除：

- SQL语句：![image-20231018163327084](https://gitee.com/coi4/test/raw/master/img/image-20231018163327084.png)

- 接口方法：![image-20231018163359819](https://gitee.com/coi4/test/raw/master/img/image-20231018163359819.png)

- @Delete注解：用于编写delete操作的SQL语句
- 如果mapper接口方法形参只有一个普通类型的参数，#{…} 里面的属性名可以随便写，如：#{id}、#{value}。

日志输出：

- 可以在application.properties中，打开mybatis的日志，并指定输出到控制台。
- ![image-20231018163540853](https://gitee.com/coi4/test/raw/master/img/image-20231018163540853.png)

预编译SQL：

- 优势：
  - 性能更高
  - 更安全（防止SQL注入）
- **SQL**注入是通过操作输入的数据来修改事先定义好的SQL语句，以达到执行代码对服务器进行攻击的方法。
- 性能更高：预编译SQL，编译一次之后会将编译后的SQL语句缓存起来，后面再次执行这条语句时，不会再次编译。（只是输入的参数不同）
- 更安全(防止SQL注入)：将敏感字进行转义，保障SQL的安全性。

参数占位符：

![image-20231018163741958](https://gitee.com/coi4/test/raw/master/img/image-20231018163741958.png)

![image-20231018163752383](https://gitee.com/coi4/test/raw/master/img/image-20231018163752383.png)

新增：

SQL语句：![image-20231018163909117](https://gitee.com/coi4/test/raw/master/img/image-20231018163909117.png)

接口方法：

![image-20231018163934609](https://gitee.com/coi4/test/raw/master/img/image-20231018163934609.png)

描述：在数据添加成功后，需要获取插入数据库数据的主键。如：添加套餐数据时，还需要维护套餐菜品关系表数据。

实现：

![image-20231018164019692](https://gitee.com/coi4/test/raw/master/img/image-20231018164019692.png)

![image-20231018164547004](https://gitee.com/coi4/test/raw/master/img/image-20231018164547004.png)

更新：

SQL语句（根据ID更新员工信息）：

![image-20231018164656694](https://gitee.com/coi4/test/raw/master/img/image-20231018164656694.png)

接口方法：

![image-20231018164719779](https://gitee.com/coi4/test/raw/master/img/image-20231018164719779.png)

查询

SQL语句：![image-20231018164743700](https://gitee.com/coi4/test/raw/master/img/image-20231018164743700.png)

接口方法：![image-20231018164803871](https://gitee.com/coi4/test/raw/master/img/image-20231018164803871.png)

```
@SpringBootTest
class SpringbootMybatisCrudApplicationTests {
    @Autowired
    private EmpMapper empMapper;

    @Test
    public void testGetById(){
        Emp emp = empMapper.getById(1);
        System.out.println(emp);
    }
}
```

数据封装：

- 实体类属性名 和 数据库表查询返回的字段名一致，mybatis会自动封装。
- 如果实体类属性名 和 数据库表查询返回的字段名不一致，不能自动封装。
- 起别名：在SQL语句中，对不一样的列名起别名，别名和实体类属性名一样
  - ![image-20231018165011397](https://gitee.com/coi4/test/raw/master/img/image-20231018165011397.png)
- 手动结果映射：通过@Results及@Result进行手动结果映射
  - ![image-20231018165101658](https://gitee.com/coi4/test/raw/master/img/image-20231018165101658.png)
- 开始驼峰命名（推荐）：如果字段名与属性名符合驼峰命名规则，mybatis会自动通过驼峰命名规则映射
- 驼峰命名规则：   abc_xyz    =>   abcXyz

  - 表中字段名：abc_xyz
  - 类中属性名：abcXyz
- 在application.properties中添加：
  - ![image-20231018165156679](https://gitee.com/coi4/test/raw/master/img/image-20231018165156679.png)

条件查询：

SQL语句：![image-20231018165247611](https://gitee.com/coi4/test/raw/master/img/image-20231018165247611.png)

接口方法：

![image-20231018165314653](https://gitee.com/coi4/test/raw/master/img/image-20231018165314653.png)

![image-20231018165324737](https://gitee.com/coi4/test/raw/master/img/image-20231018165324737.png)

参数名说明：

保证接口中方法的形参名和SQL语句中的参数占位符名相同。

参数名在不同的SpringBoot版本中，处理方案还不同：

- 在springBoot的2.x版本![image-20231018165447965](https://gitee.com/coi4/test/raw/master/img/image-20231018165447965.png)
- 在springBoot的1.x版本/单独使用mybatis（使用@Param注解来指定SQL语句中的参数名）![image-20231018165457184](https://gitee.com/coi4/test/raw/master/img/image-20231018165457184.png)

#### 4.3、XML映射文件

Mybatis的开发有两种方式：

1. 注解
2. XML

使用Mybatis的注解，主要是来完成一些简单的增删改查功能；复杂的SQL功能，建议使用XML来配置映射语句，也就是将SQL语句写在XML配置文件中。

规范：

- XML映射文件的名称与Mapper接口名称一致，并且将XML映射文件和Mapper接口放置在相同包下（同包同名）。
- XML映射文件的namespace属性为Mapper接口全限定名一致。
- XML映射文件中sql语句的id与Mapper 接口中的方法名一致，并保持返回类型一致。
- ![img](https://gitee.com/coi4/test/raw/master/img/FA08CBA9BCBC7CFB3E9748672ACE019A.png)
- \<select>标签：就是用于编写select查询语句的。

  - resultType属性，指的是查询返回的单条记录所封装的类型。

实现：

1. 创建xml映射文件

   1. ![img](https://gitee.com/coi4/test/raw/master/img/1F7C425F8E68475C6B4408FA320F50AE.png)
   2. ![img](https://gitee.com/coi4/test/raw/master/img/818DD955AECC74002C0411573D8FB7D2.png)

2. 编写

   1. ```
      <mapper namespace="com.itheima.mapper.EmpMapper">
      
          <!--查询操作-->
          <select id="list" resultType="com.itheima.pojo.Emp">
              select * from emp
              where name like concat('%',#{name},'%')
                    and gender = #{gender}
                    and entrydate between #{begin} and #{end}
              order by update_time desc
          </select>
      </mapper>
      ```

      

MybatisX 是一款基于 IDEA 的快速开发Mybatis的插件，为效率而生。

安装：![image-20231018165638626](https://gitee.com/coi4/test/raw/master/img/image-20231018165638626.png)

![img](https://gitee.com/coi4/test/raw/master/img/FB6DC20183E837287ABC239C51E70B93.png)

#### 4.4、动态SQL

随着用户的输入或外部条件的变化而变化的SQL语句，我们称为 动态SQL

<if>

- <if>：用于判断条件是否成立。使用test属性进行条件判断，如果条件为true，则拼接SQL。

  - ```
    <if test="条件表达式">
       要拼接的sql语句
    </if>
    ```

  - ```
    <select id="list" resultType="com.itheima.pojo.Emp">
            select * from emp
            where
        
                 <if test="name != null">
                     name like concat('%',#{name},'%')
                 </if>
                 <if test="gender != null">
                     and gender = #{gender}
                 </if>
                 <if test="begin != null and end != null">
                     and entrydate between #{begin} and #{end}
                 </if>
        
            order by update_time desc
    </select>
    ```

- <where>：where 元素只会在子元素有内容的情况下才插入where子句。而且会自动去除子句的开头的AND 或OR。

- ![image-20231018165854231](https://gitee.com/coi4/test/raw/master/img/image-20231018165854231.png)

> 动态更新员工信息，如果更新时传递有值，则更新；如果更新时没有传递值，则不更新。

- <set>：动态地在行首插入 SET 关键字，并会删掉额外的逗号。（用在update语句中）

  - ```
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
            "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <mapper namespace="com.itheima.mapper.EmpMapper">
    
        <!--更新操作-->
        <update id="update">
            update emp
            <!-- 使用set标签，代替update语句中的set关键字 -->
            <set>
                <if test="username != null">
                    username=#{username},
                </if>
                <if test="name != null">
                    name=#{name},
                </if>
                <if test="gender != null">
                    gender=#{gender},
                </if>
                <if test="image != null">
                    image=#{image},
                </if>
                <if test="job != null">
                    job=#{job},
                </if>
                <if test="entrydate != null">
                    entrydate=#{entrydate},
                </if>
                <if test="deptId != null">
                    dept_id=#{deptId},
                </if>
                <if test="updateTime != null">
                    update_time=#{updateTime}
                </if>
            </set>
            where id=#{id}
        </update>
    </mapper>
    ```

<foreach>

- SQL语句：![image-20231018170042407](https://gitee.com/coi4/test/raw/master/img/image-20231018170042407.png)

- 接口方法：![image-20231018170108142](https://gitee.com/coi4/test/raw/master/img/image-20231018170108142.png)
- XML映射文件：![image-20231018170120314](https://gitee.com/coi4/test/raw/master/img/image-20231018170120314.png)

- 属性：
  - collection：集合名称
  - item：集合遍历出来的元素
  - separator：每一次遍历使用的分隔符
  - open：遍历开始前拼接的片段
  - close：遍历结束后拼接的片段

<sql><include>

对重复的代码片段进行抽取，将其通过`<sql>`标签封装到一个SQL片段，然后再通过`<include>`标签进行引用。

-  <sql>：定义可重用的 SQL 片段（抽取重复代码）。

  - ```
    <sql id="commonSelect">
     	select id, username, password, name, gender, image, job, entrydate, dept_id, create_time, update_time from emp
    </sql>
    ```

-  <include>：通过属性refid，指定包含的sql片段（在原来抽取的地方进行引用)。

  - ```
    <select id="list" resultType="com.itheima.pojo.Emp">
        <include refid="commonSelect"/>
        <where>
            <if test="name != null">
                name like concat('%',#{name},'%')
            </if>
            <if test="gender != null">
                and gender = #{gender}
            </if>
            <if test="begin != null and end != null">
                and entrydate between #{begin} and #{end}
            </if>
        </where>
        order by update_time desc
    </select>
    ```

### 5、SpringBootweb综合

#### 5.1、案例

![image-20231020193936931](https://gitee.com/coi4/test/raw/master/img/image-20231020193936931.png)

##### 5.1.1、准备工作

了解需求：

![image-20231019222206055](https://gitee.com/coi4/test/raw/master/img/image-20231019222206055.png)

![image-20231019222216149](https://gitee.com/coi4/test/raw/master/img/image-20231019222216149.png)

环境搭建：

> 准备数据库表(dept、emp)
>
> 创建springboot工程，引入对应的起步依赖（web、mybatis、mysql驱动、lombok）
>
> 配置文件application.properties中引入mybatis的配置信息，准备对应的实体类
>
> 准备对应的Mapper、Service(接口、实现类)、Controller基础结构

![image-20231020193534037](https://gitee.com/coi4/test/raw/master/img/image-20231020193534037.png)

![image-20231020193557500](https://gitee.com/coi4/test/raw/master/img/image-20231020193557500.png)

开发规范

REST：表属性状态转换，是一种软件架构风格

![image-20231020193715854](https://gitee.com/coi4/test/raw/master/img/image-20231020193715854.png)

REST是风格，是约定方式，约定不是规定，可以打破。

描述模块的功能通常使用复数，也就是加s的格式来描述，表示此类资源，而非单个资源。如：users、emps、books…

响应结果：![image-20231020193916250](https://gitee.com/coi4/test/raw/master/img/image-20231020193916250.png)

##### 5.1.2、部门管理

查询部门：@GetMapping![image-20231020194126174](https://gitee.com/coi4/test/raw/master/img/image-20231020194126174.png)

前后端联调

删除部门：@PostMappping![image-20231020194202437](https://gitee.com/coi4/test/raw/master/img/image-20231020194202437.png)

新增部门：@postMapping![image-20231020194224783](https://gitee.com/coi4/test/raw/master/img/image-20231020194224783.png)

##### 5.1.3、员工管理

分页查询

分页查询带条件

删除员工

新增员工

文件上传：

- 本地存储
- 阿里云OSS

修改员工

配置文件：

- 参数配置话
- yml配置文件
- @ConfigurationRProperties

#### 5.2、登录认证

##### 5.2.1、登录功能

##### 5.2.2、登录校验

会话技术

JMT令牌

过滤器Filter

拦截器Interceptor

##### 5.2.3、异常处理

#### 5.3、AOP

事务管理

AOP基础

AOP英文全称：Aspect Oriented Programming（面向切面编程、面向方面编程），其实说白了，面向切面编程就是面向特定方法编程。 

**那面向这样的指定的一个或多个方法进行编程，我们就称之为 面向切面编程。**

作用：在程序运行期间在不修改源代码的基础上对已有方法进行增强（无侵入性: 解耦）

旨在管理bean对象的过程中底层使用动态代理机制，对特定的方法进行编程(功能增强)。

入门

步骤：

1. 导入依赖：在pom.xml中导入AOP的依赖

   - ```
     <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-aop</artifactId>
     </dependency>
     ```

2. 编写AOP程序：针对于特定方法根据业务需要进行编程

   - ```java
     @Component
     @Aspect //当前类为切面类
     @Slf4j
     public class TimeAspect {
     
         @Around("execution(* com.itheima.service.*.*(..))") 
         public Object recordTime(ProceedingJoinPoint pjp) throws Throwable {
             //记录方法执行开始时间
             long begin = System.currentTimeMillis();
     
             //执行原始方法
             Object result = pjp.proceed();
     
             //记录方法执行结束时间
             long end = System.currentTimeMillis();
     
             //计算方法执行耗时
             log.info(pjp.getSignature()+"执行耗时: {}毫秒",end-begin);
     
             return result;
         }
     }
     ```

核心概念：

1. 连接点：JoinPoint，可以被AOP控制的方法（暗含方法执行时的相关信息）如入门程序当中所有的业务方法都是可以被aop控制的方法。
2. 通知：Advice，指哪些重复的逻辑，也就是共性功能（最终体现为一个方法）
3. 切入点：PointCut，匹配连接点的条件，通知仅会在切入点方法执行时被应用
4. 切面：Aspect，描述通知与切入点的对应关系（通知+切入点）通过切面就能够描述当前aop程序需要针对于哪个原始方法，在什么时候执行什么样的操作。
   - 切面所在的类，我们一般称为**切面类**（被@Aspect注解标识的类）
5. 目标对象：Target，通知所应用的对象

AOP进阶

> Spring中AOP的通知类型：
>
> - @Around：环绕通知，此注解标注的通知方法在目标方法前、后都被执行
> - @Before：前置通知，此注解标注的通知方法在目标方法前被执行
> - @After ：后置通知，此注解标注的通知方法在目标方法后被执行，无论是否有异常都会执行
> - @AfterReturning ： 返回后通知，此注解标注的通知方法在目标方法后被执行，有异常不会执行
> - @AfterThrowing ： 异常后通知，此注解标注的通知方法发生异常后执行

在使用通知时的注意事项：

- @Around环绕通知需要自己调用 ProceedingJoinPoint.proceed() 来让原始方法执行，其他通知不需要考虑目标方法执行

- @Around环绕通知方法的返回值，必须指定为Object，来接收原始方法的返回值，否则原始方法执行完毕，是获取不到返回值的。

- ```
   @Around("execution(* com.itheima.service.*.*(..))")
      public Object around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
          log.info("around before ...");
            //调用目标对象的原始方法执行
          Object result = proceedingJoinPoint.proceed();
          
          //原始方法如果执行时有异常，环绕通知中的后置代码不会在执行了
          
          log.info("around after ...");
          return result;
      }
  ```

切入点重复——抽取

```
 @Pointcut("execution(* com.itheima.service.*.*(..))")
    private void pt(){

    }
    
    //前置通知（引用切入点）
    @Before("pt()")
    public void before(JoinPoint joinPoint){
        log.info("before ...");

    }
    
    @Around("pt()")
    public Object around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        log.info("around before ...");
        
         //调用目标对象的原始方法执行
        Object result = proceedingJoinPoint.proceed();
        //原始方法在执行时：发生异常
        //后续代码不在执行

        log.info("around after ...");
        return result;
    }
```

当切入点方法使用private修饰时，仅能在当前切面类中引用该表达式， 当外部其他切面类中也要引用当前类中的切入点表达式，就需要把private改为public，而在引用的时候，具体的语法为：

全类名.方法名()

```
@Before("com.itheima.aspect.MyAspect1.pt()")
    public void before(){
        log.info("MyAspect2 -> before ...");
```

通知顺序：

在不同切面类中，默认按照切面类的类名字母排序：

- 目标方法前的通知方法：字母排名靠前的先执行
- 目标方法后的通知方法：字母排名靠前的后执行

如果我们想控制通知的执行顺序有两种方式：

1. 修改切面类的类名（这种方式非常繁琐、而且不便管理）

2. 使用Spring提供的@Order注解切面类的执行顺序

   ```
   @Slf4j
   @Component
   @Aspect
   @Order(1) //切面类的执行顺序（前置通知：数字越小先执行; 后置通知：数字越小越后执行）
   public class MyAspect4 {
   ```

切入点表达式：

1. execution(……)：根据方法的签名来匹配

   - ```
     execution(访问修饰符?  返回值  包名.类名.?方法名(方法参数) throws 异常?)
     
     //其中带`?`的表示可以省略的部分
     ```

   - ```
     @Before("execution(void com.itheima.service.impl.DeptServiceImpl.delete(java.lang.Integer))")
     ```

   - 切入点表达式的语法规则：

     1. 方法的访问修饰符可以省略
     2. 返回值可以使用`*`号代替（任意返回值类型）
     3. 包名可以使用`*`号代替，代表任意包（一层包使用一个`*`）
     4. 使用`..`配置包名，标识此包以及此包下的所有子包
     5. 类名可以使用`*`号代替，标识任意类
     6. 方法名可以使用`*`号代替，表示任意方法
     7. 可以使用 `*`  配置参数，一个任意类型的参数
     8. 可以使用`..` 配置参数，任意个任意类型的参数

2. @annotation(……) ：根据注解匹配

   - 实现步骤：

     1. 编写自定义注解

        ```
        @Target(ElementType.METHOD)
        @Retention(RetentionPolicy.RUNTIME)
        public @interface MyLog {
        }
        ```

     2. 在业务类要做为连接点的方法上添加自定义注解

        - ```
           @Override
              @MyLog  //自定义注解（表示：当前方法属于目标方法）
              public void delete(Integer id) {
                  //1. 删除部门
                  deptMapper.delete(id);
              }
            
          ```

     3. 切面类：

        - ```
           @Before("@annotation(com.itheima.anno.MyLog)")
              public void before(){
                  log.info("MyAspect6 -> before ...");
              }
          ```

连接点：

- 对于@Around通知，获取连接点信息只能使用ProceedingJoinPoint类型

- 对于其他四种通知，获取连接点信息只能使用JoinPoint，它是ProceedingJoinPoint的父类型

- ```java
  @Slf4j
  @Component
  @Aspect
  public class MyAspect7 {
  
      @Pointcut("@annotation(com.itheima.anno.MyLog)")
      private void pt(){}
     
      //前置通知
      @Before("pt()")
      public void before(JoinPoint joinPoint){
          log.info(joinPoint.getSignature().getName() + " MyAspect7 -> before ...");
      }
      
      //后置通知
      @Before("pt()")
      public void after(JoinPoint joinPoint){
          log.info(joinPoint.getSignature().getName() + " MyAspect7 -> after ...");
      }
  
      //环绕通知
      @Around("pt()")
      public Object around(ProceedingJoinPoint pjp) throws Throwable {
          //获取目标类名
          String name = pjp.getTarget().getClass().getName();
          log.info("目标类名：{}",name);
  
          //目标方法名
          String methodName = pjp.getSignature().getName();
          log.info("目标方法名：{}",methodName);
  
          //获取方法执行时需要的参数
          Object[] args = pjp.getArgs();
          log.info("目标方法参数：{}", Arrays.toString(args));
  
          //执行原始方法
          Object returnValue = pjp.proceed();
  
          return returnValue;
      }
  }
  
  ```

AOP案例

#### 5.4、原理篇

##### 5.4.1、配置优先级

SpringBoot项目当中支持的三类配置文件：

- application.properties
- application.yml
- application.yaml

SpringBoot项目当中，我们要想配置一个属性，可以通过这三种方式当中的任意一种来配置都可以（推荐统一使用一种格式配置（yml是主流））

> 配置文件优先级排名（从高到低）：
>
> 1. properties配置文件
> 2. yml配置文件
> 3. yaml配置文件

除了支持配置文件的配置方式以外，还支持另外两种常见的配置方式：

1. Java系统属性配置 （格式： -Dkey=value）

   - ```
     -Dserver.port=9000
     ```

2. 命令行参数 （格式：--key=value）

   - ```
     --server.port=10010
     ```

![img](https://gitee.com/coi4/test/raw/master/img/74088DCBB150845112B60250E28C0946.png)

![img](https://gitee.com/coi4/test/raw/master/img/E6C5A37B3763D88C1AC9F93261CDAB1C.png)

> 优先级： 命令行参数 >  系统属性参数 > properties参数 > yml参数 > yaml参数

如果项目已经打包上线了：

1. 执行maven打包指令package，把项目打成jar文件![img](https://gitee.com/coi4/test/raw/master/img/1C284D6BED5F9207EFF5E8F5AA174BFB.png)

2. 使用命令：java -jar 方式运行jar文件程序，同时设置Java系统属性和命令行参数

   ![img](https://gitee.com/coi4/test/raw/master/img/F689542AA96A7CC54569117649712213.png)

##### 5.4.2、Bean管理

默认情况下，SpringBoot项目在启动的时候会自动的创建IOC容器(也称为Spring容器)，并且在启动的过程当中会自动的将bean对象都创建好，存放在IOC容器当中。

###### 5.4.2.1、主动获取Bean

1. 根据name获取bean

   - ```
     Object getBean(String name)
     ```

2. 根据类型获取bean

   - ```
     <T> T getBean(Class<T> requiredType)
     ```

3. 根据name获取bean（带类型转换）

   - ```
     <T> T getBean(String name, Class<T> requiredType)
     ```

```java
@SpringBootTest
class SpringbootWebConfig2ApplicationTests {

    @Autowired
    private ApplicationContext applicationContext; //IOC容器对象

    //获取bean对象
    @Test
    public void testGetBean(){
        //根据bean的名称获取
        DeptController bean1 = (DeptController) applicationContext.getBean("deptController");
        System.out.println(bean1);

        //根据bean的类型获取
        DeptController bean2 = applicationContext.getBean(DeptController.class);
        System.out.println(bean2);

        //根据bean的名称 及 类型获取
        DeptController bean3 = applicationContext.getBean("deptController", DeptController.class);
        System.out.println(bean3);
    }
}
```

###### 5.4.2.2、Bean作用域

设置bean对象为非单例

| **作用域**  | **说明**                                        |
| ----------- | ----------------------------------------------- |
| singleton   | 容器内同名称的bean只有一个实例（单例）（默认）  |
| prototype   | 每次使用该bean时会创建新的实例（非单例）        |
| request     | 每个请求范围内会创建新的实例（web环境中，了解） |
| session     | 每个会话范围内会创建新的实例（web环境中，了解） |
| application | 每个应用范围内会创建新的实例（web环境中，了解） |

可以借助Spring中的@Scope注解来进行配置作用域![img](https://gitee.com/coi4/test/raw/master/img/768BC8BD64752C9CEBD0138C27063C11.png)

###### 5.4.2.3、第三方Bean

第三方提供的类是只读的。无法在第三方类上添加@Component注解或衍生注解。

1. 在启动类上添加@Bean标识的方法
2. 在配置类中定义@Bean标识的方法

##### 5.4.3、SpringBoot管理

SpringBoot框架之所以使用起来更简单更快捷，是因为SpringBoot框架底层提供了两个非常重要的功能：一个是起步依赖，一个是自动配置。

通过SpringBoot所提供的起步依赖，就可以大大的简化pom文件当中依赖的配置，从而解决了Spring框架当中依赖配置繁琐的问题。

通过自动配置的功能就可以大大的简化框架在使用时bean的声明以及bean的配置。我们只需要引入程序开发时所需要的起步依赖，项目开发时所用到常见的配置都已经有了，我们直接使用就可以了。

> spring-webmvc依赖：这是Spring框架进行web程序开发所需要的依赖
>
> servlet-api依赖：Servlet基础依赖
>
> jackson-databind依赖：JSON处理工具包
>
> 如果要使用AOP，还需要引入aop依赖、aspect依赖
>
> 项目中所引入的这些依赖，还需要保证版本匹配，否则就可能会出现版本冲突问题

SpringBoot只需要引入Web开发的起步依赖：springboot-starter-web。

起步依赖的原理就是Maven的依赖传递。

SpringBoot项目在启动时通过自动配置完成了bean对象的创建。

当我们想要使用这些配置类中生成的bean对象时，可以使用@Autowired就自动注入了

### 6、后端开发总结

maven

SpringBoot入门、

MySQL、

mybatis

### 7、maven高级

#### 7.1、分模块设计与开发

?将项目按照功能拆分成若干个子模块，方便项目的管理维护、扩展，也方便模块间的相互调用，资源共享。

![image-20231021092123572](https://gitee.com/coi4/test/raw/master/img/image-20231021092123572.png)

步骤：

- 创建maven模块 tlias-pojo，存放实体类。
- 创建maven模块 tlias-utils，存放相关工具类。

分模块开发需要先针对模块功能进行设计，再进行编码。不会先将工程开发完毕，然后进行拆分。

#### 7.2、继承与聚合

##### 7.2.1、继承

###### 7.2.1.1、继承关系

继承描述的是两个工程间的关系，与java中的继承相似，子工程可以继承父工程中的配置信息，常见于依赖关系的继承。

作用：简化依赖配置、统一管理依赖

实现：<parent> … </parent>

1. 创建maven模块 tlias-parent ，该工程为父工程，设置打包方式pom(默认jar)。![image-20231021092738262](https://gitee.com/coi4/test/raw/master/img/image-20231021092738262.png)
2. 在子工程的pom.xml文件中，配置继承关系。![image-20231021092900233](https://gitee.com/coi4/test/raw/master/img/image-20231021092900233.png)
   - 在子工程中，配置了继承关系之后，坐标中的groupId是可以省略的，因为会自动继承父工程的 。
   - relativePath指定父工程的pom文件的相对位置（如果不指定，将从本地仓库/远程仓库查找该工程）。
3.  在父工程中配置各个工程共有的依赖（子工程会自动继承父工程的依赖）。![image-20231021092950211](https://gitee.com/coi4/test/raw/master/img/image-20231021092950211.png)
   - 若父子工程都配置了同一个依赖的不同版本，以子工程的为准。

> jar：普通模块打包，springboot项目基本都是jar包（内嵌tomcat运行）
>
> war：普通web程序打包，需要部署在外部的tomcat服务器中运行
>
> pom：父工程或聚合工程，该模块不写代码，仅进行依赖管理

###### 7.2.1.2、版本锁定

在maven中，可以在父工程的pom文件中通过 <dependencyManagement> 来统一管理依赖版本。

子工程引入依赖时，无需指定 <version> 版本号，父工程统一管理。变更依赖版本，只需在父工程中统一变更。

<dependencyManagement> 与 <dependencies>的区别是什么?

- <dependencies> 是直接依赖,在父工程配置了依赖,子工程会直接继承下来。 
- <dependencyManagement> 是统一管理依赖版本,不会直接依赖，还需要在子工程中引入所需依赖(无需指定版本)

##### 7.2.2、聚合

聚合

   将多个模块组织成一个整体，同时进行项目的构建。

聚合工程

   一个不具有业务功能的“空”工程（有且仅有一个pom文件）

作用

   快速构建项目（无需根据依赖关系手动构建，直接在聚合工程上构建即可）

maven中可以通过 <modules> 设置当前聚合工程所包含的子模块名称

聚合工程中所包含的模块，在构建时，会自动根据模块间的依赖关系设置构建顺序，与聚合工程中模块的配置书写位置无关。

> 继承与聚合：
>
> 作用
>
> - 聚合用于快速构建项目
> - 继承用于简化依赖配置、统一管理依赖
>
> 相同点：
>
> - 聚合与继承的pom.xml文件打包方式均为pom，可以将两种关系制作到同一个pom文件中
> - 聚合与继承均属于设计型模块，并无实际的模块内容
>
> 不同点：
>
> - 聚合是在聚合工程中配置关系，聚合可以感知到参与聚合的模块有哪些
> - 继承是在子模块中配置关系，父模块无法感知哪些子模块继承了自己

#### 7.3、私服

私服是一种特殊的远程仓库，它是架设在局域网内的仓库服务，用来代理位于外部的中央仓库，用于解决团队内部的资源共享与资源同步问题。

私服在企业项目开发中，一个项目/公司，只需要一台即可（无需我们自己搭建，会使用即可）。

![image-20231021093604762](https://gitee.com/coi4/test/raw/master/img/image-20231021093604762.png)

1. 设置私服的访问用户名/密码（settings.xml中的servers中配置）![image-20231021093628044](https://gitee.com/coi4/test/raw/master/img/image-20231021093628044.png)
2. IDEA的maven工程的pom文件中配置上传（发布）地址![image-20231021093741522](https://gitee.com/coi4/test/raw/master/img/image-20231021093741522.png)
3. 设置私服依赖下载的仓库组地址（settings.xml中的mirrors、profiles中配置）