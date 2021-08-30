# CSS3学习笔记
哪些浏览器支持css的某个元素特性?
一个在线网站可以查询[点击](caniuse.com)
## 1. CSS reset
```css
*{
    margin:0;
    padding:0
    box-sizing:border-box;
}
ol,ul{
    list-style:none;
}
a{
    text-decoration:none;
}
table{
    border-collapse:collapse;
    border-spacing:0;
}
```
## 2. 体系化学习css
搜索css文档 css spec
### 2.1 语法
选择器{
    属性名:属性值;
}
css区分大小写,注释只有/* */
### 2.2 at语法
* @charset"utf-8" 必须放在第一行
* @import url(2.css)
* @meida(min-width:100px;){
    语法一
}?
### 2.3 调试css
* w3c验证器
* vscode看代码颜色
* webstorm
* 开发者工具看警告
### 2.4 border 调试法
使用时每个样式都写
border:1px solid red;
看位置是否生效,逐行换调试
### 2.5 关于查资料
* 关键词+mdn
* css tricks
* 张鑫旭的博客
### 2.6 规范权威
w3c
css2.1中文版,遇到问题再查
## 3. 文档流
### 3.1 经验
写多个span
span{第$个span}*8 Tab
### 3.2 inline内联
内联:默认从左到右,默认合并在一起
块级:类似div,从上至下,独占一行 block元素
具体某个元素是否内联,看怎么写样式
inline-block不会截断,inline在最后宽度不够时,会阶段从第二行开始
```css
div{
display:inline;
display:block;
}
```
### 3.3 注意事项
1. inline元素不接受width指定
2. div在未确认width时,width默认auto,有多宽占多宽,不是100%
3. block默认自动计算width,也可以width指定,inline-block也可以指定width
4. inline元素的高度由line-height间接确定,与字体有关,与height无关
5. block和inline-block都可以设置height
6. 当div中没有内容时,高为0

### 3.4 溢出overflow的处理方法
1. overflow:hidden;
2. overflow:scroll;
3. overflow:auto;

### 3.5 脱离文档流
当使用float布局时可以脱离文档流
float:left;
或者 position:absolute/fixed;
当脱离文档流时,就不算在内容高度里了

## 4. 盒模型
margin是外边距,padding是内边距
### 4.1 content-box与border-box
width只含content的盒子就是content-box,包含border padding content的盒子就是border-box
### 4.2 经验
1. vscode输入.borderbox ->Tab 自动生成 <div class="borderbox"></div>
2. 选择盒模型 box-sizing:border-box;
3. 引入外部css样式表 html头部添加 <link rel="stylesheet" href="style.css" type="text/css">
### 4.3 margin合并
1. 两个孩子之间的上下margin会合并，即是孩子1 的下margin会与孩子2的上margin合并为一个margin，可以用以下代码改变。
```css
display:inline-block;
```
2. 第一个与最后一个孩子的margin会与parent的margin合并，若不想合并的话有三种解决方式：
* 加padding
* 加overflow:hidden
* 加border
3. margin只有上下合并，没有左右合并
4. margin合并之间必须没有其他东西，例如padding，有的话就无法合并
### 4.4 基本单位
1. 长度单位(mdn 搜索width)
* px 像素
* em 相对于自身font-size的倍数
```css
.div{
    font-size:20px;
    border:1px solid red;
    width:3em;/*  3*font-size=3*20px */
}
```
* 百分数
* rgb(0,0,0)  rgba(255,0,127,0) 
可以直接使用qq截图取色，按下ctrl即可切换16进制,rgba可以设置透明度，0为全透明，1为不透明
* hsl(360,100%,100%)  hsl(色相,饱和度,亮度) 
## 5. float布局
先说明：
一般要兼容老的浏览器使用flex布局，要兼容IE9，使用float布局，如果只兼容最新的浏览器，使用grid布局
### 5.1 步骤
1. 子元素加width和flaot:left;
2. 在父元素上写 .clearfix 固定写法
div加了float就脱离了文档流了，标签里面的内容为空，加入clearfix就不会了
```css
.clearfix:after{
    content:'';
    display:block;
    clear:all;
}
```
### 5.2 经验
1. 最后一个div不写width，但可以写最大宽度
2. float是针对IE的，无法响应式
3. 尽量采用display:inline-block;
4. 网页的背景图片，右键检查可以得到地址，可以在img标签使用
5. outline:1px solid red; 不占宽度的border
5. margin：0 auto；自动居中
但是以下方式更好
```css
margin-left:auto;
margin-right:auto;
```
6. 可以采用负margin来实现平均布局，中间加个x（clearfix）可以消除float，外边距也不会合并
## 6. flex布局
### 6.1 使用flex布局
1. 采用flex布局
```css
body{
display:flex | inline-flex;
}

```
2. 控制流动方向
```css
.container{
    flex-direction:row | row-reverse | column | column-reverse;
}
```
3. 控制是否换行
```css
.container{
    flex-wrap:wrap | nowrap;
}
```
4. 控制对齐方式
```css
.container{
    justify-content: flex-start | flex-end;
    /*从行首或者行尾开始*/
}
```
flex具有多种灵活多变的对齐方式，具体参考MDN文档[justify-content](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-content)
5. item的属性
* order 排序
可以利用order改变item的显示顺序，order默认为0
```css
.item:first-child{
    order:5;
}
.item:nth-child(2){
    order:100;
}
.item:nth-child(3){
    order:30;
}
.item:last-child{
    order:5;
}
```
6. flex-grow 剩余空间分配
这个属性主要是控制item多余空间的分配，不写的话默认为0
flex-grow:0;的意思不是宽度为0 ，而是只更具内容来确定宽度
```css
.item:first-child{
    flex-grow:1;
}
.item:nth-child(2){
    flex-grow:2;
}
```
以上代码的意思是，在容器中剩余的空间里，平均分成三份，第一个孩子占一份，第二个孩子占2份。
7. flex-shrink  元素的收缩
flex 元素仅在默认宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值。
默认是1，代表当内容空间不足时，大家一起收缩。
当flex-shrink:0;时是防止变瘦，无论多窄我都不收缩，比如淘宝就是这样设计的。
8. align-items 交叉轴方向上的对齐方式
例如
```css
.container{
    align-items:center; /*居中 主轴横向对齐*/
}
.container2{
    justify-content:center | space-between; 
}
```
### 6.2 flex 实践
1. vertical-align 垂直对齐
```css
.logo{
    vertical-align:middle;
}
```
以上使用方法常常用在图片logo上，防止出现奇怪的空隙。
2. 不要轻易把width和height都写死，因为用户使用不同的设备观看，但可以写最大最小宽度
```css
.container{
    min-width:500px;
    max-width:500px;
```
3. flex基本可以满足所有布局
flex的MDN详细解释[Flexbox](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
## 7. grid布局
在css布局中，如果是一维布局我们采用flex，二维布局采用grid
在grid布局中，分container和items
grid尤其适合不规则布局，像衣柜一样的布局都可以使用grid
### 7.1 成为container items

```css
.container{
    display:grid | inline-grid;
}
.container{
    grid-template-columns:40px 50px auto 50px 40px;
    grid-template-rows:25% 100px auto;
    
}
.item-a{
    /*item可以设置范围，其中数字代表线条的名字*/
    grid-column-start:2;
    grid-column-end:3;
    grid-row-start:1;
    grid-row-end:3;
}

```
### 7.2 fr 份
比如分成2行3列
```css
.container{
    display:grid;
    grid-template-columns:1fr 1fr 1fr;
    grid-template-rows:1fr 1fr;
    grid-gap:12px;/*格子间隙*/
}
```
### 7.3 grid-template-areas 分区
![示意图](D:\WEB\CSS3\grid-template-areas.png)
html
```html
<body>
<div class="container">
    <header>herder</header>
    <aside>aside</aside>
    <main>main</main>
    <div class="ad">ad</div>
    <footer>footer</footer>
</div>
</body>
```
css代码部分
```css
   .container {
            min-height: 100vh;
            display: grid;
            grid-template-rows: 60px auto 60px;
            grid-template-columns: 100px auto 100px;
            grid-template-areas: 
            "header header header"
            "aside  aside  aside"
            "footer  footer footer"
        }
        .container >*{
            border: 1px solid red;
        }
        .container > header{
            grid-area: header;
        }
        .container >aside{
            grid-area: aside;
        }
        .container>main{
            grid-area: main;
        }
        .container> .ad{
            grid-area: ad;
        }
        .container>footer{
            grid-area: footer;
        }
```
