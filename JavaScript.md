# JavaScript

## 同步异步

### Promise

**es6 新增 引用类型**

**三种状态**

- pending ( 待定 )
- fulfilled ( 兑现 )
- reject ( 拒绝 )

**使用 new 创建的 promise  都需要传入一个执行器函数 作为参数, 该函数同步执行**

**Promise静态方法:**

- .resolve()  

  幂等方法 , 传入Promise , 相当于空包装, 保留Promise 状态

- .reject()

  不幂等

**Primise实例方法:**

(ES 规范的 异步结构 , 都实现了Thenable 接口, 即都有一个then() 方法)

- .then()

  添加处理程序 主要方法

  两个可选参数 onResolved() 和 onRejected()

  **返回新promise实例** ( 基于onResolved() 的返回值构建 )

- .catch()

  语法糖, 相当于 .then(null, onRejected)

  一个参数 onreject处理程序的值

  **返回新Promise实例**

- .finally()

  **返回新Promise实例**

  大多数情况下 , 表现为 父promise 的传递 , 若返回一个待定的promise

#### ES Promise 未具备的特性

- promise 取消

  cancel token  实例化取消令牌,  在返回 resolve 前. 传进函数, 提前resolve 或 reject

## Class

**des : ** ES6 新 基础性语法糖结构 ( 原型 和 构造函数 )

**特点 : **

- 类定义 不具备 声明提升( class Xxx {})
- 受块作用限制

**构成 :**

- 构造函数方法

- 实例方法

  定义在类的原型对象上

- 获取函数

- 设置函数

- 静态类方法

  定义在类本身上

**使用new :**

- 内存中创建新对象
- 新对象内部的[[prototype]] 指针 被赋值为构造函数的 prototype 属性
- 构造函数内部的this 被赋值为这个新对象
- 执行构造函数内部的代码 
- 如果构造函数 返回 非空对象 , 则返回该对象 , 否则, 返回刚创建的新对象

**原型方法 :** 类 块中 定义的方法

**支持迭代器 与 生成器 方法**

( 添加默认的迭代器, 把类实例 变成可迭代对象 )

```js
class Xxx() {
    *[Symbol.iterator] () {
        yield *this.nicknames.entries()
    }
}
```

### 继承

**des : ** extends 关键字, 可以继承任何拥有[[Construct]]  和 原型 的对象

- 通过 **super** 关键字 引用他们的原型(仅派生类使用, 且只在类构造函数, 实例方法, 静态方法内部)

**[[HomeObject]]** : 内部特性, 一个指向定义该方法的对象的指针, 是自动赋值, 且只能在js引擎内部访问, **super** 始终定义为 **[[HomeObject]]** 的原型

#### 抽象基类

**des : ** 供其他类继承, 但本身不被实例化, 通过 **new.target** 实现

**new.target** : 保存 通过 new 关键字 调用的 类 或 函数, 通过实例化时, 检测 new.target 是否 抽象基类, 组织对抽象基类的实例化