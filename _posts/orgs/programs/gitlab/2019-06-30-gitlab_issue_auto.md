---
title: "Gitlab issue自动化处理"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2019-06-30 日 17:57&gt;</span></span>
layout: post
categories: 
- programming
tags: 
- gitlab
---

# Table of Contents

1.  [流程(OAuth password授权方法)](#org7af2354)
    1.  [认证获取Token](#org7cdec98)
    2.  [获取项目信息](#org94e29ba)
    3.  [获取项目Labels](#orgb64ad49)
    4.  [新建Issue](#orgdcae09c)


<a id="org7af2354"></a>

# 流程(OAuth password授权方法)


<a id="org7cdec98"></a>

## 认证获取Token

{% highlight bash %}
echo 'grant_type=password&username=<your_username>&password=<your_password>' > auth.txt
curl --data "@auth.txt" --request POST https://gitlab.example.com/oauth/token
{% endhighlight %}

{% highlight javascript %}
// 新建表单数据

const formData = new FormData()
formData.append("grant_type", "password")
formData.append("username", "user1")
formData.append("password", "password")
fetch("https://gitlab.example.com/oauth/token", {method:"POST", body:formData}).then(res=>res.json()).then(response=>{
    console.log(response);
}).catch(err=>console.log(err))
{% endhighlight %}

Response:

    {
      "access_token": "1f0af717251950dbd4d73154fdf0a474a5c5119adad999683f5b450c460726aa",
      "token_type": "bearer",
      "expires_in": 7200
    }


<a id="org94e29ba"></a>

## 获取项目信息

{% highlight bash %}
# 获取指定用户项目信息
curl --header "Authorization: Bearer <access_token>" https://gitlab.example.com/api/v4/users/:userid/projects

# 获取指定组的项目信息
curl --header "Authorization: Bearer <access_token>" https://gitlab.example.com/api/v4/groups/:userid/projects
{% endhighlight %}


<a id="orgb64ad49"></a>

## 获取项目Labels

获取指定项目的labels

{% highlight bash %}
curl --header "Authorization: Bearer <access_token>" https://gitlab.example.com/api/v4/projects/:id/labels
{% endhighlight %}


<a id="orgdcae09c"></a>

## 新建Issue

{% highlight bash %}
curl --request POST --header "Authorization: Bearer <access_token>" https://gitlab.example.com/api/v4/projects/4/issues?title=Issues%20with%20auth&labels=bug

# 或者提交表单数据
curl -d 'title=Issues2%20with%20auth&labels=bug' --request POST --header "Authorization: Bearer 5f3b9960d21507e12fc3119f88b874ba50a83f7a15b2eb3d78ccd00ec0f2dedc" 'https://gitlab.example.com/api/v4/projects/1/issues'
{% endhighlight %}

表单内容清单：

| Attribute | Type | Required | Description |
|---|---|---|---|
| id | integer/string | yes | The ID or URL-encoded path of the project owned by the authenticated user |
|---|---|---|---|
| title | string | yes | issue标题 |
|---|---|---|---|
| description | string | no | issue 描述内容，支持Markdown |
|---|---|---|---|
| labels | string | no | 标签 |
|---|---|---|---|
| 等等。。。 | | | |
|---|---|---|---|
