---
title: C++ - 实现单例模式
date: 2021-09-02 21:58:21
categories: 
- C++
- 设计模式
tags: 
- C++
- 设计模式
excerpt: 使用 C++ 实现单例模式的多种方式，包括但不限于：懒汉、懒汉+双重检查锁、饿汉、局部静态实例等等方式。
---

## 1 概述

总体实现方式：将构造函数设为私有的 private，然后通过类的一个**公共静态函数**来生成实例。
并且，拷贝构造函数、移动构造函数、赋值运算符等也要设为 private（或者=delete）

几种实现方式：

- 懒汉（非线程安全）
- 懒汉+互斥锁 mutex（双重检查锁模式）（线程安全）
- 饿汉（天生线程安全）
- 局部静态实例（线程安全）
- pthread_once（线程安全）
- memory barrier 模式（线程安全）
- Atomic（线程安全）

## 2 实现

### 2.1 懒汉

懒汉方式，只有当用到该单例时，才初始化单例。

具体实现：
```cpp
/* 
 * singleton.h
 */
#ifndef SINGLETON_H
#define SINGLETON_H

class Singleton {
public:
    static Singleton * getInstance();

private:
    Singleton() = default;
    ~Singleton() = default;
    Singleton(const Singleton&) = delete;
    Singleton & operator=(const Singleton&) = delete;

private:
    static Singleton* instance;
};

#endif // SINGLETON_H
```

```cpp
/* 
 * singleton.cpp
 */
#include "singleton.h"

Singleton_lazy* Singleton::instance = nullptr;

Singleton* Singleton::getInstance() {
    if(instance == nullptr) {
        instance = new Singleton();
    }
    return instance;
}
```

### 2.2 懒汉+加锁 mutex（双重检查锁模式）

懒汉方式是线程不安全的，所以需要加保护措施。使用**双重检查锁**，可以较大限度减小锁的粒度。

双重检查锁的伪代码：
```cpp
Singleton* Singleton::getInstance() {
    // 双重检查锁
    if(instance == nullptr) {   // 第一次检查
        Lock lock
        if(instance == nullptr) {   // 第二次检查
            instance = new Singleton();
        }
    }
    return instance;
}
```

具体实现：
```cpp
/* 
 * singleton.h
 */
#ifndef SINGLETON_H
#define SINGLETON_H

#include <mutex>

class Singleton {
public:
    static Singleton * getInstance();

private:
    Singleton() = default;
    ~Singleton() = default;
    Singleton(const Singleton&) = delete;
    Singleton & operator=(const Singleton&) = delete;

private:
    static Singleton* instance;
    static std::mutex mu;
};

#endif // SINGLETON_H
```

```cpp
/* 
 * singleton.cpp
 */
#include "singleton.h"

Singleton* Singleton::instance = nullptr;
std::mutex Singleton::mu;

Singleton* Singleton::getInstance() {
    // 双重检查锁
    if(instance == nullptr) {
        std::lock_guard<std::mutex> guard(Singleton::mu);
        if(instance == nullptr) {
            instance = new Singleton();
        }
    }
    return instance;
}
```

### 2.3 饿汉

饿汉方式在最初就生成一个单例。

由于并发情况下只是简单的“读操作”，即返回该单例的指针，所以线程安全。

具体实现：

```cpp
/* 
 * singleton.h
 */
#ifndef SINGLETON_H
#define SINGLETON_H

class Singleton {
public:
    static Singleton * getInstance();

private:
    Singleton() = default;
    ~Singleton() = default;
    Singleton(const Singleton&) = delete;
    Singleton & operator=(const Singleton&) = delete;

private:
    static Singleton* instance;
};

#endif // SINGLETON_H
```

```cpp
/* 
 * singleton.cpp
 */
#include "singleton.h"

// 一开始就生成一个实例
Singleton* Singleton::instance = new Singleton();

Singleton* Singleton::getInstance() {
    return instance;
}
```

### 2.4 局部静态实例

在 C++11 后，在 getInstance() 内声明一个局部静态对象，则只会有着一个单例。并且，该静态对象会在程序结束时自动析构回收。

具体实现：

```cpp
/* 
 * SingleInstance.h
 */
class SingleInstance_local {
public:
    static SingleInstance_local & getInstance();

private:
    SingleInstance_local() = default;
    ~SingleInstance_local() = default;
    SingleInstance_local(const SingleInstance_local&) = delete;
    SingleInstance_local & operator=(const SingleInstance_local&) = delete;
};
```

```cpp
/*
 * SingleInstance.cpp
 */
SingleInstance_local & SingleInstance_local::getInstance() {
    // 局部静态变量
    static SingleInstance_local sl;
    return sl;
}
```

### 2.5 pthread_once

在 unix 平台的话，在不适用 C++11 的情况下，还可以通过 `pthread_once` 来实现 Singleton。

函数原型：`int pthread_once(pthread_once_t once_control, void (init_routine) (void));`

具体实现：

```cpp
class singleton {
public:
    singleton *instance() {
        // init函数只会执行一次
        pthread_once(&ponce_, &singleton::init);
        return p;
    }

private:
    singleton();
    singleton(const singleton &other);
 
    //要写成静态方法的原因：类成员函数隐含传递this指针（第一个参数）
    static void init() {
        instance = new singleton();
    }

private:
    static pthread_once_t ponce_;
    static singleton *instance;
```
