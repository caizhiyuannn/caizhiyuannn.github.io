---
title: "面向对象设计模式-设计原则"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2018-10-15 Mon&gt;</span></span> \today
layout: post
categories: 
- programming
tags: 
- 面向对象 
- 设计模式 
- java
---

# Table of Contents

1.  [设计原则](#org183c60d)
    1.  [单一职责](#orgbfaebfc)
    2.  [里氏替换原则](#org9bd9372)
        1.  [示例](#org5d70fa0)
    3.  [依赖倒置原则](#orgd815436)
        1.  [依赖的三种写法](#org3ba40ad)
    4.  [接口隔离原则](#org7b9650d)
    5.  [迪米特法则](#org0aff8f7)
    6.  [开闭原则](#org778482b)


<a id="org183c60d"></a>

# 设计原则

资料：《设计模式模式之禅》

---


<a id="orgbfaebfc"></a>

## DONE 单一职责

单一职责原则，英文缩写SRP，全称Single Responsibility Principle。  
原始定义：

> There should never be more than one reason for a class to change。

-   一个类，最好只负责一件事，只有一个引起它变化的原因。


<a id="org9bd9372"></a>

## DONE 里氏替换原则

原始定义：

> 1.  If for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T,
>     the behavior of P is unchanged when o1 is substituted for o2 then S is a subtype of T.  
>     如果对每一个类型为 T1的对象 o1，都有类型为 T2 的对象o2，使得以 T1定义的所有程序 P 在所有的对象 o1 都代换成 o2 时，程序 P 的行为没有发生变化，那么类型 T2 是类型 T1 的子类型。
> 
> 2.  Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.  
>     所有引用基类的地方必须能透明地使用其子类的对象。

遵循规则：

-   子类必须完全实现父类的方法
-   子类可以有自己的拓展方法或属性
-   子类覆盖(overload)或实现父类的方法时输入参数可以被方法，但是要兼容父类方法；就是覆盖参数兼容父类，子类可以再拓展参数。
-   子类覆写(override)或实现父类的方法时输出结果可以被缩小，方法的后置条件（即方法的返回值）要比父类更严格。


<a id="org5d70fa0"></a>

### 示例

{% highlight java %}
// 抽象类
public abstract AbstractGun {
    public abstract void shoot();
}

// 子类实现父类或抽象类方法, 复写抽象类方法
class Handgun extends AbstractGun {
    @Override
    public void shoot() {
        System.out.println("Handgun");
    }
}

class Rifle extends AbstractGun {
    public void shoot() {
        System.out.println("Rifle");
    }
}

// 调用
class  Soldier {
    private AbstractGun gun;

    public void setGun(AbstractGun _gun) {
        this.gun = _gun
    }

    public void killEnemy() {
        this.gun.shoot();
    }
}

//
public class Client {
    public static void main(String[], args) {
        Soldier sanmao = new Soldier();
        sanmao.setGun(new Rifle);
        sanmao.killEnemy();
    }
}

{% endhighlight %}


<a id="orgd815436"></a>

## DONE 依赖倒置原则

原始定义：

> High level modules should not depend upon low level modules. Both should depend upon abstractions.  
> Abstractions should not depend upon details. Details should depend upon abstractions.

-   高层模块不应该依赖低层模块，两则都应该其抽象。
-   抽象不应该依赖细节。
-   细节应该依赖抽象


<a id="org3ba40ad"></a>

### 依赖的三种写法

-   通过构造函数传递依赖对象
    
    {% highlight java %}
    // 依赖 ICar 接口实现的car
    
    public interface IDriver {
        public void drive();
    }
    
    public class Driver implements IDriver {
        private ICar car;
        // 通过构造函数注入依赖的对象
        public Driver(Icar _car) {
            this.car = _car;
        }
    
        public void drive() {
            this.car.run();
        }
    
    }
    {% endhighlight %}
-   通过setter方法传递依赖对象
    
    {% highlight java %}
    // 依赖ICar 接口实现的car
    
    public interface IDriver {
        public void setCar(Icar car);
        public void drive();
    
    }
    
    public class Driver implements IDriver {
        private Icar car;
        public void setCar(Icar car) {
            this.car = car;
        }
    
        public void drive() {
            this.car.run();
        }
    }
    {% endhighlight %}
-   通过接口声明依赖对象
    
    {% highlight java %}
    // 通过接口声明依赖对象
    
    public interface IDriver {
        public void drive(ICar car);
    }
    
    
    public class Driver implements IDriver {
        public void drive(ICar car) {
            car.run();
        }
    }
    {% endhighlight %}


<a id="org7b9650d"></a>

## TODO 接口隔离原则


<a id="org0aff8f7"></a>

## TODO 迪米特法则


<a id="org778482b"></a>

## TODO 开闭原则
