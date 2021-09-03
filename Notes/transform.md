# transform全解 
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
