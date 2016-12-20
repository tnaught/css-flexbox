## 基本概念
1. 任何元素都可以使用flex布局，display:flex或display: inline-flex; ([DEMO](http://localhost:5000/flex.html#1))

2. 设为flex布局的元素为flex container,flex container的子元素为flex item 

3. 主轴：main axis,main start,main end,main size  

4. 交叉轴：cross axis,cross start,cross end,cross size ([DEMO](http://localhost:5000/flex-flow.html))  

5. 设为flex布局以后，flex item的float、clear和vertical-align失效

6. 如果flex container设定了高度，那item的高度都是这个值，如果container是auto,则container的最大高度就是item内容撑开的最大高度。

## 浏览器支持情况：  

+ Chrome 29+(最新55)  
+ Firfox 28+(最新50)  
+ Internet Explorer 11+  
+ Opera 17+  
+ Safari 6.1+(加-webkit-)  
+ Android 4.4+  
+ iOS 7.1+(加-webkit-)  

加前缀的情况下支持率如下：

| 地区 | 全部支持 | 部分支持 | 总 |
| :------:| ------: | :------: |:----:|
| 中国 | 69.13% | 19.69% |88.81% |
| 全球|82.98%|14.34% | 97.32% 


## 属性
[css-tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)上介绍得很详细，这里简单的罗列一下  
flex container的属性:
	
	+ flex-direction：row | column | row-reverse | column-reverse(受writing-mode相关)
	+ flex-wrap: nowrap | wrap | wrap-reverse
	+ flex-flow: flex-direction flex-wrap([DEMO](http://localhost:5000/flex-flow.html))
	+ justify-content: flex-start(default) | flex-end | center | space-between | space-around
	+ align-items: flex-start | flex-end | center | baseline | stretch((default, 没有height的情况下才能stretch，stretch不会超过max-height值，不会小于min-height的值)
	+ align-content: flex-start | flex-end | center | space-between | space-around | stretch(default)

flex item的属性：  

	+ flex-grow：0
	+ flex-shrink: 1
	+ flex-basis: auto
	+ flex: flex-grow（缺省值1,和默认值不同) flex-shrink(缺省值1) flex-basis(缺省值：0,和默认值不同)[0和auto的区别](http://localhost:5000/flex.html#2)
	+ order[DEMO](http://localhost:5000/order.html)
	+ align-self:flex-start | flex-end | center | baseline | stretch

## 和其他属性的关系

1. 绝对定位元素 
	> * absolute元素的flex值不生效([DEMO](http://localhost:5000/absolute.html))   	 
	> * 计算absolute元素默认定位的时候可以把absolute当作一个孤立的flex item来看待，也就是说用来对齐的属性(`align-items`、`justify-content`、`align-self`)是生效的  
	> * 在有left和top的情况下absolute元素的定位规则保持不变
	   
2. margin 
	> * margin不会发生合并，flex container和flex item的margin不合并，flex item之间的margin也不合并  
	> * margin auto可以实现居中对齐([DEMO](http://localhost:5000/margin.html))   
	> * 百分值的margin会有浏览器差异性，不建议使用
	
 
## flex-grow和flex shrink的计算
[详情见DEMO](http://localhost:5000/flex.html)

## width、flex-basis、min-width、max-width、'content-width'的关系

	1. 在flex-basis的值为非auto的时候flex-basis用来grow或shrink,grow的最大值为max-width，如果max-width的值为auto，max-width的值用max(width,'content-width')的值来代替，如果max-width和width都没有，那就由'content-width'决定了。shrink的计算方法同理，可收缩的最小值为min-width,如果min-width的值为auto,则用min为(width, 'content-width')来代替，如果min-width和width都没有，那就由'contente-width'来决定了。
  2. 如果grow或shrink的值不在(min-width, max-width)的范围内，那么该项最终宽度值用min-width或max-width代替，然后对新的剩余空间或者不足空间进行重新分配。也就是会发生回溯，效率可能不高。
  3. 在flex-basis的值为auto的时候，flex-basis由width来代替，如果width也没有那就由'content-width'来代替了。这个时候即使设置了flex-shrink的值也有可能发生内容溢出了
  4. 'content-width'是一个很大的变数，最终是由文本长度(***主要受英文不换行单词的影响***)和浏览器决定的，如果想不受'content-width'的影响，建议将min-width和max-width设置为非auto的值


## conclusion
1. 不用考虑浏览器不兼容的情况下，真的是比float、负margin的那些奇技淫巧要强大太多了，有机会大家多尝试起来吧

2. 当min-width和max-width为auto的时候，flex item弹性宽度的计算比较复杂，需要特别注意，不过主要是针对是长英文字符串的情况。

3. 在高度的计算上，尤其是align-items/align-content的值为stretch的时候，也需要注意max-height min-height的计算,不过stretch的时候剩余空间是平均分配的，计算起来比较简单

4. 有不少浏览器兼容的问题，见[caniuse中的known issues](http://caniuse.com/#feat=flexbox),有待进一步研究和探讨 


#reference  

+ [http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)   
+ [https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
+ [https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties)
+ [http://caniuse.com/#feat=flexbox](http://caniuse.com/#feat=flexbox)
+ [https://zhuanlan.zhihu.com/p/24372279?from=timeline&isappinstalled=0](https://zhuanlan.zhihu.com/p/24372279?from=timeline&isappinstalled=0)
+ [规范文档](https://www.w3.org/TR/css-flexbox/)
