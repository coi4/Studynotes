# JavaWeb开发教程（2023）



* 课程路线：

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

method属性：用来设置请求方式的

data属性：作为请求体被发送的数据；如果是post请求，数据需要作为data属性的值

then（）需要传递一个匿名函数。该匿名函数被称为回调函数，意思是该匿名函数在发送请求时不会被调用，而是在成功响应后调用的函数。而该回调函数中result参数是对相应的数据进行封装的对象，通过result.data可以获取到相应的数据

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



#### 4.2、前后端分离开发

![image-20231014174021330](https://gitee.com/coi4/test/raw/master/img/image-20231014174021330.png)

![image-20231014174103993](https://gitee.com/coi4/test/raw/master/img/image-20231014174103993.png)

YApi

* YApi 是高效、易用、功能强大的 api 管理平台，旨在为开发、产品、测试人员提供更优雅的接口管理服务
*  http://yapi.smart-xwork.cn/

添加项目、添加分类、添加接口

#### 4.3、前端工程化

在企业级的前端项目开发中，把前端开发所需的工具、技术、流程、经验等进行规范化、标准化。

![image-20231014174727460](https://gitee.com/coi4/test/raw/master/img/image-20231014174727460.png)

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
   - 图形化界面：![image-20231014175455923](https://gitee.com/coi4/test/raw/master/img/image-20231014175455923.png)

2. 目录构建

   - 基于Vue脚手架创建出来的工程，有标准的目录结构，如下：

     ![image-20231014175637792](https://gitee.com/coi4/test/raw/master/img/image-20231014175637792.png)

![image-20231014175655859](https://gitee.com/coi4/test/raw/master/img/image-20231014175655859.png)

​    3.启动

![image-20231014180408645](https://gitee.com/coi4/test/raw/master/img/image-20231014180408645.png)

![image-20231014180433483](https://gitee.com/coi4/test/raw/master/img/image-20231014180433483.png)

  4.配置端口

![image-20231014180604113](https://gitee.com/coi4/test/raw/master/img/image-20231014180604113.png)

##### 4.3.3、Vue项目开发流程

![image-20231014180856789](https://gitee.com/coi4/test/raw/master/img/image-20231014180856789.png)

Vue的组件文件以 .vue结尾，每个组件由三个部分组成：<template> 、<script>、<style> 。

#### 4.4、Vue组件库Element

Element：是饿了么团队研发的，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库。

组件：组成网页的部件，例如 超链接、按钮、图片、表格、表单、分页条等等。

官网：[https://element.eleme.cn/#/zh-CNListener](https://element.eleme.cn/)

##### 4.4.1、快速入门

1. 安装ElementUI组件库 （在当前工程的目录下），在命令行执行指令：	![image-20231014181410153](https://gitee.com/coi4/test/raw/master/img/image-20231014181410153.png)
2. 引入ElementUI组件库：![image-20231014181508376](https://gitee.com/coi4/test/raw/master/img/image-20231014181508376.png)
3. 访问官网，复制组件代码，调整

##### 4.4.2、常见组件

* Table 表格：用于展示多条结构类似的数据，可对数据进行排序、筛选、对比或其他自定义操作
* Pagination 分页：当数据量过多时，使用分页分解数据
* Dialog 对话框：在保留当前页面状态的情况下，告知用户并承载相关操作
* From 表单：由输入框、选择器、单选框、多选框等控件组成，用以收集、校验、提交数据

##### 4.4.3、案例

- 根据页面原型完成员工管理页面开发，并通过Axios完成数据异步加载。

![image-20231014182505745](https://gitee.com/coi4/test/raw/master/img/image-20231014182505745.png)

- 服务端数据获取地址：http://yapi.smart-xwork.cn/mock/169327/emp/list

  ![image-20231014182555721](https://gitee.com/coi4/test/raw/master/img/image-20231014182555721.png)

  - 创建页面，完成页面的整体布局规划
  - 布局中各个部分的组件实现
  - 列表数据的异步加载，并渲染展示

- Vue项目中使用Axios:

  - 在项目目录下安装axios：npm install axios;
  - 需要使用axios时，导入axios：import axios from 'axios';

#### 4.5、Vue路由

![image-20231014182808578](https://gitee.com/coi4/test/raw/master/img/image-20231014182808578.png)

* 介绍： Vue Router 是 Vue 的官方路由。
* 组成：
  * VueRouter：路由器类，根据路由请求在路由视图中动态渲染选中的组件
  * <router-link>：请求链接组件，浏览器会解析成<a>
  * <router-view>：动态视图组件，用来渲染展示与路由路径对应的组件

1. 安装（创建Vue项目时已选择）![image-20231014183150672](https://gitee.com/coi4/test/raw/master/img/image-20231014183150672.png)

2. 定义路由

   ![image-20231014183349241](https://gitee.com/coi4/test/raw/master/img/image-20231014183349241.png)

##### 4.5.1、案例

通过Vue的路由VueRouter完成左侧菜单栏点击切换效果

![image-20231014183515951](https://gitee.com/coi4/test/raw/master/img/image-20231014183515951.png)

```
<router-link to="/dept">部门管理</router-link>
<router-link to="/emp">员工管理</router-link>
```

```
<router-view></router-view>
```

#### 4.6、打包部署

##### 4.6.5、打包

![image-20231014184037307](https://gitee.com/coi4/test/raw/master/img/image-20231014184037307.png)

##### 4.6.6、部署

将打包好的 dist 目录下的文件，复制到nginx安装目录的html目录下。

双击 nginx.exe 文件即可，Nginx服务器默认占用 80 端口号，如果80端口号被占用，可以在nginx.conf中修改端口号。(netstat –ano | findStr 80)

- 介绍：Nginx是一款轻量级的Web服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。其特点是占有内存少，并发能力强，在各大型互联网公司都有非常广泛的使用。

- 官网：https://nginx.org/
- ![image-20231014184150729](https://gitee.com/coi4/test/raw/master/img/image-20231014184150729.png)



## 二、后端Web开发

### 1、maven-SpringBootWeb入门

### 2、MySQL

### 3、Mybatis

### 4、SpringBootweb

### 5、maven高级