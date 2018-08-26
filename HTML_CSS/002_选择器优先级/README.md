## **选择器的优先级和计算**
### **优先级**（从高到低排列）
1. 在属性后面有！import的元素样式
2. 作为style写在元素中的内联样式
3. id选择器
4. class选择器
5. 标签选择器
6. 相邻选择器
7. 子代选择器
8. 后代选择器
9. 统配符选择器
10. 属性选择器
11. 伪类选择器

### **复杂场景计算方法**

![](https://raw.githubusercontent.com/funny-man/zee-blong/master/HTML_CSS/002_%E9%80%89%E6%8B%A9%E5%99%A8%E4%BC%98%E5%85%88%E7%BA%A7/1535272011759_21.png)


## **关于a:link, a:hover, a:active, a:visited顺序**

**正确顺序应为：**

1. a：link
2. a：visited 
3. a:hover 
4. a:active

**原因：**

- 1.当选择器优先级别相同时，后定义的会覆盖先定义的
- 2.以此类推，当鼠标经过未访问链接，同时有link和hover属性，
由于后定义的覆盖先定义的，所以hover在后面
- 以此类推，当鼠标经过已访问链接，同时有visited和hover属性，
由于后定义的覆盖先定义的，所以hover在link和visited后面
