# HTML-base标签详解

> [文档查看](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/base) 



### 属性说明

#### href

文档中说此属性是“用于文档中相对URL地址的基础URL”，不好理解，我们来做几个实验。

#### 实验一

base-href-1.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>base-href实验1：不设置base标签</title>
</head>
<body>
<a href="">这是一个href属性为空的链接</a>
<br>
<a href="http://www.baidu.com">这是一个href属性设为绝对路径(http://www.baidu.com)的链接</a>
<br>
<a href="test.html">这是一个href属性设置为相对路径（test.html）的链接</a>
    </body>
</html>
```

效果如下：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170603/162817095.png)

现在我们来依次点击这三个链接，结果如下：

* 第一个链接点击后当前页面刷新，相当于跳转到了当前页面自身

* 第二个链接点击后 在*当前标签页* 打开了我们所设置的*绝对路径*指向的页面（百度）

* 第三个链接点击后在*当前标签页* 打开了该页面同目录下的test页面，如图：

  ![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170603/163353511.png)

好，请记下这几个结果，我们进行第二个试验：

#### 实验二　

base-href-2.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>base-href实验1：不设置base标签</title>
    <base href="/">
</head>
<body>
<a href="">这是一个href属性为空的链接</a>
<br>
<a href="http://www.baidu.com">这是一个href属性设为绝对路径(http://www.baidu.com)的链接</a>
<br>
<a href="test.html">这是一个href属性设置为相对路径（test.html）的链接</a>
    </body>
</html>		
```



这次我们在上一个页面的基础上，在`<head>` 标签内增加了`<base>`标签，并为其`href` 属性赋值为根路径符号`/` ,现在再点击一下页面上的三个链接，结果如下：

* 第一个链接，点击后跳转到了服务器*根目录* 下
* 第二个链接，点击后依然在当前标签页跳转到了我们指定的绝对路径指向的页面，即百度首页。
* 第三个链接，点击后浏览器在当前标签页跳转到了*根目录* 下的test页面

好的，这下我们明白了，也就是说，**`<base>` 标签的`href`属性，实际上就是为页面中所有的元素的`href`属性设置了基础值（对元素`href`为绝对路径的元素不起作用）**,当这些元素进行跳转时，都会基于当前目录加上这个默认的URL（相对路径的情况下）再加上自己的`href`属性值来跳转。



为了验证我们的想法，我们再做第三个实验和第四个实验：

实验三

base-href-3.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>base-href实验1：不设置base标签</title>
    <base href="localhost/test">
</head>
<body>
<a href="">这是一个href属性为空的链接</a>
<br>
<a href="http://www.baidu.com">这是一个href属性设为绝对路径(http://www.baidu.com)的链接</a>
<br>
<a href="test.html">这是一个href属性设置为相对路径（test.html）的链接</a>
    </body>
</html>
```



这次，我们将`<base>`标签的`href`属性设置为了一个相对路径，再点击下面三个链接，结果如下：

* 第一个链接，点击后跳转到了当前目录下的`localhost/test`,  
* 第二个链接，点击后依然跳转到了绝对路径指向的页面（百度）
* 第三个链接，点击后跳转到了当前目录下的localhost目录下的test.html页面

也许你会好奇，为什么第三个链接不是跳转到localhost目录下的test目录下的test.html呢？

细心如你，肯定会发现，我们在设置`<base>`标签的`href`属性时，设置的是相对路径，而这个相对路径最后没有使用代表目录的符号反斜杠`/`, 所以这里浏览器没有将`localhost/test`中的`test`识别为目录，而是识别为一个文件了，所以它就会默认去寻找该文件同目录下的test.html文件去了。

不信，你可以把`base`标签的`href` 属性设置为`localhost/abc.html`，那么第一个链接将跳转到当前目录下的localhost目录下的abc.html页面, 而第三个链接将跳转到当前目录下的localhost目录下的test.html下。



好了，我们继续第四个试验：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>base-href实验4：base标签href属性为绝对路径</title>
    <base href="http://localhost/test/">
</head>
<body>
<a href="">这是一个href属性为空的链接</a>
<br>
<a href="http://www.baidu.com">这是一个href属性设为绝对路径(http://www.baidu.com)的链接</a>
<br>
<a href="test.html">这是一个href属性设置为相对路径（test.html）的链接</a>
    </body>
</html>	
```



这次我们为`<base>`标签的`href`属性设置了一个绝对路径，再看点击链接的结果：

* 第一个链接，跳转到了我们所设置的`<base>`标签的`href`属性的绝对路径所指向的地址（http://localhost/test/）；
* 第二个链接，依然是在当前页跳转到了其所设置的绝对路径所指向的页面（百度）
* 第三个链接，则跳转到了http://localhost/test/test.html页面



实验三与实验四证明了我们再实验二中所作的总结。现在，对于`<base>`标签的`href`属性，应该有了一个感性的认识的，对于在什么场景下使用它，也一定是心中有数了吧，哈哈！



#### target

根据文档，此属性其实就是规定了页面中新打开窗口的方式的默认值。

我们继续做实验

#### 实验五

base-target-1.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>base-target实验1：为页面增加子窗口（框架）</title>
    <base href="http://localhost/test/">
</head>
<body>
<a href="">这是一个href属性为空的链接</a>
<br>

<a href="http://www.baidu.com">这是一个href属性设为绝对路径(http://www.baidu.com)的链接</a>
<br>
<a href="test.html">这是一个href属性设置为相对路径（test.html）的链接</a>
<br>

<iframe src="./frame.html" width="600" height="400"></iframe>

    </body>
</html>
```

为了验证`target`属性，我们再实验四的页面基础上，又在页面中增加了一个子窗口（框架）`iframe`，此框架中显示与当前页面同级目录下的`frame.html` 页面，

frame.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>框架页面</title>
</head>
<body>
<h3>这是一个框架内的页面</h3>

<a href="">这是一个框架内的链接</a>
</body>
</html>
```



此时，有意思的事情发生了：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170603/173642101.png)

奇怪，为什么呢，我们进入控制台看看：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170603/173854793.png)



当我们把鼠标放置到`iframe`标签上时，此时控制台显示其绝对路径为`http://localhost/test/frame.html`

原来，`iframe`标签的`src`与`a`标签的`href`属性一样，受`<base>`标签的`href`属性影响，所以寻址错误了。

我们修改后继续：

base-target-2.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>base-target实验1：base标签target属性为''-修正iframe的src</title>
    <base href="http://localhost/test/" target="">
</head>
<body>
<a href="">这是一个href属性为空的链接</a>
<br>

<a href="http://www.baidu.com">这是一个href属性设为绝对路径(http://www.baidu.com)的链接</a>
<br>
<a href="test.html">这是一个href属性设置为相对路径（test.html）的链接</a>
<br>

<iframe src="http://localhost:63342/html5css3/high-html/base/frame.html" width="600" height="400"></iframe>

    </body>
</html>

```

此时，页面正常如下：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170603/174547564.png)

现在，当前页面的`<base>`标签的`target`属性值为空，我们来看看点击页面中的三个链接和框架内的一个链接时的结果：

* 点击第一个链接，在 *当前页面*  跳转到了 `http://localhost/test/`这个我们在`<base>`标签的`href`属性中指定的地址；
* 点击第二个链接，在 *当前页面*  跳转到了我们在该元素`href`属性所设置的绝对路径所指向的页面（百度首页）
* 点击第三个链接，在 *当前页面*  跳转到了`http://localhost/test/test.html` 这个地址。
* 点击框架内的链接，框架内页面进行了刷新。

这时，我们发现：**实际上，我们在父页面设置的`<base>`标签的`href`属性并不会影响到框架内的页面**，因为如果影响到的话，应该会和第一个链接一样，跳转到`http://localhost/test/`这个地址去，可实验结果表明并没有。



接下来，我们把当前页面的`<base>`标签的`target`属性的值由空改为`_self`，然后点击页面内的所有链接，发现与为空时的结果相同。



现在，由于target属性的值（`_parent`,`_top`）涉及到子窗口、父窗口、顶级窗口这些概念，我们要改造一下我们的框架页面frame.html:

frame.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>框架页面</title>	
    <base href="http://localhost/frametest/" target="_self">
</head>
<body>
<h3>这是一个框架内的页面</h3>

<a href="">这是一个框架内的链接</a>
<br>
<iframe src="http://localhost:63342/html5css3/high-html/base/subiframe.html" width="500" height="200"></iframe>
</body>
</html>
```



我们做了三件事：

+ 为框架页面添加了`<base>`标签，并为其`target`赋值为`_self`（由上面的实验可知，当值为self与值为空时，其实是等同的。）
+ 为其`<base>`标签的`href`属性设置了值`http://localhost/frametest/`
+ 在该框架页内又嵌套了一个框架页，指向同目录下的`subiframe.html`页面（src地址的设置原因同实验五的第一个说明）,并且同样为它设置了`<base>`标签。

subframe.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>子框架的子框架</title>
    <base href="http://localhost/subframetest/" target="_self">
</head>
<body>
<h3>这是子框架的子框架</h3>
<a href="">这是子框架的子框架里的链接</a>
</body>
</html>
```



现在，然我们看看效果：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170604/085259133.png)

现在，我们接着进行实验：

#### 实验六

我们知道，**`<base>`标签的`target`属性只影响当前页面内链接的打开方式** ，所以接下来我们先实验当前页面里的链接打开方式。



我们将当前页面的`<base>`标签的`target`属性改为`_blank`，再点击当前页面的三个链接，发现链接都在新的标签页打开了。



然后当我们将当前页面的`<base>`的`target`属性分别改为`_parent`和`_top` 时，发现所有链接还是在当前页面打开。其原因是，当前页面本身不是任何页面的子孙页面（窗口），所以它自己的父级和顶级窗口就是它自己。



为了验证以上说法，我们接着进行实验：



现在，我们将frame.html与subframe里的`<base>`的`target`属性的值设置的是`_self`，根据前面的实验我们知道，其等同于设置为空或不设置。



现在分别点击子框架（frame.html）与孙子框架（subframe.html）里的链接，发现都是在其所在的框架窗口内跳转：

点击子框架里的链接结果：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170604/090920428.png)



点击孙子框架内的链接结果：

![mark](http://7xlnr9.com1.z0.glb.clouddn.com/blog/20170604/091004325.png)



> 注：由于子框架与孙子框架内base标签的href属性所设置的路径，服务器上并不存在，所以均显示的是拒绝请求的提示



#### 实验七

现在，我们将frame.html与subframe里的`<base>`的`target`属性的值都设置为`_parent`，然后分别点击这两个框架页面内的链接，结果如下：

* 点击子框架内的链接时，链接在它的父窗口内（也就是当前页面）打开
* 点击孙子框架内的链接时，链接在它的父窗口内（也就是子框架）打开



然后，我们将frame.html与subframe里的`<base>`的`target`属性的值都设置为`_top`，然后分别点击这两个框架页面内的链接，结果如下：

* 点击子框架内的链接时，链接在它的顶级窗口内（也就是当前页面）打开
* 点击孙子框架内的链接时，链接在它的顶级窗口内（也就是当前页面）打开



最后，我们将frame.html与subframe里的`<base>`的`target`属性的值都设置为`_blank，然后分别点击这两个框架页面内的链接，结果如下：

* 点击子框架内的链接时，链接在新标签页内打开
* 点击孙子框架内的链接时，链接在新标签页内打开


至此，我们关于HTML的**<base>** 标签的实验和讲解就全部做完了，对其基本特性和使用场景也有了一个清晰的认识，本节完。



> PS:此属性所有版本浏览器均支持