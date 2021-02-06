# [CSS3伪类和伪元素的特性和区别](https://www.cnblogs.com/ihardcoder/p/5294927.html)

前端er们大都或多或少地接触过CSS伪类和伪元素，比如最常见的`:focus`,`:hover`以及`<a>`标签的`:link`、`visited`等，伪元素较常见的比如`:before`、`:after`等。

其实上面提到的这些伪类和伪元素都是CSS1和CSS2中的概念，CSS1和CSS2中对伪类的伪元素的区别比较模糊，甚至经常有同行将`:before`、`:after`称为伪类。CSS3对这两个概念做了相对较清晰地概念，并且在语法上也很明显的讲二者区别开。

### 伪类 - pseudo classes

首先看看CSS2中对伪类的定义：

> [CSS 伪类用于向某些选择器添加特殊的效果](http://www.w3school.com.cn/css/css_pseudo_classes.asp)。

单单看定义完全不懂在讲什么。截止CSS2，伪类有以下几种（偷个懒，截图引自W3School）：

![img](https://images2015.cnblogs.com/blog/595796/201603/595796-20160319131906271-1237169085.png)

然后是CSS3对伪类的定义：

> The pseudo-class concept is introduced to permit selection based on information that lies outside of the document tree or that cannot be expressed using the other simple selectors.

> A pseudo-class always consists of a "colon" (😃 followed by the name of the pseudo-class and optionally by a value between parentheses.

> Pseudo-classes are allowed in all sequences of simple selectors contained in a selector. Pseudo-classes are allowed anywhere in sequences of simple selectors, after the leading type selector or universal selector (possibly omitted). Pseudo-class names are case-insensitive. Some pseudo-classes are mutually exclusive, while others can be applied simultaneously to the same element. Pseudo-classes may be dynamic, in the sense that an element may acquire or lose a pseudo-class while a user interacts with the document.

简单翻译一下：

> 伪类存在的意义是为了通过选择器找到那些不存在与DOM树中的信息以及不能被常规CSS选择器获取到的信息。

> 伪类由**一个**冒号`:`开头，冒号后面是伪类的名称和包含在圆括号中的可选参数。

> 任何常规选择器可以再任何位置使用伪类。伪类语法不区别大小写。一些伪类的作用会互斥，另外一些伪类可以同时被同一个元素使用。并且，为了满足用户在操作DOM时产生的DOM结构改变，伪类也可以是动态的。

其实第一段话就囊括CSS3伪类的全部定义了，这段话中指出CSS3伪类的功能有两种：

1. 获取不存在与DOM树中的信息。比如`<a>`标签的`:link`、`visited`等，这些信息不存在与DOM树结构中，只能通过CSS选择器来获取；
2. 获取不能被常规CSS选择器获取的信息。比如伪类`:target`，它的作用是匹配文档(页面)的URI中某个标志符的目标元素，例如我们可以通过如下代码来实现页面内的区域跳转：

```html
<ul class="tabs">
	<li><a href="#tab1">标签一</a></li>
	<li><a href="#tab2">标签二</a></li>
	<li><a href="#tab3">标签三</a></li>
</ul>
<div id="tab1" class="tab_content">
<!--tabed content--></div>
<div id="tab2" class="tab_content">
<!--tabed content--></div>
<div id="tab3" class="tab_content">
<!--tabed content--></div>
```

CSS代码如下：

```css
.tab_content {
  height: 800px;
  background: red;
  margin-bottom: 100px;
}
#tab1:target, #tab2:target, #tab3:target {
	background:blue;
}
```

当然，通过JavaScript来获取`window.location.hash`同样可以实现上例中的效果，但这是另外一回事了。总之，**`:target`通过CSS实现了常规CSS无法实现的逻辑**。

其实对比来看，CSS2中对伪类的定义也是合理地，但是它并未指出“某些选择器”是“哪些选择器”，CSS3对伪类的定义就显得明确了很多。

再举个栗子，通过`:nth-child()`伪类可以实现一些很有意思的效果，比如：

```css
table tr:nth-child(2n) td{
   background-color: #ccc;
}
table tr:nth-child(2n+1) td{
   background-color: #fff;
}
table tr:nth-child(2n+1):nth-child(5n) td{
   background-color: #f0f;
}
```

上面的代码将所有偶数行背景色设置为`#ccc`，不能被5整除的奇数行设置背景色`#fff`，能够被5整除的奇数行设置背景色`#f0f`。

如果不使用伪类而是使用JavaScript代码来实现上述的效果，恐怕要复杂很多。

可以总结出`:nth-child()`伪类的效果是将被常规css选择器筛选出的元素按照既定规定进行再次筛选。

CSS3中还引入了许多新的伪类，感兴趣的读者可以参考[这里](http://www.w3.org/TR/2011/REC-css3-selectors-20110929/#pseudo-classes)。

### 伪元素 - Pseudo-elements

CSS2中对伪元素的定义：

> [CSS 伪元素用于向某些选择器设置特殊效果](http://www.w3school.com.cn/css/css_pseudo_elements.asp)。

好吧，跟伪类的定义完全一样有木有（吐槽一下W3School的翻译）。其实人家这样翻译也没有错，本来CSS2对伪类和伪元素的[定义](http://www.w3.org/TR/CSS2/selector.html#pseudo-elements)就是完全一样的：

> CSS introduces the concepts of pseudo-elements and pseudo-classes to permit formatting based on information that lies outside the document tree.

截止CSS2，伪元素有以下几种：

![img](https://images2015.cnblogs.com/blog/595796/201603/595796-20160319132032365-1912300035.png)

然后再看CSS3中伪元素的[定义](http://www.w3.org/TR/2011/REC-css3-selectors-20110929/#pseudo-elements)：

> Pseudo-elements create abstractions about the document tree beyond those specified by the document language. For instance, document languages do not offer mechanisms to access the first letter or first line of an element's content. Pseudo-elements allow authors to refer to this otherwise inaccessible information. Pseudo-elements may also provide authors a way to refer to content that does not exist in the source document (e.g., the ::before and ::after pseudo-elements give access to generated content).

> A pseudo-element is made of two colons (:😃 followed by the name of the pseudo-element.

> This :: notation is introduced by the current document in order to establish a discrimination between pseudo-classes and pseudo-elements. For compatibility with existing style sheets, user agents must also accept the previous one-colon notation for pseudo-elements introduced in CSS levels 1 and 2 (namely, :first-line, :first-letter, :before and :after). This compatibility is not allowed for the new pseudo-elements introduced in this specification.

> Only one pseudo-element may appear per selector, and if present it must appear after the sequence of simple selectors that represents the subjects of the selector.

> Note: A future version of this specification may allow multiple pseudo-elements per selector.

简单翻译一下：

> 伪元素在DOM树中创建了一些抽象元素，这些抽象元素是不存在于文档语言里的（可以理解为html源码）。比如：documen接口不提供访问元素内容的第一个字或者第一行的机制，而伪元素可以使开发者可以提取到这些信息。并且，一些伪元素可以使开发者获取到不存在于源文档中的内容（比如常见的`::before`,`::after`）。

> 伪元素的由**两个冒号**`::`开头，然后是伪元素的名称。

> 使用两个冒号`::`是为了区别伪类和伪元素（CSS2中并没有区别）。当然，考虑到兼容性，CSS2中已存的伪元素仍然可以使用一个冒号`:`的语法，但是CSS3中新增的伪元素必须使用两个冒号`::`。

> 一个选择器只能使用一个伪元素，并且伪元素必须处于选择器语句的最后。

> 注：不排除未来会加入同时使用多个伪元素的机制。

同样，第一段话是伪元素的清晰定义，也是伪元素与伪类最大的区别。简单来说，伪元素创建了一个虚拟容器，这个容器不包含任何DOM元素，但是可以包含内容。另外，开发者还可以为伪元素定制样式。

已`::first-line`为例，它获取了指定元素的第一行内容并且将第一行的内容加入到虚拟容器中。如果通过JavaScript来实现这个逻辑，那么要考虑的因素就太多了，比如制定元素的宽度、字体大小，甚至浮动元素的图文混排等等。当然，这些问题确实是可以用JavaScript来解决的，但是相对于`::first-line`简简单单的几个字，用JavaScript恐怕不止这些吧！

举个综合使用伪类和伪元素的栗子：

```
q:lang(de)::after{
    content: " (German) ";
}
q:lang(en)::after{
    content: " (English) ";
}
q:lang(fr)::after{
    content: " (French) ";
}
q:not(:lang(fr)):not(:lang(de)):not(:lang(en))::after{
    content: " (Unrecognized language) ";
}
```

以上代码通过伪类`"lang`获取不同`lang`属性的节点，并为之设置伪元素`::after`，伪元素的内容是此节点的语言类型。

最后，总结一下伪类与伪元素的特性及其区别：

1. 伪类本质上是为了弥补常规CSS选择器的不足，以便获取到更多信息；
2. 伪元素本质上是创建了一个有内容的虚拟容器；
3. CSS3中伪类和伪元素的语法不同，后者使用双冒号；
4. 可以同时使用多个伪类，而只能同时使用一个伪元素；

> https://www.cnblogs.com/ihardcoder/p/5294927.html