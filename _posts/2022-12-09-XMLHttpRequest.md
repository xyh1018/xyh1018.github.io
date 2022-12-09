---
layout: post
title: 封装AJAX
date: 2022-12-09 23:43
author: "xyh"
tags:
    - AJAX
    - javascript
---

```javascript
class Ajax {
            constructor(url, options) {
                this.url = url
                this.options = Object.assign({}, DEFAULT, options)
                this.init()
            }
            init() {
                let xhr = new XMLHttpRequest();
                this.xhr = xhr;
                let that = this;
                xhr.onload = function () {
                    if (that.ok()) {
                        console.log('成功');
                    } else {
                        console.log('失败');
                    }
                };
                // xhr.addEventListener(
                //     'load',
                //     () => {
                //         if (this.ok()) {
                //             console.log('success');
                //         } else {
                //             console.log('error');
                //         }
                //     },false
                // );
                xhr.open(this.options.method, this.url + this.addParam(), true)
                xhr.send(null)
            }
            // 检测响应的 HTTP 状态码是否正常
            ok() {
                const xhr = this.xhr;
                return (xhr.status >= 200 && xhr.status < 300) || xhr.status === 304;
            }
            // 在地址上添加数据
            addParam() {
                return this.addURLData(this.url,this.serialize(this.options.params))
            }
            // 给url添加?或者&
            addURLData(url,data) {
                if(!data) return;
                let mark = null;
                if(url.includes('?')) {
                    mark = '&'
                }else {
                    mark = '?'
                }
                return `${mark}${data}`
            }
            // 数据序列化成 a=b&c=d 格式的字符串
            serialize(param) {
                const results = [];
                for(const [key,value] of Object.entries(param)) {
                    results.push(`${encodeURIComponent(key)}=${encodeURIComponent(value)}`)
                }
                return results.join('&')
            }
        }
```
