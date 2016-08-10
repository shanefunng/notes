# Common Markdown syntax
---
## 标题

# This is an `<h1>` tag
## This is an `<h2>` tag
###### This is an `<h6>` tag

## 强调

*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_

## 列表

**有序列表：**

1. Item 1
2. Item 2
3. Item 3
   * Item 3a
   * Item 3b
   
**无序列表：**

* Item 1
* Item 2
  * Item 2a
  * Item 2b


## 链接
* 自动识别链接：http://github.com - automatic!
* 行内链接：[GitHub](http://github.com) is worldwide site.
* 参考链接：
 [baidu][first reference] is useful search engine in China.	
* 图片链接：![baidu logo](https://www.baidu.com/img/bd_logo1.png)
* 图片参考链接：![baidu logo][second reference]
 [first reference]: www.baidu.com
 [second reference]: https://www.baidu.com/img/bd_logo1.png

## 块引用

>we're lvind the future so
>the present is our past.

## 行内代码

I think you should use an `<addr>` element here instead.

# Github Flavored Markdown Syntax
---
## 语法高亮

* 方式一：

```javascript
function fancyAlert(arg) {
	if(arg) {
		$.facebox({div:'#foo'})
	}
}
```

```java
public class Person {
	private string name;
	private int age;
}
```

* 方式二：（开头空四个空格或者一个tab）

	public void main(String[] args) {}



## 任务列表

- [x] this is a complete item.
- [ ] this is an incomplete item.
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported

## 表格

First Header | Second Header
:--- | ---:
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

## SHA引用:自动转为链接

16c999e8c71134401a78d4d46435517b2271d6ac  
mojombo@16c999e8c71134401a78d4d46435517b2271d6ac  
mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac

## Issue引用：自动转为链接

#1  
mojombo#1  
mojombo/github-flavored-markdown#1

## 引用用户：输入 @usename

## 自动链接

任何URL(如 http://www.baidu.com/) 将会自动转为链接

## 删除线

大哥，~~我错了~~

## Emoji

:blush:

## 补充：(列表后面加两个空格自动换行)

* __生成段落：__段落前面加空行
* __无视markdown语法：__加上反斜杠 `\`  
 Let's rename \*our-new -project\* to \*our-old-project\*

