# css的一点总结「转载」
一、基础
1. 复位
推荐大家使用reset.css
```
* {
box-sizing: border-box;
margin: 0;
padding: 0;
}
```
2. 重置表单样式
移除各个浏览器之间的差异性，然后自定义样式
```
input, button, select, textarea {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  outline: none;
  border: none;
}
```
3. 变量
```

/* 将变量声明到全局 */
:root {
  --theme_color: red
}

/* 使用变量，参数2为当未找到变量--theme_color时所使用的值 */
body {
  color: var(--theme-color, '#000')
}

/* 将变量声明到局部, 只能在elem的子节点中使用*/
.selector {
  --color: black
}

.selector span {
  color: var(--color)
}
```
// 4. 题外话，Javascript如何操作css变量
```
// 操作全局变量
document.documentElement.style.setProperty('--theme_color', 'blue');
```
// 操作局部变量，如果有两个selector，那么现在只设置了第一个的selector，不影响第二个selector的变量
```
document.querySelectorAll(selector)[0].style.setProperty('--color', 'blue');
```
5. 边距盒子
border-box
使盒子的width，height包括内容、边框、内边距，不包括边距，经常遇到宽度100%，但是有padding的时候会溢出
```
.border-box {
  box-sizing: border-box
}
```
6. 计算函数
注意，减号、加号运算符首尾必须要有空格
```
.selector {
  width:
  calc(100% / 3 * 2 - 5px + 10px)
}
```
6. 为body设置行高，不必为其他元素设置，文本元素很容易继承body样式
```
body {
  line-height: 1.5
}
```
7. 使用SVG图标
SVG的好处就不多说了吧
```
.logo {
  background: url('logo.svg')
}
```
8. 字体大小根据不同视口进行调整
auto-size
不用写Javascript了
```
:root {
  font-size: calc(2vw + 1vh)
}

body {
  font-size: 1rem
}
```
9. 禁用鼠标事件、移动端禁止图片长按保存功能
```
/* PC、移动端都禁止点击事件 */
.no-events {
  pointer-events: none
}

/* 移动端禁止长按呼出菜单 */
.no-callout {
  -webkit-touch-callout: none
}
```
10. 移动端禁止用户长按文字选择功能
```
.unselect {
  -webkit-touch-callout:none;
  -webkit-user-select:none;
  -khtml-user-select:none;
  -moz-user-select:none;
  -ms-user-select:none;
  user-select:none
}
```
11. 文字模糊
blur
```
.blur {
  color: transparent;
  text-shadow: 0 0 5px rgba(0, 0, 0, 0.5)
}
```
12. 文字渐变
text-gradient
```
.text-gradient {
  background-image: -webkit-gradient(linear, 0 0, 0 bottom, from(rgb(63, 52, 219)), to(rgb(233, 86, 86)));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent
}
```
13. 背景渐变兼容性写法
```
.gradient {
  background: linear-gradient(to top, rgba(0, 0, 0, .8), rgba(0, 0, 0, 0));
  background: -webkit-linear-gradient(bottom, rgba(0, 0, 0, .8), rgba(0, 0, 0, 0));
  background: -moz-linear-gradient(bottom, rgba(0, 0, 0, .8), rgba(0, 0, 0, 0));
  background: -ms-linear-gradient(bottom, rgba(0, 0, 0, .8), rgba(0, 0, 0, 0));
  background: -o-linear-gradient(bottom, rgba(0, 0, 0, .8), rgba(0, 0, 0, 0));
  background: -webkit-gradient(linear, 0 100%, 0 0, from(rgba(0, 0, 0, .8)), to(rgba(0, 0, 0, 0)))
}
```
14. 为手持设备定制特殊样式
```
<link type="text/css" rel="stylesheet" href="handheldstyle.css" media="handheld">
```
15. 不换行、自动换行、强制换行
不换行一般用再溢出时显示省略号，强制换行一般用在有特殊字符、英文单词的时候
```
p {
  /* 不换行 */
  white-space: nowrap;

  /* 自动换行 */
  word-wrap: break-word;
  word-break: normal;

  /* 强制换行 */
  word-break: break-all;
}
```
16. 超出N行显示省略号
overflow
```
.hide-text-n {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: n;
  overflow: hidden
}
```
17. 移动端顺畅滚动
```
.scroll-touch {
  -webkit-overflow-scrolling: touch
}
```
18. 多张背景图
background
```
body {
  background: url() no-repeat left center / 1rem, url() no-repeat right center / 1rem
}
```
19. Iphone相册标题吸顶
sticky
```
html

<ul class="sticky-list">
  <!-- n个sticky-item -->
  <li class="sticky-item">
    <div class="title">2018年8月1日</div>
    <ul class="photo-list">
      <!-- n个photo-item -->
      <li class="photo-item">
        <img src="timg.jpg">
      </li>
    </ul>
  </li>
</ul>
scss

.sticky-list {
  .sticky-item {
    .title {
      position: -webkit-sticky;
      position: sticky;
      top: 0;
      padding: .5rem;
      background-color: #fff;
    }
  }
  .photo-list {
    display: flex;
    flex-wrap: wrap;
    padding: .5rem;
    padding-bottom: 0;
    .photo-item {
      flex-basis: 19%;
      margin-right: 1%;
      margin-bottom: 1%;
      &:last-child {
        margin-right: 0;
      }
      img {
        display: block;
        width: 100%;
      }
    }
  }
}
```
20. 横竖屏匹配
```
/* 竖屏时样式 */
@media all and (orientation:portrait) {
  body::after {
      content: '竖屏'
    }
}

/* 横屏时样式 */
@media all and (orientation:landscape) {
    body::after {
      content: '横屏'
    }
   
}

```
21. 硬件加速
写transition、animation时，请用transform代替left、top等属性，从而使动画更流畅
```
.cube {
  -webkit-transform: translateZ(0);
  -moz-transform: translateZ(0);
  -ms-transform: translateZ(0);
  -o-transform: translateZ(0);
  transform: translateZ(0)
}
```
22.移动端屏幕旋转时，字体大小不改变
```
html, body, form, p, div, h1, h2, h3, h4, h5, h6 {
 -webkit-text-size-adjust: 100%;
 -ms-text-size-adjust: 100%;
 text-size-adjust: 100%
}
```
23.Animation动画结束时，保持该状态不变
```
animation-fill-mode: forwards;
```
二、伪类、伪元素
1. 当a标签没有文本内容，但有 href 属性的时候，显示它的 href 属性
```
 /* href为标签上的property，可以换成任何一个 */
a[href^='http']:empty::after {
  content: attr(href)
}

 /* 字符串拼接 */
a:empty::after {
  content: "("attr(href)")"
}
```
2. 用户点击反馈
btn-active

item-active

menu-active

.btn:active {
  opacity: .7;
  /* background-color: #f1f1f1 */
}
3. 移动端pointer型元素(a,button或者手动cursor: pointer的元素)点击去除高光
```
* {
  -webkit-tap-highlight-color: transparent
}
```
4. 清除浮动
```
.clearfix::after {
  content: '';
  display: block;
  height: 0;
  visibility: hidden;
  clear: both
}
```
5. 最后一个元素不需要边框、边距等
```
ul > li:not(:last-child) {
  border-bottom: 1px solid #c5b7b7
}
```
6. 基数项、偶数项、倍数分组项
```
/* 基数 */
.selector:nth-child(2n-1) {}

/* 偶数 */
.selector:nth-child(2n) {}

/* 倍数分组项 */
.selector:nth-child(3n+1) {} /* 匹配第1、4、7、10... */
.selector:nth-child(3n+5) {} /* 匹配第5、8、11、14... */
.selector:nth-child(5n-1) {} /* 匹配第4、9、13、17... */

```
5. 逗号分隔列表
between
```
ul > li:not(:last-child)::after {
  content: ','
}
```
6. 表单元素各种状态的设置
focus + placeholder
```
checked

disabled

/* Input、textarea设置placeholder文字的颜色（这里的placeholder是个伪元素，并不是伪类） */
.selector::placeholder {
  color: #666
}

/* 设置表单元素获取焦点时的样式 */
.selector:focus {
  border: 1px solid #ebebeb
}

/* 设置表单元素被禁止时的样式 */
.selector:disabled {
  background-color: #f1f1f1
}

/* 设置checkbox、radio被选中时的样式 */
.selector:checked {
  background-color: #f1f1f1
}
7. 将checkbox改造成switch组件（利用伪类checked状态）
switch
checkbox:checked + ::after伪元素轻松实现

html

<input class='switch-component' type='checkbox'>
css

/* 背景层 */
.switch-component {
  position: relative;
  width: 60px;
  height: 30px;
  background-color: #dadada;
  border-radius: 30px;
  border: none;
  outline: none;
  -webkit-appearance: none;
  transition: all .2s ease;
}

/* 按钮 */
.switch-component::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 50%;
  height: 100%;
  background-color: #fff;
  border-radius: 50%;
  transition: all .2s ease;
}

/* 选中状态时，背景色切换 */
.switch-component:checked {
  background-color: #86c0fa;
 }

/* 选中状态时，按钮的位置移动 */
.switch-component:checked::after {
  left: 50%;
}
```
8. 美化破碎图像
每个浏览器效果都不一样，可以忽略
```
img {
  position: relative;
  display: block;
  width: 100%;
  height: auto;
  font-family: Helvetica, Arial, sans-serif;
  font-weight: 300;
  text-align: center;
  line-height: 2
}

/* 提示语 */
img:before {  
  content: "We're sorry, the image below is broken :(";
  display: block;
  margin-bottom: 10px
}

 /* 显示图片url引用 */
img:after {  
  content: "(url: " attr(src) ")";
  display: block;
  font-size: 12px
}
```
9. 隐藏没有静音、自动播放的影片
```
video[autoplay]:not([muted]) {
  display: none
}
```
10. 首字、首行放大
line

letter
```
/* 首字放大 */
p:first-letter {
  font-size: 2rem
}

/* 首行放大 */
p:first-line {
  font-size: 2rem
}
```
11. a标签伪类设置顺序LVHA
```
a:link {}
a:visited {}
a:hover {}
a:active {}
```
12. 增强用户体验，使用伪元素实现增大点击热区
hover
```
.btn {
  position: relative
}

.btn::befoer{
  content: "";
  position: absolute;
  top: -1rem;
  right: -1rem;
  bottom: -1rem;
  left: -1rem
}
```
13. 伪元素实现换行，替代换行标签
```
.br::after{
  content: "A";
  white-space: pre
}
```
14. 夜间模式
```
此方法是checkbox:checked + ~选择器 + css变量啦，此处的变量为局部变量，非常酷，大家可以自己加一些其他的变量，如文字的颜色

html

<input class='switch-component' type='checkbox'>
<div class="theme-container"></div>
css

body,
html {
  margin: 0;
  padding: 0;
  height: 100%
}

/* 省略switch-component的样式 */

.theme-container {
  --theme_color: #fff; /* 主题色 */
  width: 100%;
  height: 100%;
  background-color: var(--theme_color);
  transition: background-color .2s ease
}

.switch-component:checked + .theme-container {
  --theme_color: #313131 /* 重置变量 */
}
```
15. 感应用户聚焦区域
hot
```
foucs-within表示一个元素获得焦点，或，该元素的后代元素获得焦点。划重点，它或它的后代获得焦点，上图则是.form-wrapper的候代元素input获得了焦点

.form-wrapper:focus-within {
  transition: all .2s ease;
  transform: translateY(-1rem);
  background-color: #f1f1f1;
}
```
16. Tab切换
tab
```
此方法为radio:checked + label + ~选择器，还有:foucs-within、:target方法，不过这两种方法实现起来比较复杂，而且还有一些Bug，本文不示范

html

<!-- 默认选中第一个Tab -->
<div class="container">
  <input class="nav1" id="li1" type="radio" name="nav" checked>
  <input class="nav2" id="li2" type="radio" name="nav">
  <ul class='nav'>
    <li>
      <label for="li1">Tab1</label>
    </li>
    <li>
      <label for="li2">Tab2</label>
    </li>
  </ul>
  <ul class="content">
    <li>Content1</li>
    <li>Content2</li>
  </ul>
</div>
css

input {
  display: none
}

.nav>li {
  display: inline-block
 }

/* tab按钮的默认样式 */
.nav>li>label {
  display: block;
  padding: 1rem 2rem;
  cursor: pointer
}

/* content内容的默认样式 */
.content>li {
  display: none;
  padding: 1rem;
  animation: fade-out .5s cubic-bezier(0.075, 0.82, 0.165, 1)
}

/* tab按钮选中的样式 */
.nav1:checked~.nav li:first-child,
.nav2:checked~.nav li:last-child {
  background-color: #bf8963;
  color: #fff
 }

/* content显示的样式 */
.nav1:checked~.content>li:first-child,
.nav2:checked~.content>li:last-child {
  display: block
}

/* 调皮一下，写个动画 */
@keyframes fade-out {
  from {
    transform: translateX(2rem);
    opacity: 0
  }
  to {
    transform: translateX(0);
    opacity: 1
  }
 }
 ```
17. 当输入框的value的长度不为0时，显示搜索按钮
shown
```
这里用到placeholder-shown伪类，简单来说就是当input标签有了placeholder属性并且内容不为空时，会触发该状态，但是当input标签有了value值之后，就会消除该状态，所以这里也要配合:not选择器

html

<div class="input-line">
  <input type="text" placeholder="请输入关键字进行搜索">
  <button type="button" class="search-btn">搜索</button>
</div>
css

.search-btn {
  opacity: 0;
  transition: all .5s ease-in-out
}

 input:not(:placeholder-shown)~.search-btn {
  opacity: 1
 }
 ```
18. input获取焦点时，上浮效果
input-up
```
input {
  appearance: none;
  outline: none;
  border: none;
  padding: 1rem;
  border-bottom: 1px solid #ebebeb;
  transition: all .2s ease-in-out;
 }

input:focus {
  box-shadow: 0 3px 10px 1px rgba(0, 0, 0, .1);
  transform: translateY(-.5rem)
 }
 ```
19. 菜单栏的弹性伸缩
menu
```
跟夜间模式几乎一样，所以说，只要脑洞够大，什么效果都可以做的出来
html

<div class="index">
  <input type="checkbox" id="btn">
  <label for="btn"></label>
  <div class="menu"></div>
  <div class="content">
    <p>我是内容</p>
  </div>
</div>
css

body,
html {
  height: 100%;
  overflow-x: hidden;
}

.index {
  height: 100%;
}

/* 菜单栏的初始样式 */
.menu {
  position: fixed;
  top: 0;
  left: 0;
  width: 10rem;
  height: 100%;
  background-color: darkgrey;
  transform: translateX(-10rem);
  z-index: 1;
  transition: all .2s ease-in;
}

 /* 内容区的初始样式 */
 .content {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color: cornsilk;
  transform: translateX(0);
  transition: all .3s ease-in;
 }

 input {
  display: none;
}

 /* 切换按钮的初始样式 */
 label {
  position: fixed;
  top: 1rem;
  left: 1rem;
  z-index: 2;
  transition: all .2s ease-in;
}

 /* 切换按钮选中的样式 */
input:checked~label {
  left: 12rem;
}

/* 切换按钮文字的切换样式 */
input:not(:checked)~label::after {
  content: '拉出'
}

input:checked~label::after {
  content: '收起'
}

/* 菜单栏显示的样式 */
input:checked~.menu {
  transform: translateX(0)
}

 /* 内容区显示的样式 */
input:checked~.content {
  transform: translateX(10rem)
 }
 ```
20. 移动端Android设备上去掉语音输入按钮
```
input::-webkit-input-speech-button {
  display: none
}
```
*21.去掉input，type为search时自带的清空按钮
```
.search::-webkit-search-cancel-button {
   display: none 
}
```
三、布局
1. 使用FlexBox摆脱外边距的各种 hack
flexbox
再也不用last-child { margin: 0 }
```
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between
}

ul > li {
  flex-basis: 23%;
  height: 5rem;
  background-color: #f1f1f1;
  margin-bottom: 1rem
}
```
2. 左右滑动
scroll-x
移动端上滑动丝滑要加-webkit-overflow-scrolling: touch
```
.scroll-x {
  display: flex;
  width: auto;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch
}

.scroll-x > .scroll-x-item {
  flex-shrink: 0;
  margin-right: .5rem
}
```
3. 绝对底部
内容高度不够时，元素显示在最底部，内容高度>100%时，元素撑在最底部（常用于Footer），注意这并不是Fixed定位
absolute footer
```
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

html {
  height: 100%
 }

body {
  position: relative;
  min-height: 100%;
  padding: 0;
  padding-bottom: 5rem
}

.footer {
  position: absolute;
  bottom: 0
}
```
不一定要以body为父元素，只要确保父元素的最小高度为100%就行

4. 左边固定，右边自适应
当然还有浮动的方法，这里介绍flexbox
```
.flex {
  display: flex
}

.flex > .left {
  width: 100px
 }

.flex > .right {
  flex: 1
  }
```
5. 子元素高度auto时，使其全屏居中
一般用在dialog、toast...
```
.all-center {
  position: fixed;
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center
}
```
作者：白色风车kai
链接：https://www.imooc.com/article/51405
来源：慕课网
本文原创发布于慕课网 ，转载请注明出处，谢谢合作
