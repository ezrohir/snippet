### 数值
####　NaN
NaN是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合.
```
typeof Nan  //'number'
isNan(Nan)  // true
isNan(123)  // false
isNan('hello')  // true

func myIsNan(value) {
  return typeof value === 'number' && isNan(value)
}
```

#### 与数值相关的全局方法
```
parseInt('123')   // 123
parseInt('abc')   // NaN
parseInt('1000',2) // 8
```


### 字符串
btoa()：字符串或二进制值转为Base64编码
atob()：Base64编码转为原来的编码

### 对象
#### Object对象的静态方法
所谓静态方法,是指部署在 Object 对象自身的方法.
如 Object.keys 方法 Object.getOwnPropertynames 方法.

#### Object对象的实例方法
除了 Object 对象本身的方法,还有不少方法是部署在 Object.prototype 对象上的, 所有 Objcet 的实例 对象都继承了这些方法 .

#### 构造函数与new命令
构造函数的写法就是一个普通的函数，但是有自己的特征和用法。构造函数名字的第一个字母通常大写。
```
var Vehicle = function () {
  this.price = 1000;
};
```
+ 函数体内部使用了this关键字，代表了所要生成的对象实例。
+ 生成对象的时候，必需用new命令，调用Vehicle函数。

#### new命令的原理
1. 创建一个空对象，作为将要返回的对象实例
2. 将这个空对象的原型，指向构造函数的prototype属性
3. 将这个空对象赋值给函数内部的this关键字
4. 开始执行构造函数内部的代码
```
function _new(/* 构造函数 */ constructor, /* 构造函数参数 */ param1) {
  // 将 arguments 对象转为数组
  var args = [].slice.call(arguments);
  // 取出构造函数
  var constructor = args.shift();
  // 创建一个空对象，继承构造函数的 prototype 属性
  var context = Object.create(constructor.prototype);
  // 执行构造函数
  var result = constructor.apply(context, args);
  // 如果返回结果是对象，就直接返回，否则返回 context 对象
  return (typeof result === 'object' && result != null) ? result : context;
}

// 实例
var actor = _new(Person, '张三', 28);
```

#### 使用 Object.create() 创见实例对象
构造函数作为模板，可以生成实例对象。但是，有时只能拿到实例对象，而该对象根本就不是由构造函数生成的，这时可以使用Object.create()方法，直接以某个实例对象作为模板，生成一个新的实例对象。
```
var person1 = {
  name: '张三',
  age: 38,
  greeting: function() {
    console.log('Hi! I\'m ' + this.name + '.');
  }
};

var person2 = Object.create(person1);

person2.name // 张三
person2.greeting() // Hi! I'm 张三.
```



### prototype 对象
原型对象的作用，就是定义所有实例对象共享的属性和方法。

“原型链”的作用是，读取对象的某个属性时，JavaScript 引擎先寻找对象本身的属性，如果找不到，就到它的原型去找，如果还是找不到，就到原型的原型去找。如果直到最顶层的Object.prototype还是找不到，则返回undefined。

如果对象自身和它的原型，都定义了一个同名属性，那么优先读取对象自身的属性，这叫做“覆盖”（overriding）。
