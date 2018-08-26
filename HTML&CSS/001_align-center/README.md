# 居中

---

## 水平居中

**内联元素**
在父元素上写text-align : center
**块级元素**
在元素上设置 margin : 0 auto ;(margin-left : auto;   margin-right : auto;)


## 垂直居中

- 通过absolute的top：50%并且设置 margin-top：-child的高度 （这种方法前提是知道子元素高度）
[预览](http://js.jirengu.com/fowujuheru/1/edit)

- 通过absolute的top：50%并且利用CSS3的transform: translate(-50%, -50%);移动自身宽高的50%
[预览](http://js.jirengu.com/fowujuheru/1/edit)

- 通过child的before或者after添加一个元素都设置display: inline-block;并且before或者after设置高度100%；每个元素添加vertical-align: middle;（通常情况下before或者after设置宽度为0为不可见状态）
[预览](http://js.jirengu.com/lexiluwake/1/edit)

- table>tr>td中的元素不管是div还是文字都会以垂直居中（也可以吧div设置display: table；变成table效果一样）
[预览](http://js.jirengu.com/fetibotide/1/edit)



