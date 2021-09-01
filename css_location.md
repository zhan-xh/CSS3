<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [CSS定位](#css%E5%AE%9A%E4%BD%8D)
  - [1 一个div的分层](#1-%E4%B8%80%E4%B8%AAdiv%E7%9A%84%E5%88%86%E5%B1%82)
    - [div分层 从上往下](#div%E5%88%86%E5%B1%82-%E4%BB%8E%E4%B8%8A%E5%BE%80%E4%B8%8B)
  - [2 position的5个取值](#2-position%E7%9A%845%E4%B8%AA%E5%8F%96%E5%80%BC)
    - [2.1相对定位](#21%E7%9B%B8%E5%AF%B9%E5%AE%9A%E4%BD%8D)
    - [2.2 绝对定位](#22-%E7%BB%9D%E5%AF%B9%E5%AE%9A%E4%BD%8D)
      - [使用场景](#%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)
    - [2.3 固定定位fixed](#23-%E5%9B%BA%E5%AE%9A%E5%AE%9A%E4%BD%8Dfixed)
      - [使用场景](#%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF-1)
        - [经验](#%E7%BB%8F%E9%AA%8C)
    - [2.4 粘贴定位 sticky](#24-%E7%B2%98%E8%B4%B4%E5%AE%9A%E4%BD%8D-sticky)
      - [经验](#%E7%BB%8F%E9%AA%8C-1)
  - [层叠上下文](#%E5%B1%82%E5%8F%A0%E4%B8%8A%E4%B8%8B%E6%96%87)
    - [如何创建一个作用域](#%E5%A6%82%E4%BD%95%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E4%BD%9C%E7%94%A8%E5%9F%9F)
    - [注意](#%E6%B3%A8%E6%84%8F)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# CSS定位

## 1 一个div的分层
首先需要明确一个点：布局是屏幕平面上的，而定位是垂直于屏幕上的，background是包含border的，即是background处于border更下一层。
### div分层 从上往下
定位元素z-index为正的元素，在所有元素之上，只要是正常文字，不管出现在那个div里，根据先后出现覆盖。
* 定位元素（z-index=0 | 1| 2.....）
* 内联子元素(文字内容)
* 浮动元素（float:left | right）//脱离了文档流，比之前上升了一点，即是浮动
* 块级子元素(div)
* border
* background
* 定位元素(z-index=-1)
## 2 position的5个取值
默认值
position:static;
即是当前元素在文档流中，一般不升起来，不脱离文档流。
### 2.1相对定位
1. 用于位移
这种定位占的位置不变，但显示的位置根据代码有所偏移。
其他元素任然认为其在原位。
```css
.container{
position:relative;
top:10px;
left:10px;
}
```
2. 用于给绝对定位absolute做父亲

3. 配合z-index使用
z-index默认每个元素都是auto，但是计算出来是0
z-index=1;压住0，不会覆盖别人
z-index=-1;使其向下沉，比0小

### 2.2 绝对定位
position:absolute;
#### 使用场景
1. 脱离原来的位置，另起一层，比如对话框的关闭。
一般关闭按钮都用绝对定位来做，相对于父元素祖先元素定位。
使用绝对定位必须有个父元素，在其父元素上加
position:relative;
儿子用
```css
.child{
    position:absolute;
    top:0;
    right:0;
}
```
2. 鼠标提示
white-space:nowrap;//文字内容不允许换行
html
```html
<button>点击
    <span class="tips">提示内容</span>
</button>

```
css代码
```css
  button {
            position: relative;
        }

        button span {
            position: absolute;
            border: 1px solid red;
            white-space: nowrap;
            bottom: calc(100%+10px);
            left: 50%;
            transform: translateX(-50%);
        }

        button span {
            display: none;
        }

        button:hover span {
            display: inline-block;
        }
```
注意：
* absolute是相对于祖先元素中最近的一个定位元素(position不是static)定位的。
* 某些浏览器不写top和right位置会发生错乱。
* left：100%;指的是距左100% 善用
* 善用left：50%; 加上负margin 能很好的居中显示
* 展示一个hover：chrome控制台-> style右上角：hov -> 勾上hover
### 2.3 固定定位fixed
position:fixed;
#### 使用场景
1. 烦人的广告
相对于视口定位
```css
   .fixed{
            position: fixed;
            left: 10px;
            bottom: 10px;
        }
```
让一个东西居中
```css
    .container{
            display: flex;
            justify-content: center;
            align-items: center;
        }
     
```
##### 经验
* 不要把fixed属性放在一个含有transform属性的元素里，会出现bug。
* 可以做一个回到顶部按钮
* 手机上尽量不要用fixed，坑很多。

### 2.4 粘贴定位 sticky
当未到我时，我就像文档流一样向上滑动，当我到顶快要看不见时，我就像粘在顶部一样，不动了，特别适合标题导航之类，但兼容性不好，许多浏览器不能使用。
```css
.container{
    position: -webkit-sticky;
    top: 0;
}
```

#### 经验
* 如果写了absolute，一般都要补一个relative
* 若写了absolute或者fixed，一定要补一个top和left

## 层叠上下文
MDN文档参考 [css层叠上下文](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
z-index谁的数值大，谁的层数就高，就可以覆盖别人，默认z-index=0;
当z-index=-1|-2|-3;则其层数比background更低。
从上往下，层数降低
* 定位元素（z-index=0 | 1| 2.....）
* 内联子元素(文字内容)
* 浮动元素（float:left | right）//脱离了文档流，比之前上升了一点，即是浮动
* 块级子元素(div)
* border
* background
* 定位元素(z-index=-1)
每一个层叠上下文相当于一个小世界作用域，处在同一个世界的z-index才可以比较，不同作用域的z-index无法比较。
### 如何创建一个作用域
当
position:relative;
1. 令z-index=0;注意不是auto，auto不会创建层叠上下文
2. display:flex;
3. opacity 只要不为1就可以创建
4. position:fixed;
5. transform:none;


### 注意
默认层叠上下文是html元素，html会把所有元素包裹起来