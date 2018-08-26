# BFC 

> BFC的全称是 Block Format Content直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

## 如何生成 BFC
当父目录的

- float属性不为none
- position为absolute或者fixed
- display为inline-block,table-cell,table-caption,fle x,inline-flex，
- overflow不为visible

都会生成BFC。

## 作用
**清除浮动**

如图由于内部元素浮动无法撑开父容器

![](https://github.com/funny-man/zee-blong/blob/master/HTML_CSS/003_BFC_%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8/1488720104361_2.png)

因此我们可以通过为父容器加入overflow: hidden;触发父容器的bfc使父容器计算高度时候把内部的浮动元素包含。

![](https://github.com/funny-man/zee-blong/blob/master/HTML_CSS/003_BFC_%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8/1488454106016_2.png)

**防止垂直margin重叠（折叠）**

如图当两个div设置margin:50px时候但是他们之间的距离还是50px说明两个margin重叠（折叠）了

![](https://github.com/funny-man/zee-blong/blob/master/HTML_CSS/003_BFC_%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8/1488454106495_5.png)

在其中一个div父容器加入overflow: hidden;触发bfc此时间距变为100px

![](https://github.com/funny-man/zee-blong/blob/master/HTML_CSS/003_BFC_%E6%B8%85%E9%99%A4%E6%B5%AE%E5%8A%A8/1488454106377_4.png)

----

# 边距合并

**相邻元素：**两个或多个毗邻的普通流中的块元素垂直方向上的 margin 会折叠，取其中margin的最大值
**包含（父子）元素叠加：**包含元素的外边距隔着父元素的padding和border， 当这两项都不存在的时候， 父元素与其包含垂直外边距相邻的子元素（也就是第一个子元素和最后一个子元素）， 产生叠加。 添加padding border中的任何一项即会取消叠加。

**最终的margin值计算方法如下：** 

- 全部都为正值，取最大者；
- 不全是正值，这两个值相加得到的值
- 两个负值则取绝对值的最大值

## 兄弟元素之间发生外边距叠加
条件

    兄弟元素都不是float元素
    兄弟元素都不是absolute元素
    兄弟元素都不是inline-block元素

 那么让它们之间不发生外边距叠加则可以：

    让兄弟元素float
    让兄弟元素absolute
    让兄弟元素inline-block

如果实在要避免垂直边距折叠那就只能所有元素都只写margin-top或者margin-bottom

## 父子元素之间发生margin折叠

条件
父元素和第一个子元素发生margin-top叠加

    父元素没有创建BFC
    父元素和第一个子元素之间没有非空内容
    父元素没有border-top
    父元素没有padding-top
    
父元素和最后一个子元素发生margin-bottom叠加

    父元素没有创建BFC
    父元素height为auto、min-height为0
    父元素和最后一个子元素之间没有非空内容
    父元素没有border-bottom
    父元素没有padding-bottom
    
2种情况都总结了，那么让他们不发生外边距叠加也就显得很容易了：

    为父元素创建BFC
    为父元素设置相应的padding或者border

[内容参考外边距叠加](http://www.smallni.com/collapsing-margin/)

---

# 清除浮动

- clear:both 在父元容器中添加一个空的div，并向其添加样式clear:both清除浮动，使得父容器撑起来
- BFC:利用特定的属性触发父容器bfc，使父容器形成一个新的BFC.其便具有BFC包含浮动的特质，使高度撑起来。但是每个属性都有他的副作用。
- clearfix {zoom:1} 表示针对于IE6,7，其原理是使父容器形成一个类似于BFC的特性 
- clearfi:after {content:""; display:block; clear:both;} 和第一个方法类似但是不用再html中加无用标签
