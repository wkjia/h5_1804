# bootstrap
-[bootstrap全局样式](https://v3.bootcss.com/css/)

# 栅格系统

## 阈（yù）值:
阈的意思是界限，故阈值又叫临界值，是指一个效应能够产生的最低值或最高值。此一名词广泛用于各方面，包括建筑学、生物学、飞行、化学、电信、电学、心理学等

## 响应式列重置
即便有上面给出的四组栅格class，你也不免会碰到一些问题，例如，在某些阈值时，某些列可能会出现比别的列高的情况。为了克服这一问题，建议联合使用 .clearfix 和 响应式工具类。
```js
eg:
<div class="row">
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>

  <!-- Add the extra clearfix for only the required viewport -->
  <div class="clearfix visible-xs-block"></div>

  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
</div>
```
除了列在分界点清除响应， 您可能需要 重置偏移, 后推或前拉某个列。请看此栅格实例。
```js
<div class="row">
  <div class="col-sm-5 col-md-6">.col-sm-5 .col-md-6</div>
  <div class="col-sm-5 col-sm-offset-2 col-md-6 col-md-offset-0">.col-sm-5 .col-sm-offset-2 .col-md-6 .col-md-offset-0</div>
</div>

<div class="row">
  <div class="col-sm-6 col-md-5 col-lg-6">.col-sm-6 .col-md-5 .col-lg-6</div>
  <div class="col-sm-6 col-md-5 col-md-offset-2 col-lg-6 col-lg-offset-0">.col-sm-6 .col-md-5 .col-md-offset-2 .col-lg-6 .col-lg-offset-0</div>
</div>
```
## 列偏移

使用 .col-md-offset-* 类可以将列向右侧偏移。这些类实际是通过使用 * 选择器为当前元素增加了左侧的边距（margin）。例如，.col-md-offset-4 类将 .col-md-4 元素向右侧偏移了4个列（column）的宽度。
```js
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 col-md-offset-4">.col-md-4 .col-md-offset-4</div>
</div>
<div class="row">
  <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
  <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
</div>
<div class="row">
  <div class="col-md-6 col-md-offset-3">.col-md-6 .col-md-offset-3</div>
</div>
```
## 嵌套列

为了使用内置的栅格系统将内容再次嵌套，可以通过添加一个新的 .row 元素和一系列 .col-sm-* 元素到已经存在的 .col-sm-* 元素内。被嵌套的行（row）所包含的列（column）的个数不能超过12（其实，没有要求你必须占满12列）。

```js
div class="row">
  <div class="col-sm-9">
    Level 1: .col-sm-9
    <div class="row">
      <div class="col-xs-8 col-sm-6">
        Level 2: .col-xs-8 .col-sm-6
      </div>
      <div class="col-xs-4 col-sm-6">
        Level 2: .col-xs-4 .col-sm-6
      </div>
    </div>
  </div>
</div>
```
## 列排序

```js
<div class="row">
  <div class="col-md-9 col-md-push-3">.col-md-9 .col-md-push-3</div>
  <div class="col-md-3 col-md-pull-9">.col-md-3 .col-md-pull-9</div>
</div>
```
# 排版

## 标题

```
HTML 中的所有标题标签，<h1> 到 <h6> 均可使用。另外，还提供了 .h1 到 .h6 类，为的是给内联（inline）属性的文本赋予标题的样式。
```
## 页面主体

```
Bootstrap 将全局 font-size 设置为 14px，line-height 设置为 1.428。这些属性直接赋予 <body> 元素和所有段落元素。另外，<p> （段落）元素还被设置了等于 1/2 行高（即 10px）的底部外边距（margin）。
```
## 中心内容

```
通过添加 .lead 类可以让段落突出显示。
```
## 被删除的文本
```
对于被删除的文本使用 <del> 标签。
```
```js
<del>This line of text is meant to be treated as deleted text.</del>
```
## 无用文本
```
对于没用的文本使用 <s> 标签。
```
```js
s>This line of text is meant to be treated as no longer accurate.</s>
```
## 插入文本
```
额外插入的文本使用 <ins> 标签。
```
```js
<ins>This line of text is meant to be treated as an addition to the document.</ins>

```
## 带下划线的文本

```
为文本添加下划线，使用 <u> 标签
```
```js
<u>This line of text will render as underlined</u>
```
## 斜体
```
用斜体强调一段文本
```
```js
<em>rendered as italicized text</em>
```
## 对齐
```
通过文本对齐类，可以简单方便的将文字重新对齐。
```
```js
<p class="text-left">Left aligned text.</p>
<p class="text-center">Center aligned text.</p>
<p class="text-right">Right aligned text.</p>
<p class="text-justify">Justified text.</p>
<p class="text-nowrap">No wrap text.</p>
```
## 改变大小写
```
通过这几个类可以改变文本的大小写
```
```js
<p class="text-lowercase">Lowercased text.</p>
<p class="text-uppercase">Uppercased text.</p>
<p class="text-capitalize">Capitalized text.</p>
```
```
lowercased text.

UPPERCASED TEXT.

Capitalized Text.
```
## 引用
```
在你的文档中引用其他来源的内容。
```
### 默认样式的引用
```
将任何 HTML 元素包裹在 <blockquote> 中即可表现为引用样式。对于直接引用，我们建议用 <p> 标签。
```
```js
<blockquote>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
</blockquote>
```
```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.

```
### 多种引用样式
```
对于标准样式的 <blockquote>，可以通过几个简单的变体就能改变风格和内容。

命名来源
添加 <footer> 用于标明引用来源。来源的名称可以包裹进 <cite>标签中。
```
```js
<blockquote>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
  <footer>Someone famous in <cite title="Source Title">Source Title</cite></footer>
</blockquote>

```
```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.

Someone famous in Source Title
```
### 另一种展示风格
```
通过赋予 .blockquote-reverse 类可以让引用呈现内容右对齐的效果。
```
```js
<blockquote class="blockquote-reverse">
  ...
</blockquote>
```
```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.

                                Someone famous in Source Title

