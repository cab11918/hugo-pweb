---
weight: 1
bookCollapsedSection: false
title: "DOM实现报告自动分页"
---
## **实现自动分页效果的思路-插入元素并从移除DOM**

<kbd style='background-color:#FF9B6A;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF9B6A; border-radius: 4px; font-size: 15px'>DOM</kbd> <kbd style='background-color:#FF5151;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF5151; border-radius: 4px ; font-size: 15px'>JS</kbd> <kbd style='background-color:#87AAAA;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#87AAAA; border-radius: 4px ; font-size: 15px'>自动化</kbd>



### **引言**

​	很多时候前端开发者可以使用目前主流框架如React等实现对于比较复杂的报告（如体检报告、医疗影像报告...）的开发工作。但是如果用户的信息相对冗杂且信息的数量不确定时，每个页面所能展示的内容数量就难以被确定。举个例子，一个肺部疾病的病人可能在CT影像中可能只会有2个可疑病灶，也可能有20多个... 报告中的样式是无法确定的，很多时候可能会因为业务原因作修改。这些修改包括：文字、图片、间距等等。

### **实现思路**

​	既然文字、图片等信息的来源通常是后端接口返回的数据，通过文字或者图片数量去计算然后通过JS方法去实现分组显然不会很准确。（光是中英文和样式就会导致每行自述不固定，图片的阴影、自适应缩放也是如此）如果能获取这些信息在文本流中的准确宽高度问题也就解决了。

`document.createElement`,`document.body.appendChild`,`document.body.removeChild`这三个方法刚好能帮我们解决这个问题。只需要在DOM中新建这个元素，获取高度，最后移除这个元素就能获得所需的信息并且在渲染完成之前不添加多余元素到页面。

```js
//预检文本在当前格式下将占用的高度，对于模拟新建的元素 a ，可以提前对其设定样式以保证测量所需性质（高度）的真实性
function preFlight(text: string) {
  var a = document.createElement("div")
  a.innerText = text
  a.style.width = '793px'
  document.body.appendChild(a);
  let temp = a.offsetHeight
  document.body.removeChild(a);
  return temp
}
```

### **技术难点/问题**

考虑到这种实现方法确实会基于现有数据在当前DOM外构建子树，当信息量大的时候这种分页方式也势必会影响性能。

### **参考**

[你真的了解回流和重绘吗](https://segmentfault.com/a/1190000017329980)

[document.body.appendChild()会重新渲染整棵DOM树吗](https://segmentfault.com/q/1010000013551201)











