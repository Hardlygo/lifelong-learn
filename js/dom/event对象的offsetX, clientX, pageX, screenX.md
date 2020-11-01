<!--
 * @Author: your name
 * @Date: 2020-11-01 20:36:31
 * @LastEditTime: 2020-11-01 22:14:23
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \leetcodee:\JSWorkSpace\lifelong-learn\js\dom\event对象的offsetX, clientX, pageX, screenX.md
-->
>现在需要对event对象的几大与坐标有关的属性做一个总结，以便于认识 

1. `offsetX|offsetY`
offsetX/Y获取到是触发点相对被触发dom的左上角距离(包括padding在内，不包括border)，不过左上角基准点在不同浏览器中有区别，以内容区左上角为基准点（不包括边框），如果触发点在边框border上会返回负值。
![offsetX/Y.png](https://upload-images.jianshu.io/upload_images/706345-bce478abf4183f84.png?imageMogr2/auto-orient/strip|imageView2/2/w/458/format/webp) 
>用途：待发现
 
 2. `clientX|clientY和pageX|pageY`
     1. `clientX|clientY`这对坐标相对于窗口，从窗口的顶部/左侧边缘计算得出，类似于css属性的`position:fixed ` `clientX|clientY`的原点是一直可以看得到的，这是窗口坐标。
     2. `pageX|pageY`这对坐标相对于文档根（文档左上角），即网页左上角，注意是网页，类似于css属性的`position:absolute ` 。`pageX|pageY`的原点会随着文档被滑动而看不到，这是文档坐标 。
     >当页面滚动到最开始时，此时窗口的左上角恰好是文档的左上角，它们的坐标彼此相等。但是，在文档移动之后，元素的窗口相对坐标会发生变化，因为元素在窗口中移动，而元素在文档中的相对坐标保持不变。在下图中，我们在文档中取一点，并演示了它滚动之前（左）和之后（右）的坐标： 
     
     ![QQ截图20201101210526](https://i.loli.net/2020/11/01/BixaZgG9dzyQXs1.jpg)
     > 当文档滚动了：
     > - pageY — 元素在文档中的相对坐标保持不变，从文档顶部（现在已滚动出去）开始计算
     > - clientY — 同一元素的窗口相对坐标确实发生了变化（箭头变短了），因为同一个点越来越靠近窗口顶部。 

    >特点：pageY=clientY+纵向已滚动长度
    >注意：这个纵向已滚动距离一般是子div高度大于父div此时这里的纵向已滚动距离是父div的scrollTop，子div的scrollTop是0，因为子div没有滚动。
 3. `screenX|screenY`获取到的是触发点相对显示器屏幕左上角的距离，不随页面滚动而改变。
 ![enter image description here](https://upload-images.jianshu.io/upload_images/706345-6b0be53496e58a18.png?imageMogr2/auto-orient/strip|imageView2/2/w/949/format/webp)
 而`clientX|clientY`永远都是【上图应用】下来的最左上的那一点。

 4. 元素坐标：`getBoundingClientRect` 
    [到这里去看，一定要点进去看，很重要，很详细的介绍了getBoundingClientRect](https://zh.javascript.info/coordinates#yuan-su-zuo-biao-getboundingclientrect)

    方法 `elem.getBoundingClientRect() `返回最小矩形的窗口坐标，该矩形将 elem 作为内建 DOMRect 类的对象。

主要的 DOMRect 属性：

+ x/y — 矩形原点相对于窗口的 X/Y 坐标，
width/height — 矩形的 width/height（可以为负）。
此外，还有派生（derived）属性：

+ top/bottom — 顶部/底部矩形边缘的 Y 坐标，
left/right — 左/右矩形边缘的 X 坐标。
![QQ截图20201101215658](https://i.loli.net/2020/11/01/2v7mEUCyk9qojSN.jpg)

>当上下滑动窗口时 top/bottom/y是会变化的。
>注意：这里的坐标原点都是与clientY|clientX的坐标原点是一样的，故可以利用css的fixed属性设置某个元素固定在视窗口的某处，使用 CSS position 以及 left/top（或 right/bottom）。

5. #### 文档坐标
文档相对坐标从文档的左上角开始计算，而不是窗口。

在 CSS 中，窗口坐标对应于 position:fixed，而文档坐标与顶部的 position:absolute 类似。

我们可以使用 position:absolute 和 top/left 来把某些内容放到文档中的某个位置，以便在页面滚动时，元素仍能保留在该位置。但是我们首先需要正确的坐标。

这里没有标准方法来获取元素的文档坐标。但是写起来很容易。

这两个坐标系统通过以下公式相连接：
+ `pageY` = `clientY` + 文档的垂直滚动出的部分的高度。
+ `pageX` = `clientX` + 文档的水平滚动出的部分的宽度。


### 总结
页面上的任何点都有坐标：

1. 相对于窗口的坐标 — `elem.getBoundingClientRect()`。

2. 相对于文档的坐标 —` elem.getBoundingClientRect()` 加上当前页面滚动。

窗口坐标非常适合和 position:fixed 一起使用，文档坐标非常适合和 position:absolute 一起使用。

这两个坐标系统各有利弊。有时我们需要其中一个或另一个，就像 CSS position 的 absolute 和 fixed 一样。

参考：[坐标(一定要去看)](https://zh.javascript.info/coordinates#yuan-su-zuo-biao-getboundingclientrect)

[event对象的offsetX, clientX, pageX, screenX，你能分清吗](https://www.jianshu.com/p/9afff6038bf5)
![enter image description here](https://upload-images.jianshu.io/upload_images/706345-a4d8d293324e9bf2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)