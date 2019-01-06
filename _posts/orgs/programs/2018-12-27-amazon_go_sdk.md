---
title: "AWS SDK for GOLang"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-12-27 Thu 14:47&gt;</span></span>
layout: post
categories: 
- programming
tags: 
- sdk 
- golang
---

# Table of Contents

1.  [SDK入门](#orgb56189e)
    1.  [安装go版SDK](#orgf7dd2c3)
    2.  [获取AWS访问密钥](#org87a3286)
2.  [配置SDK](#org19ae085)
    1.  [指定 AWS Region](#org2a87467)
        1.  [sdk没有指定默认的region，配置方法如下](#orgae577a6)
        2.  [示例](#org888c99c)
    2.  [指定Credentials（信任）](#orga324aad)
        1.  [创建credentials文件.aws/credentials](#org36f3cce)
        2.  [可以通过指定credentials](#org1ab437d)
3.  [Amazon CloudWatch Examples Using the AWS SDK for Go](#org815dfc5)
    1.  [Getting Metrics from CloudWatch](#org4c646fd)


<a id="orgb56189e"></a>

# SDK入门


<a id="orgf7dd2c3"></a>

## 安装go版SDK

{% highlight shell %}
go get -u github.com/aws/aws-sdk-go/...
{% endhighlight %}


<a id="org87a3286"></a>

## 获取AWS访问密钥

Access keys 由 access key ID 和 secret access key 组成。通过AWS 的IAM console 的 Security credentials面板创建。\\
例如：

    Access key ID: AKIAIOSFODNN7EXAMPLE
    Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY


<a id="org19ae085"></a>

# 配置SDK


<a id="org2a87467"></a>

## 指定 AWS Region

指定Region说明你是通过对应的region来进行发送请求的。例如us-west-2 或 us-east-2。\\
不同region表示不同的区域，能够减小数据发送的延迟。\\
[AWS官网文档说明](https://docs.aws.amazon.com/zh_cn/general/latest/gr/rande.html)


<a id="orgae577a6"></a>

### sdk没有指定默认的region，配置方法如下

-   设置环境变量 `AWS_REGION` 来指定默认region
-   设置环境变量 `AWS_SDK_LOAD_CONFIG` 值为 `true` 来通过 `.aws/folder` 配置文件获取region值
-   通过 `.aws/folder` 获取到region值时，设置NewSessionWithOptions方法参数SharedConfigState为SharedConfigEnable
-   通过sdk创建session明确指定region


<a id="org888c99c"></a>

### 示例

    # Linux, MACOS, unix
    export AWS_REGION=us-west-2
    
    # windows
    set AWS_REGION=us-west-2
    
    # 在session中指定
    sess, err := session.NewSession(&aws.Config{Region: aws.String("us-west-2")})


<a id="orga324aad"></a>

## 指定Credentials（信任）

SDK需要通过access ID和secret 来签名请求aws数据。设置方法如下：

1.  通过环境变量设置
2.  通过共享credentials文件设置。在.aws/credentials
3.  If your application is running on an Amazon EC2 instance, IAM role for Amazon EC2.


<a id="org36f3cce"></a>

### 创建credentials文件.aws/credentials

    # 通过profile指定不同的密钥
    
    [default]
    aws_access_key_id = <YOUR_DEFAULT_ACCESS_KEY_ID>
    aws_secret_access_key = <YOUR_DEFAULT_SECRET_ACCESS_KEY>
    
    [test-account]
    aws_access_key_id = <YOUR_TEST_ACCESS_KEY_ID>
    aws_secret_access_key = <YOUR_TEST_SECRET_ACCESS_KEY>
    
    [prod-account]
    ; work profile
    aws_access_key_id = <YOUR_PROD_ACCESS_KEY_ID>
    aws_secret_access_key = <YOUR_PROD_SECRET_ACCESS_KEY>

    # 指定app时指定profile
    
    $ AWS_PROFILE=test-account myapp
    
    # 在session中指定profile
    sess, err := session.NewSession(&aws.Config{
        Region:      aws.String("us-west-2"),
        Credentials: credentials.NewSharedCredentials("", "test-account"),
    })


<a id="org1ab437d"></a>

### 可以通过指定credentials

1.  AWS<sub>ACCESS</sub><sub>KEY</sub><sub>ID</sub>
2.  AWS<sub>SECRET</sub><sub>ACCESS</sub><sub>KEY</sub>
3.  AWS<sub>SESSION</sub><sub>TOKEN</sub>(optional)

例如: Linux, OS X, or Unix

    $ export AWS_ACCESS_KEY_ID=YOUR_AKID
    $ export AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
    $ export AWS_SESSION_TOKEN=TOKEN

例如：Windows

    > set AWS_ACCESS_KEY_ID=YOUR_AKID
    > set AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
    > set AWS_SESSION_TOKEN=TOKEN

例如：代码中嵌入credentials

    sess, err := session.NewSession(&aws.Config{
        Region:      aws.String("us-west-2"),
        Credentials: credentials.NewStaticCredentials("AKID", "SECRET_KEY", "TOKEN"),
    })


<a id="org815dfc5"></a>

# Amazon CloudWatch Examples Using the AWS SDK for Go


<a id="org4c646fd"></a>

## Getting Metrics from CloudWatch

这个例如教你如何检索一个已经发布的cloudwatch的开销列表数据和发布数据点到cloudwatch开销记录，总的来说就是获取监控数据和发送监控数据。

主要用到方法：

1.  ListMetrics
2.  PutMetricData
