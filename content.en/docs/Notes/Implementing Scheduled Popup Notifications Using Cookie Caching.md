---
weight: 1
bookCollapsedSection: false
title: "Implementing Scheduled Popup Notifications Using Cookie Caching"
---
## Implementing Scheduled Popup Notifications Using Cookie Caching

<kbd style='background-color:#FF9B6A;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF9B6A; border-radius: 4px; font-size: 15px'>JS-Cookies</kbd> <kbd style='background-color:#FF5151;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF5151; border-radius: 4px ; font-size: 15px'>MomentJS</kbd>



### **Introduction**

In frontend Single-Page Applications (SPAs), there is often a need to collectively and controllably notify users about critical information. In this particular business scenario, for instance, a medical institution may choose not to display relevant information about a person's medical examination until they have signed the necessary agreements. This requires presenting a notification message to each user account within the platform. Additionally, there may be a time limit for displaying this notification, such as not showing it after seven days. Is there a way to fulfill this requirement without relying on backend storage for field information?

### **Implementation Approach**

Firstly, it is essential to establish that the popup notifications are based on the institution, where each account under the institution has a unique ID. Even if different users log in on the same computer, their timers are separate. When a user logs in for the first time on a computer, we can set a cookie for each account using `Cookie.set('accountID-date', time)` (the time can be generated using dependencies like Moment.js). This way, when we need to display the information or perform other actions, we can simply compare the stored time in the cookie with the current time. This approach reduces the time cost of adding fields in the backend while achieving the desired functionality.

```js
// Check if the date corresponding to the ID exists, indicating whether it is the first login. Set a seven-day limit for displaying sensitive information.
    if (Cookie.get(accountUuid + '-date') === undefined) {
      Cookie.set(accountUuid + '-date', today);
      console.log(Cookie.get(accountUuid + '-date'), 'id-date');
    }
```

```js
// Check if the corresponding ID's date exists, i.e., whether it is the first login. Set a seven-day limit for displaying sensitive information.
    const today = moment().format('YYYY-MM-DD');
    const accountUuid = Cookie.get('cloud-accountUuid');
    if (Cookie.get(accountUuid + '-date') !== undefined) {
      let dayPassed = moment(today).diff(moment(Cookie.get(accountUuid + '-date')), 'days');
      console.log(dayPassed, 'daypassed');
      if (dayPassed > 6) {
        setCanceled(false);
      }
    }
  }, [token]);
```

### **Technical Challenges/Issues**

Implementing such methods can be challenging when it comes to high-priority and critical notifications. Cookie storage may not work in browsers' incognito mode and can be easily manipulated by malicious users. Additionally, once this implementation is deployed, it becomes difficult to maintain or modify. When there are changes in requirements or business logic, a new version needs to be deployed with deprecated timestamps added to the cookies. If this method is extensively used, it can pollute the user's cookie environment and potentially lead to bugs caused by cookie naming conflicts.

### **Reference**

[你真的了解回流和重绘吗](https://segmentfault.com/a/1190000017329980)

[document.body.appendChild()会重新渲染整棵DOM树吗](https://segmentfault.com/q/1010000013551201)

[Document.cookie](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie#read_all_cookies_accessible_from_this_location)









