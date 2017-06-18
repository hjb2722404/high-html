# 重新认识HTML系列004——全局属性contenteditable

> [查看文档](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes#contenteditable)

### 属性说明

从文档中，我们可以提取到以下关键信息：

* 它表示该element是否可以被编辑
* 默认值会继承父元素的
* 它有两个值：
  * true表示该元素可编辑
  * false表示该元素不可编辑
* 这是一个可枚举属性
* 它不是一个布尔属性



接下来我们做个实验

实验一：

html-contenteditable.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>contenteditable实验</title>
    <script type="text/javascript">
        function showTip() {
            alert('hello,按钮被点击了');
        }
    </script>
</head>
<body>

<h3 contenteditable="true">这是可编辑的h3</h3>
<h3 contenteditable="false">这是不可编辑的h3</h3>

<p contenteditable="true">这里是可编辑的p</p>
<p contenteditable="false">这里是不可编辑的p</p>

<a href="" contenteditable="true">我是可编辑的链接</a><br>
<a href="" contenteditable="false">我是不可编辑的链接</a><br>

<p contenteditable="true">可编辑的图片，实际上不可编辑</p>
<img src="./001.jpg" contenteditable="true" alt="可编辑的图片" title="可编辑的图片" width="300">
<br>
<p contenteditable="false">不可编辑的图片：</p>
<img src="./001.jpg" contenteditable="false" alt="不可编辑的图片" title="不可编辑的图片" width="300">
<br>

<input type="text" contenteditable="true" placeholder="这是一个可编辑的input"><br>
<input type="text" contenteditable="false" style="width: 400px;" placeholder="这是一个不可编辑的input,但实际上它是可编辑的">


<br>
<textarea name="info" id="info" contenteditable="true" cols="30" rows="10">可编辑</textarea>

<textarea name="info" id="info" contenteditable="false" cols="30" rows="10">不可编辑，实际上可编辑</textarea>

<blockquote contenteditable="true">这里是可编辑的引用</blockquote>
<blockquote contenteditable="false">这里是不可编辑的引用</blockquote>
可编辑的选择控件，实际上不可编辑
<select contenteditable="true" style="width: 200px;">
    <option value="1" contenteditable="true">1</option>
    <option value="3">2</option>
    <option value="3">3</option>
</select>
<br>
可编辑的进入条，实际上不可编辑
<progress value="50" min="0" max="100" contenteditable="true"></progress>
<br>

可编辑的按钮
<button contenteditable="true" onclick="showTip()">可编辑按钮</button><br>
不可编辑的按钮
<button contenteditable="false" onclick="showTip()">不可编辑按钮</button>


<br>
可编辑的表格
<table contenteditable="true" border="1">
    <tr>
        <td contenteditable="false">不可编辑的单元格</td>
        <td>继承父元素，可编辑</td>
    </tr>
    <tr contenteditable="false">
        <td>继承父元素，不可编辑</td>
        <td contenteditable="true">可编辑的单元格</td>
    </tr>
</table>



<div id="div1" contenteditable="true">
    <h3> 我是div1中的h3</h3>
    <p>我是div1中的p,<a href="">我是p中的链接</a></p>
</div>

</body>
</html>
```



我们在这个实验中为大多数我们常用的标签分别设置了contenteditable属性为true和false，感兴趣的可以粘贴代码然后亲自看看效果，我们这里直说结论：

* contenteditable属性只对页面中的默认不可编辑都文本有意义
* 表单元素不受contenteditable属性影响，即：本来便可获取输入的元素（input/textarea等）,无论contenteditable设为true还是false，其总是可编辑的。如select/option/progress等表单元素，根本不受影响，即使设置了contenteditable属性为true，其文本部分也不可编辑。
* contenteditabel属性可继承，如table的例子，但是子元素可以通过设置不同的值来单独设置可编辑性。
* 图片、链接等元素设置contenteditable属性会有影响，但没有实际意义。



### 使用场景

说了这么多，这个属性在实际应用中，到底应用在哪些场景下呢？

下面是我能想到的两种场景：

#### 场景一：模板效果预览

在平时的开发中，会有一些现成的网页模板可供选择，类似下面这样的：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170616/093552831.png)

像这类英文的模板，由于中文字体与英文字体不同，有时我们实际的文本长度与模板示例中的长度也可能不一样，如果我们想快速看看应用为中文网站时最终的文字呈现效果是怎样的，那么直接在页面上编辑当然是最方便的了。

我们只需要将<body>标签加上contenteditable属性设为true，就可以直接在页面上将示例文本修改为我们最终想要呈现的文本，来预览效果。如下：

```html
<body contenteditable="true">
```



此时，我们就可以在模板页面中自由编辑内容，而不必改代码中的示例文本了：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170616/094552054.png)



#### 场景二 无表单提交修改



第二种场景类似我们修改QQ签名，这时候我们只需要提交一条输入，如果使用表单<form>、<input>元素来提交的话，会有点杀鸡用牛刀的感觉，此时我们就可以将这条可被修改的内容所在元素的contenteditable属性设置为true，然后使用js来监听此元素的改变，然后实时将用户编辑后的内容提交给服务器保存，岂不方便很多。

这个我就不写例子了，有兴趣的可以自己试试、。

