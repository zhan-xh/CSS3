<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [浏览器渲染原理](#%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93%E5%8E%9F%E7%90%86)
  - [浏览器渲染的6个步骤](#%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93%E7%9A%846%E4%B8%AA%E6%AD%A5%E9%AA%A4)
  - [三种不同的渲染(更新)方式](#%E4%B8%89%E7%A7%8D%E4%B8%8D%E5%90%8C%E7%9A%84%E6%B8%B2%E6%9F%93%E6%9B%B4%E6%96%B0%E6%96%B9%E5%BC%8F)
    - [第一种 全走](#%E7%AC%AC%E4%B8%80%E7%A7%8D-%E5%85%A8%E8%B5%B0)
    - [第二种 跳过布局](#%E7%AC%AC%E4%BA%8C%E7%A7%8D-%E8%B7%B3%E8%BF%87%E5%B8%83%E5%B1%80)
    - [第三种 跳过布局与绘制](#%E7%AC%AC%E4%B8%89%E7%A7%8D-%E8%B7%B3%E8%BF%87%E5%B8%83%E5%B1%80%E4%B8%8E%E7%BB%98%E5%88%B6)
- [动画的原理](#%E5%8A%A8%E7%94%BB%E7%9A%84%E5%8E%9F%E7%90%86)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# 浏览器渲染原理
chrome开发者工具可以查看哪些是重新绘制渲染的
步骤：chrome右键“检查”-> 按下esc -> 左上角三个点 -> 点击"Rendering" -> 勾上"paint flashing" 
然后页面重新渲染时绿色就表示重新绘制(repaint)
## 浏览器渲染的6个步骤
1. 创建HTML DOM
2. 创建CSS DOM
3. 合成以上两棵树
4. 布局 Layout
5. 绘制 paint
6. 合成图层 composite
## 三种不同的渲染(更新)方式
有一个网站可以查看各属性重新渲染时到底触发哪种方式
点击跳转[csstriggers](http://csstriggers.com/)
### 第一种 全走
JS/CSS -> style -> Layout -> Paint -> Composite
div.remove 触发当前元素消失，页面重新绘制，其它元素全部relayout
### 第二种 跳过布局
JS/CSS -> Style -> Paint -> Composite
如果改变背景颜色，直接repaint+composite
### 第三种 跳过布局与绘制
JS/CSS -> Style -> Composite
改变transform，只需要composite

# 动画的原理
帧：每个静止的画面
一般播放速度电视时24帧，游戏是30帧
一个小demo
html
```html
<div id="demo"></div>
```
css
```css
   #demo {
            width: 100px;
            height: 100px;
            border: 1px solid red;
            transition: all is linear;
        }

        #demo.end {
            transform: translateX(200px);
        }
```
js
```javascript
    let n = 1
        let id = setTimeout(() => {
            demo.classList.add('end')
        }, 1000);
```