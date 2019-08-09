---
title: vue滚动数据控制纵向滚动条
date: 2019-08-05 11:04:27
tags:
---

```javascript
  mounted() {
    clearInterval(this.intervalidList)
    // 获取需要绑定的table
    this.dom = this.$refs.alarmOf.bodyWrapper
    this.dom.addEventListener('scroll', () => {
      // 滚动距离
      const scrollTop = this.dom.scrollTop
      // 变量windowHeight是可视区的高度
      const windowHeight = this.dom.clientHeight || this.dom.clientHeight
      // 变量scrollHeight是滚动条的总高度
      const scrollHeight = this.dom.scrollHeight || this.dom.scrollHeight
      if (scrollTop + windowHeight === scrollHeight) {
        // 获取到的不是全部数据 当滚动到底部 继续获取新的数据
        this.dom.scrollTop = 0
      }
    })
    this.intervalidList = setInterval(() => {
      this.dom.scrollTop++
    }, 100)
  },
```

