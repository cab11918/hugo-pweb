---
weight: 1
bookCollapsedSection: false
title: "Thoughts on Implementing Business Logic Splitting in Lists"

---

## **Thoughts on Implementing Business Logic Splitting in Lists**

<kbd style='background-color:#FF9B6A;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF9B6A; border-radius: 4px; font-size: 15px'>Redux</kbd> <kbd style='background-color:blue;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:blue; border-radius: 4px ; font-size: 15px'>JS</kbd><kbd style='background-color:#FF5151;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF5151; border-radius: 4px ; font-size: 15px'>Note</kbd>



### **Introduction**

List display elements are commonly used in frontend development for various business scenarios. As an SPA (Single Page Application) grows and the functional requirements increase, splitting an existing list into two halves can sometimes be a challenging task.

<div style="display:flex; justify-content:center">
  <img src="/Users/minghaoyu/Library/Application Support/typora-user-images/image-20211218102907320.png" alt="image-20211218102907320" style="zoom: 33%;" />
  <img src="/Users/minghaoyu/Library/Application Support/typora-user-images/image-20211218103112660.png" alt="image-20211218103112660" style="zoom:33%;" />
  </div>


​	As depicted above, the time constraints for this requirement are quite tight. When initially considering this problem, we often tend to split the global list in Redux into two lists using business logic and then present them using the component's local state to achieve the splitting. However, the problem arises when dealing with feature-rich, large-scale applications where each individual element has more than five different functionalities for operations such as create, read, update, and delete. This doesn't even include the interactivity with other elements. Consequently, we would need to add new code for each existing functionality to cater to the current local list.

### **Implementation Approach**

Since our goal is to preserve the existing list in the Redux state without introducing additional global or component-specific states, and to ensure that the existing functionalities can be reused without modifications, we can achieve this by conditionally rendering the original list multiple times.

Specifically:

```js
arr1 -> [1,2,3,4,5]
arr1(render(i<3)) -> [1,2]
arr1(render(!i<3)) -> [3,4,5]
```

### **Technical Challenges/Issues**

While the business logic itself may not be complex, the implementation approach is crucial. Using two filter renderings will inevitably have a performance impact and introduce other potential drawbacks. However, in time-constrained and urgent scenarios, it is a relatively minimal-effort solution. The absence of additional new states also facilitates code maintenance in the future.





