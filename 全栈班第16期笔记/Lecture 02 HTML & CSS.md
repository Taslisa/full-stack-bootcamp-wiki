# Lecture 02 HTML & CSS

## 主要知识点
  - [Lecture 02  HTML&CSS](#lecture-02-html&css)
    - [2.1 HTML Introduction](#21-html-introduction)
    	- [2.1.1 HTML基本结构](#211-html基本结构)
    	- [2.1.2 live-server](#212-live-server)
    	- [2.1.3 ```<h1>```](#213-h1)
    	- [2.1.4```<p>```](#214-p)
    	- [2.1.5 ```<strong>```和```<em>```](#215-strong和em)
    	- [2.1.6 ```<ol>```和```<ul>```](#216-ol和ul)
    	- [2.1.7```<img>```](#217-img)
    	- [2.1.8```<a>```](#218-a)
    	- [2.1.9 HTML语义化](#219-html-语义化)
    - [2.2 CSS](#22-css)
    	- [2.2.1 What is CSS](#221-what-is-css)
    	- [2.2.2 Ways to apply CSS](#222-ways-to-apply-css) 
    	- [2.2.3 选择器 Selector](#223-选择器-selector)
    	- [2.2.4 RGB/RGBA Model](#224-rgb/rgba-model)
    	- [2.2.5 Hex Model](#225-hex-model)
    	- [2.2.6 Dev tool](#226-dev-tool)

# 课堂笔记

### Lecture 02 HTML&CSS
#### 2.1 HTML Introduction
- 现代Web app 的三大基石——HTML, CSS, JavaScript 
- CSS给HTML定义好的内容做排版，JavaScript提供网页与用户交互的能力

HTML基本结构： open + closing tag + content

> 技巧：vscode里 !加tab可以自动生成html

- 网页开发中，一开始创建的那个文件一般叫index.html

#### 2.1.1 HTML 基本结构
```html
<!DOCTYPE html>
  <html>
    <head>
      <title> Title </title>
    </heade>
    
    <body> 
    </body>
 
  </html>

```

- ```<!DOCTYPE html>``` 告诉浏览器或者文本编辑器这个文件是HTML file 
- ```<head>``` 任何在head里的东西不会被浏览器渲染出来
- ```<head>```、```<title>```、```<body>```有且只有一个
#### 2.1.2  live-server
- 在VScode extension里安装Live-server 插件，完成后点击右下角Go-live选项，会打开浏览器
或者在直接右击index.html open with Chrome

####  2.1.3 ```<h1>```
- 从```<h1>``` 到```<h6>``` 有各种不同等级的Heading，为页面创造视觉层级效果
- 实际工作时，UI Design会提供设计样本，Developer只需要跟着样本开发即可

#### 2.1.4 ```<p>```
-  ```<p>```里面可以换行
- ```<link rel = "icon" href = "" />```:设定icon

#### 2.1.5 ```<strong>```和```<em>```
- ```<strong>```和```<em>```wrap住要强调的元素，对element做强调

#### 2.1.6 ```<ol>```和```<ul>```
- 都由```<ol>```和```<ul>```作为parent，```<li>```作为children
```html 
<ol>
	<li></li>
	<li></li>
	<li></li>
<ol>
```
#### 2.1.7 ```<img>```
- self-closing 的 tag，一定要定义src和alt
  标签包含以下参数

- src：来源，如果图片文件在当前路径，直接使用xxx.jpg, 若在其他地方的img文件夹里，则加上 ./img/xxx.jpg

图3

- alt:  图片描述，img加载不出来，告诉它这个图片是干嘛的, 

- height, width 调节图片尺寸

#### 2.1.8 ```<a>```
- href：代表链接指向的网页
- target：_blank  代表点击链接会跳转到一个新的tab

#### 2.1.9 HTML 语义化
article和header应该怎么放？这是一个很主观的东西，以下是一个例子
```html
<section>
  <article>
    <header>
      <h1> Title </h1>
    </header>
    <p>This is paragraph</p>
  </article>
</section>
```

####  2.2 CSS
#### 2.2.1 What is CSS
- CSS Rule
- Selector + Declaration block + Property + Value + Declaration / Style
#### 2.2.2 Ways to apply CSS
####  External style:
External style(推荐方式): head里加link标签
#### Inline style:
Inline style（最不推荐）: 省略了找node的过程，但是非常不推荐，不可复用，无单一性原则
#### Internal style:
Internal style: 也是不推荐，会让html显得很长

#### 2.2.3 选择器 Selector
写CSS的时候，表明他要附着在什么上面：
- Class Selector：可复用，可叠加，一般最常用
- Id Selector：只能用在一个element里，用一次，所以不是很常用
！分清楚id, class的区别
Q： 选择所有的<li>的第一个：
A： inline加入class=“first-li” 或者 CSS里使用 li:first-child
*li:nth-child(3) 或者更specific 的 article p: first-child
Q:  选择<a>的属性
A：a:link 代表带href这个attribute的<a>, a:visited 代表链接点过之后的style，a: hover代表鼠标移到链接上面的style

Q：当多个选择器作用于同一个element时，哪个会生效？
A：图3 图4

#### 2.2.4 RGB/RGBA Model
每种颜色都可以用Red、Green、Blue(+Transparency)的结合来表示
>e.g. 
>R  G  B
255  0  0
纯红

* RGB Model中的 Transparency被hardcode成1

>R    G    B     A
0 255  255 0.3

#### 2.2.5 Hex Model
使用 0 - ff 代替RGB Model中的 0 - 255
>e.g.
#00ffff
纯蓝

- 实际工作中，RGB和Hex可以混用，用google找到相关网站

### 2.2.6 Dev tool（Chrome）：
快捷键：cmd+shif+i/ctrl+shift+i
- 直接在调试窗口更改css，以显示效果
- Console: 查报错，也可以直接写代码，比如
```js
document.querySelectorAll("h1")
```
- Sources: 看源文件 
-	Network：看加载过程中的请求和文件
- Performance：看performance，比如页面加载时间
- Memory: 看页面memory使用情况，不常用
- Application：用来看cookie，storage使用情况
- Lighthouse:也是用来做performance，整体的performance，SEO，Accessibility等的分析
- Accessibility
  - devtools axe-core extension，根据分数给网站调优
> 小技巧：可以直接在Dev Tool中看一些源码，借鉴到自己项目



