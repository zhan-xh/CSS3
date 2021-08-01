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
### 4.4 基本单位

## 5. float布局
## 6. flex布局
## 7. grid布局
