## 什么是 html

-   `HTML` 指的是超文本标记语言 (Hyper Text Markup Language)
-   `HTML` 不是一种编程语言，而是一种标记语言 (markup language)
-   标记语言是一套标记标签 (markup tag)
-   `HTML` 使用标记标签来描述网页

## html 基本结构

-   `html` 标签是由<>包围的关键词。
-   `html` 标签通常成对出现，分为标签开头和标签结尾。
-   有部分标签是没有结束标签的，为单标签，单标签必须使用/结尾。
-   页面所有的内容，都在 `html` 标签中。
-   `html` 标签分为三部分：标签名称，标签内容，标签属性。
-   `html` 标签具有语义化，可通过标签名能够判断出该标签的内容，语义化的作用是网页结构层次更清晰，更容易被搜索引擎收录，更容易让屏幕阅读器读出网页内容。
-   标签的内容是在一对标签内部的内容。
-   标签的内容可以是其他标签。

## 标签属性

-   `class` 属性：用于定义元素的类名
-   `id` 属性：用于指定元素的唯一 `id`
-   `style` 属性：用于指定元素的行内样式，使用该属性后将会覆盖任何全局的样式设定

## 事件属性

-   `window` 事件属性：
    -   `onafterprint` ：文档打印之后运行的脚本
    -   `onbeforeprint` ：文档打印之前运行的脚本
    -   `onload` ：页面加载结束之后触发
    -   `onresize` ：当浏览器窗口被调整大小时触发
    -   `onunload` ：在用户从网页离开时触发（点击跳转，页面重载，关闭浏览器窗口等）
-   `form` 事件
    -   `onblur` ：元素失去焦点时触发
    -   `onchange` ：在元素值被改变时触发
    -   `onfocus` ：当元素获取焦点时触发
    -   `onselect` ：在元素文本被选中后触发
    -   `onsubmit` ：在提交表单时触发
-   `keyboard` 事件
    -   `onkeydown` ：在用户按下按键时触发
    -   `onkeypress` ：在用户敲击按钮时触发
    -   `onkeyup` ：当用户释放按键时触发
-   `mouse` 事件
    -   `onclick` ：鼠标点击时触发
    -   `ondbclick` ：鼠标双击时触发
    -   `onmousedown` ：在元素上按下鼠标按钮时触发
    -   `onmousemove` ：鼠标移入元素时触发
    -   `onmouseout` ：鼠标离开元素时触发
    -   `onmouseover` ：鼠标移入元素时触发
    -   `onmouseup` ：在元素上释放鼠标按钮时触发
-   `media` 事件

## `HTML`标签

## 网页结构

```HTML
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Document</title>
	</head>
	<body>
		<script>
		</script>
	</body>
</html>
```
