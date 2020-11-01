
>由于长时间对clientHeight、offsetHeight、scrollHeight、scrollTop这几个js-dom不理解，处于半迷糊状态，现在就仔仔细细实验整理一波，希望能做个总结，方便以后能快速理解别人代码和做出自己想要的。   

###结论

1. `clientHeight=height+padding-top+padding-bottom`
>`下面main这个div的clientHeight：1060px=1000px(height)+2x30px(padding-top+padding-bottom) `

2. `offsetHeight=height+padding-top+padding-bottom+border-top+border-bottom`
>`下面main这个div的offsetHeight：1070px=1000px(height)+2x30px(padding-top+padding-bottom)+2x5px(border-bottom+border-top)`
也就是说：`offsetHeight=clientHeight+border`
也就是说：`offsetHeight`和`clientHeight`都不包含`margin` 

3. `scrollHeight  `  
    1. 如果div不包含字内容或者子div的高度不大于父div的高度，不需要撑破父div，此时本div的scrollHeight=本clientHeight（不包含本div的border和margin）比如下面的main这个div，在这里scrollHeight=clientHeight=1060px 
    2. 如果div包含了子div并且子div的总高度大于父div的clientHeight，那么如果父div设置了`scroll:auto `就会有滚动此时父div的scrollHeight>clientHeight的。在下面的例子当中 `container的scrollHeight(1250px)=main的scrollHeight(1060px)+main的上下bottom(2x5px)+main的上下margin(2x20px)+top的height(60px)+container的上下padding(2x40px)`也就是说：当子div高度大于父div的高度时，此时父div的scrollHeight等于其内部所以子元素的height、padding、border、margin的总和加上自身的padding。这时候scrollHeight和自身的clientHeight关系不大，clientHeight当做了可以被用户看到的大小，相当于用户的显示，能看到的就这么多。

4. `scrollTop`当子div的内容高度比父div高度大并且设置了滚动时，scrollTop是父div中的内容已经向上移动并消失在可视范围的内容高度。当父div其内的内容滑到底时有个标志： `scrollHeight=clientHeight+scrollTop` 这个式子只能在滑到底时使用，没有滑
到底时 `scrollHeight>clientHeight+scrollTop`

5. 部分属性关系如下图：

![clientHeight、offsetHeight、scrollHeight、scrollTop](https://i.loli.net/2020/11/01/yLMx9aOk2vS8gsI.png) 

6. pageYOffset是window才有的属性，意思是body上滑了多少内容，相当于`scrollTop`

7. [项目地址codepen.io](https://codepen.io/hardlygo/pen/zYBWyeJ)
>源码 


```html
    <div class="container">
	<div class="top">Top</div>
	<div class="main">Main</div>
    </div>
    <button class="my-btn" >点我查真相</button>
    <div id="result"></div>
    <div id="result2"></div>
```

```css
.container{
	background:#e8ffff;
	width:100%;
	height:500px;
	overflow:auto;
	padding: 40px 0;
}
.top{
	width:100%;
	height:60px;
}

.main{
	background:#a6f6f1;
	width:100%;
	height:1000px;
	padding:30px 0;
	margin:20px 0;
	border-bottom: 5px solid #213e3b;
	border-top: 5px solid #213e3b;
}

#result{
	background:#41aea9;
}

#result2{
	background:#cee397;
}
```
```javascript
//要测试的属性 scrollHeight clientHeight offsectHeight scrollTop

let btn = document.querySelector(".my-btn");
btn.addEventListener("click", showresult);

function showresult() {

	let main = document.querySelector(".main");
	
	let scrollHeight = main.scrollHeight;
	let clientHeight = main.clientHeight;
	let offsetHeight = main.offsetHeight;
	let scrollTop = main.scrollTop;
	let pageYOffset = main.pageYOffset;

	let maincontent = `main 的 scrollHeight：${scrollHeight}px、clientHeight：${clientHeight}px、offsectHeight：${offsetHeight}px、scrollTop：${scrollTop}px、pageYOffset：${pageYOffset}。`;

	showInHtml("result", maincontent);

	let container = document.querySelector(".container");

	let containerscrollHeight = container.scrollHeight;
	let containerclientHeight = container.clientHeight;
	let containeroffsetHeight = container.offsetHeight;
	let containerscrollTop = container.scrollTop;
	let containerpageYOffset = container.pageYOffset;

	let containercontent = `container 的 scrollHeight：${containerscrollHeight}px、clientHeight：${containerclientHeight}px、offsectHeight：${containeroffsetHeight}px、scrollTop：${containerscrollTop}px、pageYOffset：${containerpageYOffset}。`;

showInHtml("result2",containercontent)

}

function showInHtml(id, content) {
	let result = document.getElementById(id);
	result.innerHTML = content;
}

//offsectHeight=height+padding-top+pading-bottom+border-top+border+bottom

```