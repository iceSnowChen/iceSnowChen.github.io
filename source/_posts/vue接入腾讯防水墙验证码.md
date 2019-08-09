---
title: vue接入腾讯防水墙验证码
date: 2019-08-07 10:28:15
tags:
---

```javascript
  created() {
    if (window.TencentCaptcha === undefined) {
      const script = document.createElement('script')
      const head = document.getElementsByTagName('head')[0]
      script.type = 'text/javascript'
      script.charset = 'UTF-8'
      script.src = 'https://ssl.captcha.qq.com/TCaptcha.js'
      head.appendChild(script)
    }
  },
  methods: {
    handleLogin() {
      const that = this
      const captcha = new window.TencentCaptcha('appid', function(res) {
          if (res.ret === 0) {
              that.loginForm.ticket = res.ticket
              that.loginForm.randstr = res.randstr
              that.loading = true
              console.log(that.loginForm)
              that.$store.dispatch('Login', that.loginForm).then(() => {
                  that.loading = false
                  that.$router.push({ path: '/' })
              }).catch(() => {
                  that.loading = false
              })
          } else {
              that.$message({
                  type: 'error',
                  message: '验证失败'
              })
          }
      })
      captcha.show()
  }
```

