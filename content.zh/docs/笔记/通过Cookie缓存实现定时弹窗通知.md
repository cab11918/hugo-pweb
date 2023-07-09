---
weight: 1
bookCollapsedSection: false
title: "Cookie缓存实现定时弹窗"
---
## **通过Cookie缓存实现定时弹窗通知**

<kbd style='background-color:#FF9B6A;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF9B6A; border-radius: 4px; font-size: 15px'>JS-Cookies</kbd> <kbd style='background-color:#FF5151;box-shadow:2px 2px rgba(0,0,0,0.3); color:white; border-color:#FF5151; border-radius: 4px ; font-size: 15px'>MomentJS</kbd>



### **引言**

​	前端SPA很多时候会需要集体性的且可控的通知用户一些关键信息。在此业务场景下，体检机构在未签约时将不会显示体检人的相关信息。这就需要对每个在平台内的每个账号弹出提示文字，有时，这个文字的出现还得有时间限制，比如七天以后这个通知就不再显示了。有没有一种方法能够不依托于后端字段信息的存储去实现这一需求呢？

### **实现思路**

​	首先，需要确定的前提是通知弹出是依据机构的，每家机构下的账户都有自己唯一的ID。即使在同一台电脑上登录了不一样的用户，他们的计时也是分开的。当用户是第一次在一台电脑上登录的时候，我们可以给每个account设置一个`Cookie.set('accountID-date',时间(此时间可以利用Moment-JS等依赖生成))` 这样子当我们在需要展示信息等时候我们只需要用Cookie里存储的时间与当前时间做一个对比就可以了，在实现功能的前提下也降低了后端增加字段的时间成本。

```js
//检查对应ID的日期是否存在，即是否第一次登陆，设置七天期限用于脱敏显示。
    if (Cookie.get(accountUuid + '-date') === undefined) {
      Cookie.set(accountUuid + '-date', today);
      console.log(Cookie.get(accountUuid + '-date'), 'id-date');
    }
```

```js
//检查对应ID的日期是否存在，即是否第一次登陆，设置七天期限用于脱敏显示。
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

### **技术难点/问题**

​	诸如此类的方法其实很难应用到高优先级、高重要性的通知上。Cookie的保存不能在浏览器的无痕模式下发挥作用且容易被人恶意修改。除此之外，这种实现方法一旦部署就会很难进行维护或者修改。当需求或者业务逻辑发生改变时，需要部署新版本给Cookies加上废弃时间戳。如果大量使用这种方法，必然会污染用户的Cookie环境，从而可能进一步引发一些由于Cookie命名所带来的bug

### **参考**

[你真的了解回流和重绘吗](https://segmentfault.com/a/1190000017329980)

[document.body.appendChild()会重新渲染整棵DOM树吗](https://segmentfault.com/q/1010000013551201)

[Document.cookie](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie#read_all_cookies_accessible_from_this_location)









