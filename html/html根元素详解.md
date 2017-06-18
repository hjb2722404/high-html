# html根元素详解
> [文档查看](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/html)

html作为HTML页面的根元素，根据文档，其原来有三个属性：`manifest`,`version`,`xmlns` ，由于新的版本更替，前两个已经不用了，我们来讲一下`xmlns`和其他**全局属性** 。

### xmlns

它的作用是指派XML的命名空间。

关于XML的命名空间，这里有详尽的教程：[XML命名空间](http://www.w3school.com.cn/xml/xml_namespaces.asp)

通过该教程，我们明确了以下几点：

* XML的命名空间解决了XML文件中标签命名冲突的问题

* XML命名空间属性被放置在元素的开始标签之中，在我们这里，元素指的就是`<html>`标签

* XML命名空间属性的设置语法为：

  * ```html
    xmlns:namespance-prefix="namespaceURI“
    ```

当然，根据html根元素的文档，我们还得加一条

* 此属性在XHTML文档中为必须要设置的，而在HTML文档中则为可选。

#### 应用场景

比如，在你的html中，你想要自定义一个标签来进行语义化的表示，你就可以使用它。

举例，如果你需要在HTML页面中使用数学运算作为标签名来表明该标签是相应的运算公式，类似下面这样：

```html
<add>3+2</add>
<minus>8-4</minus>
<time>4*5</time>
<div>12/2</div>
```

另外，你还需要使用一个标签来表示时间：

```html
<time>14:23:22</time>
```



那么，现在有两个问题：

* 如何区分HTML中的布局元素`div`与数学公式中代表除法的`div`
* 如何区分代表乘法的`time`与代表时间的`time`

这时，我们可以通过在html中添加xmlns属性的方式来对他们进行区分，代码如下：

```html
<!DOCTYPE html>
<html lang="en" xmlns:math="http://www.w3.org/1999/Math/MathMl" xmlns:date="http://www.w3.org/1999/Math/MathMl">
<head>
    <meta charset="UTF-8">
    <title>HTML-xmlns属性详解</title>
    <style>
        div { width: 200px; height:100px; border: 2px solid red}
    </style>
</head>
<body>

    <div>这是一个普通的div标签</div>
    <h4>下面是代表数学运算的除法公式的标签</h4>
    <math:div>x3/x</math:div>
    <math:time>X*y</math:time>
<h4>下面是代表时间的标签</h4>
<date:time>14:33:33</date:time>
</body>
</html>
```



然后，当其他解析器或代码维护人员看到这些源码时，就可以非常清晰地区分他们不同的内涵。 

