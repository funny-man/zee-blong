# ES6--->class

---

## 类的声明

> 定义一个类的一种方法是使用一个类声明。要声明一个类，你可以使用带有class关键字的类名（这里是“Rectangle”）。

    class Component {
      constructor(height, width) {
        this.height = height;
        this.width = width;
      }
    }

函数声明和类声明之间的一个重要区别是函数声明会提升，类声明不会。你首先需要声明你的类，然后访问它

    let p = new Rectangle(); 
    // ReferenceError

    class Rectangle {}


## 类表达式
>一个类表达式是定义一个类的另一种方式。类表达式可以是被命名的或匿名的。赋予一个命名类表达式的名称是类的主体的本地名称。

  /* 匿名类 */ 
  let Rectangle = class {
    constructor(height, width) {
      this.height = height;
      this.width = width;
    }
  };

  /* 命名的类 */ 
  let Rectangle = class Rectangle {
    constructor(height, width) {
      this.height = height;
      this.width = width;
    }
  };


注意: 类表达式也同样受到类声明中提到的提升问题的困扰。

----

## constructor

> constructor方法是一个特殊的方法，其用于创建和初始化使用class创建的一个对象。一个类只能拥有一个名为 “constructor”的特殊方法。如果类包含多个constructor的方法，则将抛出 一个SyntaxError 。

一个构造函数可以使用 super 关键字来调用一个父类的构造函数。(通过extends创造的子类构造函数里面调用父类的方法看下面例子)

## 先将extends

> extends 关键字在类声明或类表达式中用于创建一个类作为另一个类的一个子类。

    // 从extends类的继承开始
    class Cat { 
      constructor(name) {
        this.name = name;
      }
      speak() {
        console.log(this.name + ' makes a noise.');
      }
    }
    class Lion extends Cat {
      say() {
        console.log(this.name + ' roars.');
      }
    }
    var lion = new Lion('NANA')
    lion.say() // NANA roars.
    lion.speak() // NANA makes a noise.

从上面可以看出new一个子类Lion，当子类中用方法say就调用子类的方法，当子类中没有speak方法则去父类中查找这就是ES6中的继承，这比ES5的通过修改原型链实现继承方便多了；

    class Cat { 
      constructor(name) {
        this.name = name;
      }
      speak() {
        console.log(this.name + ' makes a noise.');
      }
    }
    class Lion extends Cat {
      speak() {
        console.log(this.name + ' roars.');
      }
    }
    var lion = new Lion('NANA')
    lion.speak() // NANA roars.

显然上面那样子类就用不到父类的方法了，应为被覆盖了
这时候super就派上用场了

## super
> 既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。


**作为函数**

如果子类里有constructor构造函数则必先写super()如下代码

    class Cat { 
      constructor(x,y) {
        this.x = x;
        this.y = y;
      }
    }
    class Lion extends Cat {
      constructor(x, y, name) {
        // 只有调用super之后，才可以使用this关键字
        this.name = name; // 报错
        super(x, y); // 调用父类的constructor(x, y)
        this.name = name; // 正常
      }
    }

> 子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类自己的this对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。如果不调用super方法，子类就得不到this对象。

而且 super作为函数使用super()必须放在constructor构造函数里，放在子类其他的方法里调用都会报错

**作为对象**
> 作为对象 super 关键字用于调用对象的父对象上的函数。

这里我们的需求是要在子类调用speak()同时也能调用父类的speak()

    class Cat { 
      constructor(name) {
        this.name = name;
      }
      speak() {
        console.log(this.name + ' makes a noise.');
      }
    }
    class Lion extends Cat {
      speak() {
        super.speak(); // 调用父类的speak()方法
        console.log(this.name + ' roars.');
      }
    }

    var lion = new Lion('NANA')
    lion.speak() 
    // NANA makes a noise.
    // NANA roars.

同时打印出两个结果说明子类父类的speak() 都执行了

这里需要注意，由于super指向父类的原型对象，所以定义在父类实例上的方法或属性，是无法通过super调用的。

    class Cat {
      constructor() {
        this.x = 2;
      }
    }

    class Lion extends Cat {
      get m() {
        return super.x;
      }
    }

    let lion = new Lion();
    lion.m // undefined

上面代码中，x是父类Cat实例的属性，super.x就引用不到它。

ES6 规定，在子类普通方法中通过super调用父类的方法时，方法内部的this指向当前的子类实例。

    class A {
      constructor() {
        this.x = 1;
      }
      print() {
        console.log(this.x);
      }
    }

    class B extends A {
      constructor() {
        super();
        this.x = 2;
      }
      m() {
        super.print();
      }
    }

    let b = new B();
    b.m() // 2




    ---->待续