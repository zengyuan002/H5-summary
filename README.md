# H5-summary
H5移动端知识点总结

一. 使用rem作为单位
```
html { font-size: 100px; }
@media(min-width: 320px) { html { font-size: 100px; } }
@media(min-width: 360px) { html { font-size: 112.5px; } }
@media(min-width: 400px) { html { font-size: 125px; } }
@media(min-width: 640px) { html { font-size: 200px; } }
```
给手机设置100px的字体大小; 对于320px的手机匹配是100px，其他手机都是等比例匹配; 因此设计稿上是多少像素的话，那么转换为rem的时候，rem = 设计稿的像素/100 即可;

二.  禁用a,button,input,optgroup,select,textarea 等标签背景变暗
在移动端使用a标签做按钮的时候或者文字连接的时候，点击按钮会出现一个 "暗色的"背景，比如如下代码：
```
<a href="">button1</a>
<input type="button" value="提交"/>
```
在移动端点击后 会出现"暗色"的背景，这时候我们需要在css加入如下代码即可：
```
a,button,input,optgroup,select,textarea{
    -webkit-tap-highlight-color: rgba(0,0,0,0);
}
```
三. meta基础知识点：
1.页面窗口自动调整到设备宽度，并禁止用户及缩放页面。
```
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0,maximum-scale=1.0, user-scalable=0" />

属性基本含义：

content="width=device-width：

控制 viewport 的大小,device-width 为设备的宽度

initial-scale - 初始的缩放比例

minimum-scale - 允许用户缩放到的最小比例

maximum-scale - 允许用户缩放到的最大比例

user-scalable - 用户是否可以手动缩放
2.忽略将页面中的数字识别为电话号码<meta name="format-detection" content="telephone=no" />

3. 忽略Android平台中对邮箱地址的识别

<meta name="format-detection" content="email=no" />

4. 当网站添加到主屏幕快速启动方式，可隐藏地址栏，仅针对ios的safari

<meta name="apple-mobile-web-app-capable" content="yes" />

5. 将网站添加到主屏幕快速启动方式，仅针对ios的safari顶端状态条的样式

<meta name="apple-mobile-web-app-status-bar-style" content="black" />

<!-- 可选default、black、black-translucent -->

6. 需要在网站的根目录下存放favicon图标，防止404请求(使用fiddler可以监听到)，在页面上需加link如下：

<link rel="shortcut icon" href="/favicon.ico">

因此页面上通用的模板如下：

<!DOCTYPE html>
 <html>
    <head>
        <meta charset="utf-8">
        <meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
        <meta content="yes" name="apple-mobile-web-app-capable">
        <meta content="black" name="apple-mobile-web-app-status-bar-style">
        <meta content="telephone=no" name="format-detection">
        <meta content="email=no" name="format-detection">
        <title>标题</title>
        <link rel="shortcut icon" href="/favicon.ico">
    </head>
    <body>
        这里开始内容
    </body>
</html>
```
四：移动端如何定义字体font-family
```
body{font-family: "Helvetica Neue", Helvetica, sans-serif;}
```
五：在android或者IOS下 拨打电话代码如下：
```
<a href="tel:15602512356">打电话给:15602512356</a>
```
六：发短信(winphone系统无效)
```
<a href="sms:10010">发短信给: 10010</a>
```
七：调用手机系统自带的邮件功能
```
1. 当浏览者点击这个链接时，浏览器会自动调用默认的客户端电子邮件程序，并在收件人框中自动填上收件人的地址下面

<p><a href="mailto:tugenhua@126.com">发电子邮件</a></p>

2、填写抄送地址;

在IOS手机下：在收件人地址后用?cc=开头;

如下代码：

<p><a href="mailto:tugenhua@126.com?cc=879083421@qq.com">填写抄送地址</a></p>

在android手机下，如下代码：<p><a href="mailto:tugenhua@126.com?879083421@qq.com">填写抄送地址</a></p>

3. 填上密件抄送地址，如下代码：

在IOS手机下：紧跟着抄送地址之后，写上&bcc=，填上密件抄送地址

<a href="mailto:tugenhua@126.com?cc=879083421@qq.com&bcc=aa@qq.com">填上密件抄送地址</a>

在安卓下;如下代码：

<p><a href="mailto:tugenhua@126.com?879083421@qq.com?aa@qq.com">填上密件抄送地址</a></p>

4. 包含多个收件人、抄送、密件抄送人，用分号隔(;)开多个收件人的地址即可实现。如下代码：

<p><a href="mailto:tugenhua@126.com;879083421@qq.com;aa@qq.com">包含多个收件人、抄送、密件抄送人，用分号隔(;)开多个收件人的地址即可实现</a></p>

5、包含主题，用?subject=可以填上主题。如下代码：

<p><a href="mailto:tugenhua@126.com?subject=【邀请函】">包含主题，可以填上主题</a></p>

6、包含内容，用?body=可以填上内容(需要换行的话，使用%0A给文本换行)；代码如下：

<p><a href="mailto:tugenhua@126.com?body=我来测试下">包含内容，用?body=可以填上内容</a></p>

7. 内容包含链接，含http(s)://等的文本自动转化为链接。如下代码：

<p><a href="mailto:tugenhua@126.com?body=http://www.baidu.com">内容包含链接，含http(s)://等的文本自动转化为链接</a></p>
```
八：webkit表单输入框placeholder的颜色值改变：
如果想要默认的颜色显示红色，代码如下：
```
input::-webkit-input-placeholder{color:red;}

如果想要用户点击变为蓝色，代码如下：

input:focus::-webkit-input-placeholder{color:blue;}
```
九：移动端IOS手机下清除输入框内阴影，代码如下
```
input,textarea {

-webkit-appearance: none;

}
```
十：在IOS中 禁止长按链接与图片弹出菜单
```
a, img {

-webkit-touch-callout: none;

}
```

```

calc基本用法

calc基本语法：

.class {width: calc(expression);}

它可以支持加，减，乘，除; 在我们做手机端的时候非常有用的一个知识点;

优点如下：

1. 支持使用 "+","-","*" 和 "/" 四则运算。

2. 可以混合使用百分比(%),px,em,rem等作为单位可进行计算。

浏览器的兼容性有如下：

IE9+，FF4.0+，Chrome19+，Safari6+

如下测试代码：

<div class="calc">我是测试calc</div>

.calc{
    margin-left:50px;
    padding-left:2rem;
    width:calc(100%-50px-2rem);
    height:10rem;
}
```
