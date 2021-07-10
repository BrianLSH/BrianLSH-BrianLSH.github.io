---
title: CSS基础
toc: true
tags: CSS基础 选择器
date: 2015-04-02
categories:
  - [CSS, 基础]
---

```css
css选择器总结:

基本选择器: 就是我们说的标签 
属性选择器: [] 不限于class id
id选择器: #id
类选择器: .
交集选择器: 两个选择器构成，其中第一个为标签选择器，第二个为class选择器 p.class名
并集选择器: 各种选择器组合 逗号隔开 多个选择器应用同一样式
后代选择器: 上下文选择  层次间隔无限 选取后面所有
子代选择器: > 标识, 只会选择子元素, 不包含孙子元素等
相邻兄弟选择器: +号标识 必须兄弟相邻元素 排除第一个 循环查找
兄弟选择器: ~号标识 必须兄弟元素 排除第一个 循环查找


```
### CSS 行内元素和块元素

#### H1-H5 标题，ul li,ol li,table,form,dl, div, from, menu, p,pre

#### a, span, img, input,i,strike,strong,sub,textarea

### CSS 有哪些引入方式

#### 行内式

#### 内联式

#### 外链式

#### 导入式

#### 内联式外链式导入的区别
```css
  加载顺序
      link引入的css在加载页面时同时加载，而@import中的css要在页面加载完毕后加载
  从属关系
      link是HTML提供的标签
      @import是css的语法规则，只能加载在style标签内和css文件中
  兼容性
     @import是css2.1时提出的，只能用于IE5+，而link不受兼容影响
     DOM可控性
  link支持js控制DOM改变样式，而@import不支持
      @import 的用法
      @import必须写在样式顶部，即import规则一定要先于除了@charset的其他任何CSS规则 ———MDN
  引入位置
      在html中 <style>@import url(引入的css路径);/*这个必须要写在style的第一行*/</style>
     在css中 @import url(引入的css路径); @import "引入的css路径"; /*这个@import必须要写在CSS的第一行*/
  不推荐使用@import
      影响浏览器的并行下载
      多个@import的使用会使浏览器下载顺序紊乱
```

### 3.CSS 选择器有哪些

#### 基本选择器

```css
最常见的
  CSS
  选择器是元素选择器。换句话说，文档的元素就是最基本的选择器。
  如果设置
  HTML
  的样式，选择器通常将是某个
  HTML
  元素，比如
  p、h1、em、a，甚至可以是
  html
  本身
  html {
  color: black;
}
h1 {
  color: blue;
}
h2 {
  color: silver;
}
```

#### 属性选择器

```css
可以为拥有指定属性的 HTML 元素设置样式，而不仅限于 class 和 id 属性。

注释：只有在规定了 !DOCTYPE 时，IE7 和 IE8 才支持属性选择器。在 IE6
及更低的版本中，不支持属性选择
[attribute]	用于选取带有指定属性的元素。
[attribute=value]	用于选取带有指定属性和值的元素。
[attribute~=value]	用于选取属性值中包含指定词汇的元素。
[attribute|=value]	用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。
[attribute^=value]	匹配属性值以指定值开头的每个元素。
[attribute$=value]	匹配属性值以指定值结尾的每个元素。
[attribute*=value]	匹配属性值中包含指定值的每个元素。

<style >
    [title]{
    color:red;
    }
</style>

<button title="登录" >登录</button>
<button>登录</button>

```

#### id 选择器

```css
标识 #号

*#intro {font-weight:bold;}

<p id="intro">This is a paragraph of introduction.</p>
```

#### 类选择器

```css
在 CSS 中，类选择器以一个点号显示：

<h1 class="important">
This heading is very important.
</h1>

<p class="important">
This paragraph is very important.
</p>

*.important {color:red;} 或者 .important {color:red;}

类选择器可以结合元素选择器来使用,希望只有段落显示为红色文本
p.important {color:red;}
希望为 h1 元素指定不同的样式，可以使用选择器 h1.important



CSS 多类选择器

<p class="important warning">
This paragraph is a very important warning.
</p>

.important {font-weight:bold;}
.warning {font-style:italic;}
.important.warning {background:silver;}

如果一个多类选择器包含类名列表中没有的一个类名，匹配就会失败。请看下面的规则：
.important.urgent {background:silver;} 匹配失败,这个选择器将只匹配 class
属性中包含词 important 和 urgent 的 p 元素。因此，如果一个 p 元素的 class
属性中只有词 important 和 warning，将不能匹配。不过，它能匹配以下元素：

<p class="important urgent warning">
This paragraph is a very important and urgent warning.
</p>
```

#### 交集选择器

```css
要点: 两个选择器构成，其中第一个为标签选择器，第二个为class选择器 p.class名
/*交集选择器*/
/*既是P标签，类名称又会text的元素字体变为红色*/
p.text{
    color: red;
}

 /*交集选择器-多个选择器包含的元素*/
<p>好好学习1</p>
    <p class="text">好好学习2</p>
    <p class="text">好好学习3</p>
    <p>好好学习4</p>
```

#### 并集选择器

```css
CSS并集选择器也叫群选择器，是由多个选择器通过逗号连接在一起的，
这些选择器分别是：标签选择器、类选择器或id选择器等。

在声明各种CSS选择器时，如果某些选择器的风格完全相同，或者
部分相同，便可以利用并集选择器同时声明这些风格相同的CSS选择器。

并集选择器允许同时给多个选择器应用同一种样式,如

h1,h2,p,.color,#one{
  color:blue;
  font-size:14px;
}

要点: 逗号隔开的多个(多种)选择器 应用同一种样式

 /*并集选择器*/
/*让container下的所有元素内容为蓝色*/
#container p,span,em,strong{
    color: blue;
}

/*并集选择器-多个选择 所有匹配的元素*/
<div id="container">
    <p>好好学习1</p>
    <span>好好学习2</span><br>
    <em>好好学习3</em><br>
    <strong>好好学习4</strong>
</div>
```

#### 后代选择器

```css
有关后代选择器有一个易被忽视的方面，即两个元素之间的层次间隔可以是无限的
根据上下文选择元素,一般定义不超过三级(便于阅读)

要点： 上下文选择  层次间隔无限 选取后面所有
h1 em {color:red;}
 h1.ts1 em {color:red;}

 <h1 class='ts1'>
      <em>em1</em> 
      <p>
        <em>em2</em>
      </p> 
    </h1>
em1 和 em2 都会被渲染
```

#### 子代选择器

```css
要点: > 标识, 只会选择子元素, 不包含孙子元素等

与后代选择器相比，子元素选择器只能选择作为某元素子元素的元素。
      <style>
            h1 > strong {
              color: red;
            }
      </style>

这个规则会把第一个 h1 下面的两个 strong 元素变为红色，但是第二个 h1 中的 strong 不受影响：

    <h1>This is <strong>very</strong> <strong>very</strong> important.</h1>
    <h1>
      This is <em>really <strong>very</strong></em> important.
    </h1>
或者
<h1>
   <strong>h1.very1</strong>
   <strong>h1.very2</strong>
    <p>
      <strong>p.very</strong>
    </p>
  </h1>

  只会渲染 very1 very2

    结合后代选择器和子选择器, 请看下面这个选择器：
    table.company td > p
    上面的选择器会选择作为 td 元素子元素的所有 p 元素，这个 td 元素本身从 table 元素继承，
    该 table 元素有一个包含 company 的 class 属性。
```

#### 兄弟、相邻兄弟选择器

```css
相邻兄弟选择器

‘+’选择器则表示某元素后相邻的兄弟元素，也就是紧挨着的，是单个的。
但是也会循环查找，即当两个兄弟元素相同时，会再一次循环查找

关键字 +号标识 必须兄弟相邻元素 排除第一个 循环查找

          例子一:
          p+p::before {
                  color:red;
                  content: '123';
                  display:block;
                }
          <p>p1</p>
          <p>p2</p>
          <h1>hello</h1>
          <p>p4</p>
          <p>p5</p>
          <p>p6</p>
          <p>p7</p>
          <p>p8</p>
          此时只有p2 以及p5 p6 p7 p8 有作用, 从p4 开始把p4当做第一个元素重新查找

          例子二:

            li+li::before {
                    margin: 0px 10px;
                    content: '|';
                }

          导航栏中间加一个竖杠


兄弟选择器
而‘~’选择器则表示某元素后所有同级的指定元素，强调所有的
要点  ~号标识 必须兄弟元素 排除第一个 循环查找

例子一:
          p ~ p::before {
                  color:red;
                  content: '123';
                  display:block;
                }
          <p>p1</p>
          <p>p2</p>
          <h1>hello</h1>
          <p>p4</p>
          <p>p5</p>
          <p>p6</p>
          <p>p7</p>
          <p>p8</p>
          此时除了p1 其他都会出现红色123
```

#### 伪类选择器

```css

伪类可以与 CSS 类配合使用：
a.red:visited {color:#FF0000;}

<a class="red" href="css-syntax.html">CSS 语法</a>

CSS伪类选择器：

a:link 没有访问之前a标签的样式

a:visited 已访问a标签的样式

a:hover a标签鼠标移上的样式

a:actived a标签鼠标按下的样式

input:focus input表单元素获取焦点

input:blur input表单元素失去焦点

CSS3新增的伪类选择器：

:checked 被选中 主要用在input表单元素上

:not 排除

:last-child 最后一个元素

:nth-child(n)  n表示具体的第几个  odd/2n+1 奇数 even/2n 偶数

:only-child 仅仅/唯一的元素

:nth-last-child(n) 倒数第几个元素  :nth-last-child(1) <=> :last-child

:first-of-type 第一个同级兄弟元素

:last-of-type 最后一个同级兄弟元素

:only-of-type 只有一个同级兄弟元素

:nth-of-type(n) 第几个同级兄弟元素

:nth-last-of-type(n) 倒数第几个同级兄弟元素

:empty 空内容
```

#### 伪元素选择器

```css
伪元素就是假象的元素，并不存在DOM树中，无法捕获，也无法绑定事件


::after是CSS3中伪元素写法，区别于CSS2中:的伪类写法，
:after是css2写法，::after是css3写法。用于向渲染的元素后添加内容，
这些添加不会出现在DOM中，仅在css渲染层加入

记住:只要碰到伪元素before after,content一定要加.
只要宽度不起作用，就加display:block/inline-block 转换为块或者行内块

:first-line:为某个元素的第一行文字使用样式；
:first-letter:为某个元素中的文字的首字母或第一个字使用样式；
:before:在某个元素之前插入一些内容；content不能省 没有设置为空
:after: 在某个元素之后插入一些内容；content不能省 没有设置为空

```

#### 派生选择器

```css
要点： 上下文关系定义样式

通过依据元素在其位置的上下文关系来定义样式，你可以使标记更加简洁。
li strong {
    font-style: italic;
    font-weight: normal;
  }

<p><strong>我是粗体字，不是斜体字，因为我不在列表当中，所以这个规则对我不起作用</strong></p>

<ol>
<li><strong>我是斜体字。这是因为 strong 元素位于 li 元素内。</strong></li>
<li>我是正常的字体。</li>
</ol>
在上面的例子中，只有 li 元素中的 strong 元素的样式为斜体字，无需为 strong
元素定义特别的 class 或 id，代码更加简洁。

strong {
     color: red;
     }

h2 {
     color: red;
     }

h2 strong {
     color: blue;
     }

<p>The strongly emphasized word in this paragraph is<strong>red</strong>.</p>
<h2>This subhead is also red.</h2>
<h2>The strongly emphasized word in this subhead is<strong>blue</strong>.</h2>
```
