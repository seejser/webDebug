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
