<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [transform全解 transition](#transform%E5%85%A8%E8%A7%A3-transition)
  - [经验技巧](#%E7%BB%8F%E9%AA%8C%E6%8A%80%E5%B7%A7)
  - [1.位移translate](#1%E4%BD%8D%E7%A7%BBtranslate)
    - [位移](#%E4%BD%8D%E7%A7%BB)
    - [指定视点 z轴](#%E6%8C%87%E5%AE%9A%E8%A7%86%E7%82%B9-z%E8%BD%B4)
    - [translate 3d](#translate-3d)
  - [2.缩放scale](#2%E7%BC%A9%E6%94%BEscale)
  - [3. 旋转rotate](#3-%E6%97%8B%E8%BD%ACrotate)
  - [4. 倾斜 skew](#4-%E5%80%BE%E6%96%9C-skew)
  - [5. 多重使用 用空格隔开就好](#5-%E5%A4%9A%E9%87%8D%E4%BD%BF%E7%94%A8-%E7%94%A8%E7%A9%BA%E6%A0%BC%E9%9A%94%E5%BC%80%E5%B0%B1%E5%A5%BD)
- [transition 过渡](#transition-%E8%BF%87%E6%B8%A1)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# transform全解 transition
## 经验技巧
1. 在开发者工具调试时,按住键盘上'↑' '↓'可以调整数字大小,按住ALT就可以调整小数,按住shift可以调更大
四个常用功能
## 1.位移translate
### 位移
```css
.container{
transform:translateX(50px);
/*在x方向移50px*/
}

```
### 指定视点 z轴
需要加一个父元素,指定视点,当translate大就离视点远,小就近.

transform:translate(50px,50px);
transform:translate(x,y);



```css
  #demo:hover{
transform: translateZ(0px);
}
.wrapper{
    perspective: 1000px;
    border: 1px solid red;
}

```
### translate 3d
translate(x,y,z);
translate(50%);向右偏移 身位50%
translate(-50%);向左偏移 身位50%

translate(-50%,-50%);可以做绝对定位的居中

```css
  .wrapper{
       position: relative;
   }
   .center{
       position: absolute;
       left: 50%;
       right: 50%;
       transform: translate(-50%,-50%);
   }
   
```
## 2.缩放scale
```css
.transform:hover{
    transform: scale(2);
    transition:all 1s;
}
```
当鼠标浮上去时,变大两倍
用1s变化,变成动画效果
还有scaleX,scaleY的用法

## 3. 旋转rotate
transform:rotate(45deg);
从12点方向顺时针旋转45°,默认垂直于屏幕轴旋转.
一般360°旋转用于制作loading
## 4. 倾斜 skew
transform:skewX(15deg);
## 5. 多重使用 用空格隔开就好
 transform:scale(1,2) rotate(45deg);
 transform:none;//取消所有

# transition 过渡
主要是用来呈现一个动画的效果
语法：
transition:属性名 时长 过渡方式 延迟
可以用all来代表所有属性，但是display无法过渡