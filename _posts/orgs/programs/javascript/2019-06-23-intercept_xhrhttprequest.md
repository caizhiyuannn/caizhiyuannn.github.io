---
title: "拦截HTML XHR请求数据"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2019-06-23 日 22:13&gt;</span></span>
layout: post
categories: 
- programming
tags: 
- javascript
---

# Table of Contents

1.  [Javascript 通过脚本注入获取XHR请求数据](#orgdad500d)


<a id="orgdad500d"></a>

# Javascript 通过脚本注入获取XHR请求数据

使用场景 ： 油猴脚本获取网页自身请求内容，避免多次请求。

[来源： Stack Overflow](https://stackoverflow.com/questions/16959359/intercept-xmlhttprequest-and-modify-responsetext)

{% highlight javascript %}
// subject 用于rxjs 主题订阅。
(function(subject) {
    let rawOpen = XMLHttpRequest.prototype.open;
    let arg = null;
    XMLHttpRequest.prototype.open = function() {
        arg = arguments;
        if (!this._hooked) {
            this._hooked = true;
            setupHook(this);
        }
        rawOpen.apply(this, arguments);
    };
    // 添加hook获取内容
    function setupHook(xhr) {
        function getter() {
            // 删除 getter， 非删除属性。避免调用死循环
            delete xhr.responseText;
            let ret = xhr.responseText;
            //   console.log(ret);
            subject.next({ request: arg, response: ret });
            setup();
            return ret;
        }

        function setter(str) {
            console.log("set responseText: %s", str);
        }
        function setup() {
            Object.defineProperty(xhr, "responseText", {
                get: getter,
                set: setter,
                configurable: true
            });
        }
        setup();
    }
})(subject)
{% endhighlight %}
