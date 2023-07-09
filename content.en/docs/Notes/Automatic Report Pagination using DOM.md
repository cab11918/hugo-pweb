---
weight: 1
bookCollapsedSection: false
title: "Automatic Report Pagination using DOM"
---
### **Automatic Report Pagination using DOM**

<kbd style='background-color:#FF9B6A;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF9B6A; border-radius: 4px; font-size: 15px'>DOM</kbd> <kbd style='background-color:#FF5151;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF5151; border-radius: 4px ; font-size: 15px'>JS</kbd> <kbd style='background-color:#87AAAA;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#87AAAA; border-radius: 4px ; font-size: 15px'>Automation</kbd>



### **Introduction**

In many cases, frontend developers can use popular frameworks such as React to implement the development of complex reports, such as medical examination reports or medical imaging reports. However, when dealing with user information that is relatively complex and the quantity of information is uncertain, it becomes challenging to determine the amount of content that can be displayed on each page. For example, a patient with a lung disease may have only two suspicious lesions in a CT image, or there could be more than 20. The style of the report is also uncertain and may require modifications due to business reasons. These modifications may involve changes to text, images, spacing, and other elements.

### **Implementation Approach**

Since the source of information such as text and images usually comes from data returned by backend APIs, calculating and implementing grouping based on the quantity of text or images using JavaScript methods may not be accurate. Factors such as variations in text length due to different languages and styles, as well as the presence of image shadows and adaptive scaling, make it challenging to determine a fixed layout solely based on text or image count. However, if we can obtain the accurate width and height of these elements within the text flow, the problem can be resolved.

The methods `document.createElement`, `document.body.appendChild`, and `document.body.removeChild` can conveniently help us solve this problem. By creating a new element in the DOM, getting its height, and then removing the element, we can obtain the required information without adding any extra elements to the page before rendering is complete.

```js
// To determine the height occupied by the preflight text in the current format, we can set the necessary styles in advance for the simulated new element, "a," to ensure the accuracy of the measured property (height).
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

### **Technical Challenges/Issues**

Considering that this implementation method does involve constructing a subtree outside of the current DOM based on existing data, this pagination approach can potentially impact performance, especially when dealing with a large amount of information.

### Reference

[你真的了解回流和重绘吗](https://segmentfault.com/a/1190000017329980)

[document.body.appendChild()会重新渲染整棵DOM树吗](https://segmentfault.com/q/1010000013551201)











