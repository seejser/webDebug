## input 在IOS下大于父元素或者超出父元素的大小
手机页面遇到一个横竖屏切换时出现的问题。为满足不同分辨率下正常显示，页面的input元素宽度需要撑满整个父级元素，而父级元素则是占满整行的，由于input元素有padding间距，所以使用box-sizing来保持宽度不超出父元素，代码如下：
```
<inputtype="text"class="text_input w_100"name="phone"id="phone"/>
.text_input {
box-sizing: border-box;
padding:.8em;
border:1px solid #E2E2E3;
background:#FFF;
font: normal 16px/1'SimHei';
border-radius:3px;
outline: none;
}
.w_100 {
width:100%;
}
```
input元素有padding间距，所以使用box-sizing来保持宽度不超出父元素
