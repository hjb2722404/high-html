# html全局属性讲解之——accesskey

> [查看文档](https://www.w3.org/TR/html401/interact/forms.html#h-17.11.2)

accesskey这个属性只有一个作用：**提供对页面元素的快捷访问**。



理论上，由于它是全局属性，所以所有元素都可以设置这个属性，但是，由于很多元素不具有可访问性，所以实际上，只有以下可激活元素设置了该属性才能达到快捷访问的效果：`a`，`area`，`button`，`input` ，`label` ，`textarea`。

至于`accesskey`是如何起作用的，我们来做实验：

html-accessksy.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>HTML-accesskey</title>
</head>
<body>
<FORM action="http://www.baidu.com" method="post">
    <h3>LABAL</h3>
    <P>
        <LABEL for="fuser" accesskey="u">
            User Name
        </LABEL>
        <INPUT type="text" name="user" id="fuser">
    </P>
    <P>
        <LABEL for="fmotion" accesskey="M">
            Motion
        </LABEL>
        <INPUT type="text" name="user" id="fmotion">
    </P>
    <h3>A</h3>
    <P>
        <A href="http://www.baidu.com" target="_blank" accesskey="o">去百度</A>
    </P>
    <h3>textarea</h3>
    <p>
        <textarea name="textarea" id="textarea" accesskey="i" cols="30" rows="10"></textarea>
    </p>
    <h3>Input</h3>
    <p>
        <input type="text" id="input01" placeholder="input01" accesskey="q">
    </p>
    <!--input02实际上法无法通过accesskey获得焦点，因为其快捷键与浏览器自身快捷键冲突-->
    <p>
        <input type="text" id="bbb" placeholder="input02" accesskey="f">
    </p>
    <h3>area</h3>
    <img src="001.jpg" border="0" usemap="#planetmap" alt="Planets" />

    <map name="planetmap" id="planetmap">
        <area shape="circle" coords="180,139,14" href ="1.html" alt="Venus" accesskey="1" />
        <area shape="circle" coords="129,161,10" href ="2.html" alt="Mercury" accesskey="2" />
        <area shape="rect" coords="0,0,110,260" href ="3.html" alt="Sun" accesskey="3"/>
    </map>
    <h3>button</h3>
    <p>
        <button type="reset" accesskey="r">重置</button>
    </p>
</FORM>
</body>
</html>
```



通过这样一个，我们将上面所列可以使用`accesskey`访问的元素都集中于一个页面内，并且为每个元素都设置了`accesskey`属性。



那么，accesskey 是如何起作用的呢？



实际上，比如某个元素设置了`accesskey`属性值为`b`，那么当我们在*windows* 平台下*chrome* 浏览器的组合键`Alt`+`b`时，该元素便会被激活。

注意上句中的斜体字，没错，触发该属性的组合功能键与平台相关，不同操作系统不同浏览器所使用的组合功能键都不一样，如下表：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170605/094942736.png)



表中的`a key`，就代表元素`accesskey的`值，例如上例中的`b`

好，现在我们在`windows`平台的`google chrom`e浏览器中打开我们的实验页面，并依次按下对应的`accesskey`组合键，结果如下：

* 当按下`Alt`+`u`时，`id`为`fuser`的`input`获得了焦点
* 当按下`Alt`+`m`时，`id`为`fmotion`的`input`获得了焦点
* 当按下`Alt`+`o`时，在新标签页打开了百度页面
* 当按下`Al`t+`i`时，`textarea`输入框获得了焦点
* 当按下`Alt`+`q`时，`id`为`input01`的`input`获得了焦点
* 当按下`Alt`+`f`时，弹出了浏览器的功能菜单  //！**请注意这里**
* 当按下`Alt`+`1`时，跳转到了`1.html`
* 当按下`Alt`+`2`时，跳转到了`2.html`
* 当按下`Alt`+`3`时，跳转到了`3.html`
* 当按下`Alt`+`r`时，将所有输入框中的值重置为空

通过以上结果，我们可知以下几点：

+ 1.`accesskey`属性的值为一个按键值，并且不区分大小写（由`label`部分两个`accesskey`的值一个大写，一个为小写，但都可以获得焦点可知）
+ 2.当设置的快捷组合键与浏览器自身快捷键有冲突时，`accesskey`属性不起作用。（如上例`Alt`+`f`）
+ 3.当输入类元素（`label`、`input`、`textarea`）设置了`accesskey`时，按下其`accesskey`组合键将使其获得焦点
+ 4.当链接类元素（`a`、`area`）设置了`accesskey`时，按下其`accesskey`组合键将直接跳转到对应的链接
+ 5.当按钮来元素（`button`）设置了`accesskey`时，按下其`accesskey`组合键相当于对其进行了`click`操作。



#### 总结

HTML全局属性accesskey，虽然可以提供对元素便捷的快速访问功能，但其建设成本有点高，第一是可设置的键值数量有限，第二是当设置了该属性来提供快速访问时，需要将对应的组合按键在显眼的地方提示页面消费者，而由于组合功能键的平台差异性，意味着在进行提示时需要判断平台，代价稍大。

所以该属性应该尽量用在需要用户频繁在鼠标与键盘之间进行切换的表单页面和图像热点区域比较多的页面。