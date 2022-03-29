# Lecture 03 CSS 进阶

## 主要知识点
- [Lecture 03 CSS进阶](#lecture-03-css进阶)
  - [3.1 Recap](#31-recap)
  	- [3.1.1 File Path](#311-file-path)
  	- [3.1.2 HTML语义化](#312-html-语义化)
  - [3.2 CSS 进阶](#32-css进阶)
  	- [3.2.1 Inheritance](#321-inheritance)
  	- [3.2.2 CSS Box modal](#322-css-box-modal)
  	- [3.2.3 margin](#323-margin)
  	- [3.2.4 padding](#324-padding)
  	- [3.2.5 block 和 inline elements](#325-block和inline-elements)
  	- [3.2.6 position](#326-position)
  	- [3.2.7 Units](#327-units)
  	- [3.2.8 Responsive Web Design](#328-responsive-web-design)
  	- [3.2.9 CSS Library](#css-library)   


# 课堂笔记

### Lecture 03 CSS 进阶

#### 3.1 Recap
```html
<article>
	<header>
		<h2> Header </h2>
		<img src="img" alt="img alt"/>
		<p>...</p>
	</header>
	...
```
article p:first-child 无法执行的理由：
```<article>```里面的第一个element不是```<p>```
可以改成 article header:first-child

#### 3.1.1 File path
absolute path: file or directory from the root
relative path: 把current working directory加进考虑
> . (代表current directory)
> ..（代表parent directory）
> pwd 会把current working directory给显示出来
> cd chang directory帮助在file system中navi

Folder 结构:
>-- assets
		--img
-- styles
-- templates
		blog.html
		index.html (You are here)
- 想要access img folder里的图片，需要把路径改成
../assets/img/xxx.jpg

#### 3.1.2 HTML 语义化
Benefits：
- 可以帮助做SEO
- 让element的选择更灵活
- Brower更好理解HTML档案
- 使 fellow developers 的code保持一致性

#### 3.2 CSS 进阶
#### 3.2.1 Inheritance
![img6](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE6.PNG)

#### 3.2.2 CSS Box modal
![img7](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE7.PNG)
- Final element width = left border + left padding + width + right padding + right border 
- top border + top padding + height + bottom padding + bottom border

#### 3.2.3 margin
margin: 跟外界的距离，border的外面，跟着上和左走;
- 两个div margin 叠加的时候，系统取中间最大值；e.g.一个margin 50，另一个60，系统会取60
>margin：auto 
把左边margin和右边margin能找到的最大空间做一个对半分

#### 3.2.4 padding
padding : 25px(top), 50px(left),50px(right),25px(bottom)
margin 的简写规则和 padding一致

#### 3.2.5 block和inline elements
block element：把所有元素从上至下排列，元素占据parent element所有的width，不会预留空间给下一个element做排列，
display：block 是default设置的元素为：body，main，header，footer，section，nav，aside，div，h1-h6，p，ul，ol，li。。。

inline element：只占据对内容展示来说必要的空间，不会全部占据parent element的width，给inline 元素加margin或padding，有时不会apply到全部上下左右
display：inline 是default设置的元素为：a，img，strong，em，button。。。

![img8](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE8.PNG)

#### 3.2.6 position
static：postioning不起作用
relative：和原始位置做对比，如原始位置为x，则top：30px 将element往下推 30px
fixed： position relative to viewport，随着缩放黏在viewport的某个地方，不常用
***absolute（常用）***：position to nearest position ancestor（该ancestor的postion状态须为relative），如果没有position ancestor，则使用document body，且会随着页面滑动而滑动
sticky：永远和realtive一起用，粘在一个element下面，工作中常用于search input下面的drop down

#### 3.2.7 Units:
#### ```px```
px: 用的比较少，因为是绝对单位; 长宽可能会用到
####  ```em```
em：相对单位，因为等于默认字体大小，所以默认值为16像素；跑到父元素找到的字体大小，有继承关系，如果父元素设置了不同的值，em值就会变得复杂
####  ```rem```
rem：跑到最外层root去找的字体大小，更常用，总是等于默认字体大小；
- 使用rem, 因为字体大小的基本单位是rem，所以更好比较
####  ```%```
%：相对单位，相对父元素占比
####  ```vw vh```
vw,vh: 占据在能看到的视窗大小上的百分比，用的比较少
- vw：viewwidth，视窗宽度
- vh：viewheight，视窗高度
> 如果css没有初始化，那么可能浏览器默认的属性会更改vw，vh的显示效果

#### 3.2.8 Responsive Web Design
- 随着屏幕的缩放，缩放页面上的内容，拉到一定程度，超过breakpoint后，style会变

#### 3.2.9 CSS library
- Bootstrap: https://getbootstrap.com/
- Foundation https://get.foundation/
- Pure CSS https://purecss.io/
- Mobi CSS https://getmobicss.com/
- Semantic UI https://semantic-ui.com/



