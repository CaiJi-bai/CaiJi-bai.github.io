---
layout: mypost
title: Markdown Test
categories: [Test]
---

# 标题

# 这里是 h1

## 这里是 h2

### 这里是 h3

#### 这里是 h4

##### 这里是 h5

###### 这里是 h6

```
# 这里是 h1
## 这里是 h2
### 这里是 h3
#### 这里是 h4
##### 这里是 h5
###### 这里是 h6
```

## 段落

段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落一段落

段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落二段落

## 超链接

[TMaize Blog](http://blog.tmaize.net)

```
[TMaize Blog](http://blog.tmaize.net)
```

## 引用

> 这里是引用

```
> 这里是引用
```

## 常见字体样式

_斜体_

**粗体**

~~删除线~~

```
_斜体_
**粗体**
~~删除线~~
```

## 列表

- 无序列表 1-1

  缩进 2 空格

  - 缩进 2 空格
  - 缩进 2 空格

- 无序列表 1-2
- 无序列表 1-3

1. 有序列表 1-1

   缩进 3 空格

   1. 缩进 3 空格
   2. 缩进 3 空格

2. 有序列表 1-2
3. 有序列表 1-3

```
- 无序列表 1-1

  缩进 2 空格

  - 缩进 2 空格
  - 缩进 2 空格

- 无序列表 1-2
- 无序列表 1-3

1. 有序列表 1-1

   缩进 3 空格

   1. 缩进 3 空格
   2. 缩进 3 空格

2. 有序列表 1-2
3. 有序列表 1-3
```

## 分割线

---

```
---
```

## 图片

破事水![line](emoji_01.png)
滑稽![line](emoji_02.png)

```md
![line](http://xx.com/xx.jpg)
```

块级别图片

```md
![测试图片](001.jpg)
```

![测试图片](001.jpg)

## 代码行

这是一段文字`rm -rf /*`这是一段文字

```
这是一段文字`rm -rf /*`这是一段文字
```

## 代码块

```javascript
blog.encodeHtml = function(html) {
  var o = document.createElement('div')
  o.innerText = html
  var temp = o.innerHTML
  o = null
  return temp
}
```

````
```javascript
blog.encodeHtml = function(html) {
var o = document.createElement('div')
o.innerText = html
var temp = o.innerHTML
o = null
return temp
}
```
````

## 表格测试

| Tables        |      Are      |   Cool |
| ------------- | :-----------: | -----: |
| col 3 is      | right-aligned | \$1600 |
| col 2 is      |   centered    |   \$12 |
| zebra stripes |   are neat    |    \$1 |

```md
| Tables        |      Are      |   Cool |
| ------------- | :-----------: | -----: |
| col 3 is      | right-aligned | \$1600 |
| col 2 is      |   centered    |   \$12 |
| zebra stripes |   are neat    |    \$1 |
```