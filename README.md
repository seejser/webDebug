# webDebug
1.Iphone移动Web和safari下输入文本无法显示或者显示看不到的问题
代码如下：
```
<div class="phone">
<input type="number" value="" placeholder="请输入验证码" >
</div>

```
上述代码在Android下显示正常，用iphone查看时输入文本框发现输入的文字都空白，加入背景上仍然看不到文字。
debug:在文本框input加样式：
```
style="line-height:normal;"
```
2.android click事件不起作用
代码：
```
   $(".spirit_info").click( {
        console.log('spirit_info')

    });
```
dubug:
```
   $(".spirit_info").on('click',function () {
        console.log('spirit_info')

    });
```
3.安卓input 输入留白，遮盖住input部分
HTML5在开发时，经常遇到各种问题，留白遮罩就是一种常见的问题。
产生的原因是：在安卓下，当软键盘输入弹起时，软键盘部分会自动出现遮盖，产生的原因是父级元素绝对定位：
```
 width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background: url("../images/commbg.jpg")no-repeat;
    background-size: 100% 100%;
  
```
解决方案：
```
 width: 100%;
    height: 100%;
    position: absolute;
    /* left: 0;*/
    /* right: 0;*/
    top: 0;
    bottom: 0;
    /*    background-image:url("../images/commbg.jpg");
        background-repeat:repeat-y;*/
    background: url("../images/commbg.jpg")repeat;
    background-size: 100% 100%;
    overflow-y: scroll;
```
这样，同时也解决了子元素撑开父元素的问了，自然撑开的滚动

4.微信下html页面，键盘弹出，页面变形

总结一下安卓下面解决input键盘弹出导致页面压缩变形的方法：
1）.不对input使用绝对定位，使用绝对定位会脱离文档流导致在安卓上被压缩变形。
2）.
写个监听resize事件
```
var HEIGHT = $('body').height();
        $(window).resize(function() {
            $('.main').height(HEIGHT);
        });
```
当键盘弹出的时候，重置为原来的高度

3）.最外层容器用js设置为屏幕宽高，这样键盘弹出也没事,Height不能写成百分比，得写成固定数值，通过js获取当前设备的height.


5.解决安卓端微信页面长按时出现浏览器选择打开问题

```
document.oncontextmenu=function(e){  
    //或者return false;  
    e.preventDefault();  
}; 
```

IOS 下的类似问题解决：

```
-webkit-user-select: none;
```

6.swiper 组件bug

当swiper-container 或者其父元素隐藏后被重启时，swiper loop出现空白

```

var mySwiper = new Swiper('.swiper-container',{
    pagination: {
      el: '.swiper-pagination',
    },
    observer:true,/*启动动态检查器，当改变swiper的样式（例如隐藏/显示）或者修改swiper的子元素时，自动初始化swiper。*/
    observeParents:true,/*将observe应用于Swiper的父元素。当Swiper的父元素变化时，例如window.resize，Swiper更新。*/
  })
```


7.webstrom



https://licensez.com/
