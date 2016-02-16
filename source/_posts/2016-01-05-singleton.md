title: 我犯的错误：有关singleton
date: 2016-01-05 22:14:21
categories: 编程错误
tags: [singleton]
---

## 错误想法：

在我的ClassFactory的代码当中，用来实现singleton的代码是这样的：
```
#ifndef MQPOOL_INCLUDE_CLASS_FACTORY_H_
#define MQPOOL_INCLUDE_CLASS_FACTORY_H_

......

class ClassFactory : public Object {
 public:
  ClassFactory();
  ......
 
};

inline ClassFactory& ClassFactoryInstance() {
  static ClassFactory sInstance;
  return sInstance;
}

......

#endif /* MQPOOL_INCLUDE_CLASSS_FACTORY_H_ */
```

因为我看[《Effective C++》](http://book.douban.com/subject/1842426/)的条款4的实现：
```
class FileSystem { ... }  
FileSystem &tfs() {                        // 这个函数用来替换tfs对象  
  static FileSystem fs;  
  return fs;  
}  
```
使用`static`的`local-static`变量,只有在`Instance()`函数被调用的时候才会创建，从而有了延迟初始化的效果，提高了程序的启动性能。
并且Meyers还说了："这样的单纯性使它们成为绝佳的inlining候选人.尤其是如果它们被频繁调用的话"，所以想当然的，我的实现就成了上面的那个样子。但其实大错特错。

## 构造函数不应该为public
错误的原因就是构造函数不应该为`public`，将一个要作为`singleton`的对象的构造函数声明为`public`的话，那就意味着用户的代码能够随意构建一个`ClassFactory`类型的对象，这就违背了`singleton`的单一对象原则。特意将`static`对象返回的目的----达到实例有且仅有一个的要求，就变得没有任何意义。这样就违反了条款18：让接口容易被正确使用，不易被误用。

那么应该选择`protected`还是`private`呢？
我觉得为了继承的考虑，应该选择`protected`，因为如果将构造函数声明为`private`，那么这个`ClassFactory`的派生类当中的函数也将不能访问这个构造函数，那么当需要构造一个派生类的对象的时候，将不能成功，因为不能调用基类的构造函数，这对派生类的使用场景有很大的限制。

以下是我的实现：
```
#ifndef MQUEUE_INCLUDE_CLASS_FACTORY_H_
#define MQUEUE_INCLUDE_CLASS_FACTORY_H_

class ClassFactory : public Object {
 public:
  //因为是singleton模式，所以这里不能够让用户随意创建一个ClassFacotory，所以构造函数应该放在private当中去
  //只有static ClassFactory &Instance()能调用构造函数

  static ClassFactory &Instance();
  ......
 protected:
  ClassFactory();

};

#endif /* MQUEUE_INCLUDE_CLASSS_FACTORY_H_ */

```

```
ClassFactory& ClassFactory::Instance() {
  static ClassFactory sInstance;
  return sInstance;
}
```

完整代码在这里：[https://github.com/adairjun/MQueue/blob/master/include/MQueue/class_factory.h](https://github.com/adairjun/MQueue/blob/master/include/MQueue/class_factory.h)

## `non-member function`的`singleton`
首先继续明确这一点：就是我的`inline`的`non-member function`形式的`singleton`错误的根本在什么地方。上面也说了，是因为构造函数是`public`的情况，但是考虑这样的一种情况，如果我的`singleton`对象并不是我自己定义的类，而是`STL`当中的呢？比如说一个`map`，这个时候我们对于不是自己能够掌控的对象当然是不能把它的构造函数放在`protected`当中去了。
所以我只能这样做：

```
typedef std::map<std::string, int> KeyValue; 
inline KeyValue& GlobalKeyValue()
{
    static KeyValue themap;
    return themap;
}
```
这样一来，这个`singleton`那就不应该开放给用户，只是用在自己的代码里面，而且应该把它的使用场景严格限制，比如说把它封装在一两个函数当中，以后不显示调用它，而是通过函数来使用它。
比如：
```
inline void AddToKeyValue(std::string key, int value)
{
    KeyValue &themap = GlobalKeyValue();
    if(themap.count(key))
    {
        //TODO log
    }
    themap[key] = value;
}
inline int GetKeyValue(std::string key)
{
    KeyValue &themap = GlobalKeyValue();
    if(themap.count(key))
    {
        return themap[key];
    }
    else
    {
        //TODO log
        return -1;
    }
}
```
我的意思是以后仅仅只通过`AddToKeyValue`和`GetKeyValue`这两个函数来调用`GlobalKeyValue()`,除此之外绝对不在代码中出现`GlobalKeyValue()`。


## 继续讨论一下`singleton`的重用方案。
其实要把这个`ClassFactory`标记为`singleton`并不需要直接把`singleton`的代码写进去，只要自己实现一个`singleton`的抽象类，然后让`ClassFactory`继承它就可以了，以后只要用到`singleton`的地方只需要继承这个抽象类就可以了。

可以直接用模板写成这种形式：
```
template<typename T>
class Singleton {
 public:
  Singleton(const Singleton&) = delete;
  Singleton& operator=(const Singleton&) = delete;
  virtual ~Singleton();
  
  static T& Instance() {
    static T sInstance;
    return sInstance;
  }
  
 protected:
  Singleton() {};
};
```

那么我使用`ClassFactory`的方法就是：
```
class ClassFactory : public Object, public Singleton<ClassFactory> {
 ......
}；
```

这样一来我的代码就变成了多重继承，而Meyers在[《Effective C++》](http://book.douban.com/subject/1842426/)的条款40：“明智而审慎地使用多重继承”。侯捷老师的翻译很贴切，我觉得Meyers每次说道“明智而审慎地使用”，他的意思就是能不用就不用。我还是按照他说的去做吧，在这里我仅仅只是做个实现，真正要用的话，我还是不会去使用多重继承的。










