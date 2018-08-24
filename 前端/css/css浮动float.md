# css浮动float
## 浮动的本质

最开始的时候浮动是用来给图片做环绕效果，后来人们发现浮动可以让<span style="color:red">块级元素呈现在同一行</span>，so慢慢的偏离主题人们开始用浮动来布局。

## 浮动的目的

** 让多个块级元素在同一行上显示 **
* 用 display: inline-black 可以实现，但是块级元素之间有空隙( 缺陷 )

```css
        .first,
        .second,
        .third {
            display: inline-block;
            width: 50px;
            height: 50px;
            background-color: red;
        }
```
![](https://user-gold-cdn.xitu.io/2018/8/24/1656b22d41e03696?w=344&h=120&f=jpeg&s=10454)
* 用 float: left ( 完美 )

```css
        .first,
        .second,
        .third {
            float: left;
            width: 50px;
            height: 50px;
            background-color: red;
        }
```
![](https://user-gold-cdn.xitu.io/2018/8/24/1656b239e02fd23e?w=320&h=122&f=jpeg&s=8497)
## 浮动布局核心
用大盒子（ 标准流 ）包裹需要浮动的内部元素（ 浮动流 ）
原理：用标准流大盒子是为了占位,内部小盒子随便怎么浮动都可以
```html
     <div class="head">head</div>
     <div class="main"> <!-- 大盒子包裹 2个需要浮动的元素 -->
        <div class="left">left</div>
        <div class="right">right</div>
      </div>
     <div class="footer">footer</div>
```

```css
        .main{
            background-color: red;
            height: 500px;
        }
        .main .left{
            float: left;
            width: 40%;
            height: 100%;
            background-color: blue;
        }
        .main .right{
            float: left;
            width: 60%;
            height: 100%;
            background-color: blanchedalmond;
        }
```
![](https://user-gold-cdn.xitu.io/2018/8/24/1656b23df1b3d206)


## 注意点
1. 一个父盒子里面的子元素，如果其中一个子元素有浮动，则其他子级都需要浮动，这样才能一行对齐显示。
2. 块级元素和行内元素设置浮动后，均具有行内块元素的特性（可以设置宽高，宽度基于内容计算）

## 清除浮动的本质
由于浮动元素不再占用原文档流的位置，所以它会对后面的元素排版产生影响，为了解决这些问题，此时就需要在该元素中清除浮动。
准确的说，并不是清除浮动，而是<span style="color:red;">清除浮动后造成的影响</span>。

## 何时清除浮动
父级盒子不方便设置高度，高度需要基于子元素的内容来撑开。但是子元素设置浮动后脱离了标准流，不在占位置，撑不开父级盒子的高度造成问题时。

## 清除浮动的方法

1. ** 额外标签法：在浮动盒子的后面添加一个空盒子 **

```css
    /* 父级盒子没有设置高度 */
    .main {
        width: 960px;
    }
    .left,
    .right {
        float: left;
    }
```
```html
    <div class="main">
        <div class="left"></div>
        <div class="right"></div>
        <div style="clear:both"></div> <!-- 添加空div来清除浮动 额外标签法 -->
    </div>
```
2. ** 父级添加overflow方法 触发BFC（会清除浮动） overflow:hidden **

```css
    .main{
        width: 960px;
        background-color: red;
        overflow: hidden; /* 父级盒子设置overflow：hidden 触发 BFC */
    }
    .left,
    .right{
        float: left;
        width: 100%;
        height: 500px;/* 子级元素用自身的高撑开父级元素 */
    }
```
```html
    <div class="main">
        <div class="left"></div>
        <div class="right"></div>
    </div>
```

3.  ** 利用after伪元素（常用） **

```css
    .clearfix:after{      /* 使用一个冒号是为了兼容旧浏览器 */
            content: '.'; /*兼容旧浏览器写法*/
            display: block;
            visibility: hidden;
            height: 0;
            clear: both;
        }
    .clearfix{
        *zoom:1;   /* 兼容ie6 7清除浮动的兼容写法 */
    }
```
```html
     <div class="main clearfix">
        <div class="left"></div>
        <div class="right"></div>
    </div>
```
4. ** 使用 before 和 after 双伪元素清除浮动 （常用） **

```css
    .clearfix:before,
    .clearfix:after {
        content: '';
        display: table  /* 触发BFC BFC可以清除浮动 */
    }
    .clearfix:after{
        clear:both;
    }
    .clearfix{
        *zoom:1;   /* 兼容ie6 7清除浮动的兼容写法 */
    }
```
```html
     <div class="main clearfix">
        <div class="left"></div>
        <div class="right"></div>
    </div>
```

## 总结
* 浮: 加了浮动的元素盒子是浮起来得，漂浮在其他的标准流盒子上面。
* 漏: 加了浮动的盒子，不占位置的，它浮起来了，它原来的位置漏给了标准流的盒子。
* 特: 特别注意首先浮动的盒子需要和标准流的父级搭配使用，其次浮动可以使元素显示模式体现为行内块特性。