---
title: 关于DOM中的Selection和Range
toc: true
comment: on
donate: true
tags:
 - 浏览器
 - DOM
categories:
 - [博客]
---

### 1. Selection
#### 1.1 Selection是什么？
> Selection 对象表示用户选择的文本范围或插入符号的当前位置。

首先`Selection`是一个`JS Object`，它代表页面中的文本选区，当有选中的文本返回时，代表的是一个或多个选中的文本区域对象；当没有选中时，可能代表的是最后一次点击的位置对象，也可能是个`type`为`none`的`Selection`对象。通过`window.getSelection()`方法可获得`Selection`对象，如下：

![image-20201105170317885](/Users/vison/Documents/visonyh.github.io/source/_posts/DOM编程/关于DOM中的Selection和Range.assets/image-20201105170317885.png)

#### 1.2 Selection对象的属性和方法

**属性：**

- [`anchorNode`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/anchorNode)只读

返回该选区起点所在的节点（[`Node`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)）。

- [`anchorOffset`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/anchorOffset)只读

返回一个数字，其表示的是选区起点在 [`anchorNode`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/anchorNode) 中的位置偏移量。

​		(1). 如果 `anchorNode` 是文本节点，那么返回的就是从该文字节点的第一个字开始，直到被选中的第一个字之间的字数（如果第一个字就被选中，那么偏移量为零）。

​		(2). 如果 `anchorNode` 是一个元素，那么返回的就是在选区第一个节点之前的同级节点总数。(这些节点都是 `anchorNode` 的子节点)

- [`focusNode`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/focusNode)只读

返回该选区终点所在的节点。

- [`focusOffset`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/focusOffset)只读

返回一个数字，其表示的是选区终点在 [`focusNode`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/focusNode) 中的位置偏移量。

​		(1). 如果 `focusNode` 是文本节点，那么选区末尾未被选中的第一个字，在该文字节点中是第几个字（从0开始计），就返回它。                          

​		(2). 如果 `focusNode` 是一个元素，那么返回的就是在选区末尾之后第一个节点之前的同级节点总数。

- [`isCollapsed`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/isCollapsed) 只读

  返回一个布尔值，用于判断选区的起始点和终点是否在同一个位置。

- [`rangeCount`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/rangeCount) 只读

  返回该选区所包含的连续范围的数量。

-------

**方法：**

- [`getRangeAt`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/getRangeAt)

返回选区包含的指定区域（[`Range`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range)）的**引用**。

- [`collapse`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/collapse)

将当前的选区折叠为一个点。

- [`extend`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/extend)

将选区的焦点移动到一个特定的位置。

- [`modify`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/modify)

修改当前的选区。

- [`collapseToStart`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/collapseToStart)

将当前的选区折叠到起始点。

- [`collapseToEnd`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/collapseToEnd)

将当前的选区折叠到最末尾的一个点。

- [`selectAllChildren`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/selectAllChildren)

将某一指定节点的子节点框入选区。

- [`addRange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/addRange)

一个区域（[`Range`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range)）对象将被加入选区。

- [`removeRange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/removeRange)

从选区中移除一个区域。

- [`removeAllRanges`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/removeAllRanges)

将所有的区域都从选区中移除。

- [`deleteFromDocument`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/deleteFromDocument)

从页面中删除选区中的内容。

- [`selectionLanguageChange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/selectionLanguageChange)

当键盘的朝向发生改变后修改指针的Bidi优先级。

- [`toString`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/toString)

返回当前选区的纯文本内容。

- [`containsNode`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/containsNode)

判断某一个 [`Node`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node) 是否为当前选区的一部分。



--------



### Range对象

#### 1. 什么是range对象

> 接口表示一个包含节点与文本节点的一部分的文档片段.

可以用 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 对象的 [`Document.createRange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createRange) 方法创建 Range，也可以用 [`Selection`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection) 对象的 [`getRangeAt`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection/getRangeAt) 方法获取 Range。另外，还可以通过 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 对象的构造函数 [`Range()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/Range) 来得到 Range。



####2. 创建Range方法

- [`document.createRange`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createRange)

```javascript
var range = document.createRange();
range.setStart(startNode, startOffset);
range.setEnd(endNode, endOffset);
```

- 通过`Selection`的`getRangeAt`方法

```javascript
var seleObj = window.getSelection();
var range = selection.getRangeAt(index);
```

- 直接通过Range构造函数

```javascript
var range = new Range();
range.setStart(startNode, startOffset);
range.setEnd(endNode, endOffset);
```



#### 3. Range 属性和方法

**属性：**

- [`Range.collapsed`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/collapsed) 只读

返回一个表示 `Range` 的起始位置和终止位置是否相同的[`布尔值`](https://developer.mozilla.org/zh-CN/docs/Web/API/Boolean)。

- [`Range.commonAncestorContainer`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/commonAncestorContainer) 只读

返回完整包含 `startContainer` 和 `endContainer` 的、最深一级的[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)。

- [`Range.endContainer`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/endContainer) 只读

返回包含 `Range` 终点的[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)。

- [`Range.endOffset`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/endOffset) 只读

返回一个表示 `Range` 终点在 `endContainer` 中的位置的数字。

- [`Range.startContainer`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/startContainer) 只读

返回包含 `Range` 开始的[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)。

- [`Range.startOffset`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/startOffset) 只读

返回一个表示 `Range` 起点在 `startContainer` 中的位置的数字。

-----

**定位方法：**

[`Range.setStart()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/setStart)

设置 `Range` 的起点。

[`Range.setEnd()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/setEnd)

设置 `Range` 的终点。

[`Range.setStartBefore()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/setStartBefore)

以其它[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)为基准，设置 `Range` 的起点。

[`Range.selectNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/selectNode)

使 `Range` 包含某个[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)及其内容。

[`Range.selectNodeContents()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/selectNodeContents)

使 `Range` 包含某个[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)的内容。

[`Range.collapse()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/collapse)

将 `Range` 折叠至其端点（boundary points，起止点，指起点或终点，下同）之一。

----

**编辑方法：**

*通过以下方法，可以从 `Range` 中获得节点，改变 `Range` 的内容。*

- [`Range.cloneContents()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/cloneContents)

  返回一个包含 `Range` 中所有节点的[`文档片段`](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentFragment)。

- [`Range.deleteContents()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/deleteContents)

  从[`文档`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)中移除 `Range` 包含的内容。

- [`Range.extractContents()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/extractContents)

  把 `Range` 的内容从文档树移动到一个[`文档片段`](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentFragment)中。

- [`Range.insertNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/insertNode)

  在 `Range` 的起点处插入一个[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)。

- [`Range.surroundContents()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Range/surroundContents)

  将 `Range` 的内容移动到一个新的[`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)中。