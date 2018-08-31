
#### javascript 的七种基本数据类型
六种基本数据类型

- `undefined`
- `null`
- `string`
- `boolean`
- `number`
- `symbol(ES6)`

一种引用类型
- `Object`

###   symbol(ES6) 
##### 六种基本数据类型还不够？为什么要引入 Symbel?

es5的对象属性名是字符串，容易造成属性名的冲突，如果有一种机制，保证每个属性的名字都是独一无二的，就可以从根本上防止属性名的冲突。
##### Symbel怎么生成？
`symbol`值通过`Symbol`函数生成，生成的`Symbol`是一个类似于字符串的原始类型的值。
```
const sym = Symbol(param)；
// param 可以为字符串或者对象
```
知识点：
1. 使用`new`命令会报错，这是因为生成的 `Symbol`是一个原始类型的值，不是对象，不能添加属性。
2. 如果传入的参数为对象，会调用`toString`方法，再转为字符串；传入的参数相同，`Symbol`的返回值也是不相等的。
##### Symbel值作为对象属性名时，怎样使用？
```
let mySymbol = Symbol();

// 第一种写法
let a = {};
a[mySymbol] = 'Hello!';

// 第二种写法
let a = {
  [mySymbol]: 'Hello!'
};

// 第三种写法
let a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

// 以上写法都得到同样结果
a[mySymbol] // "Hello!"
```
注意：
1. Symbol()函数，如果传入的参数为对象，会调用toString方法，再转为字符串；传入的参数相同，Symbol的返回值也是不相等的。
2. Symbol的值不能与其他的值进行运算，Symbol可以显式的转为字符串、布尔值，但不能转为数值。
3. Symbol每一个都是不相等的，意味着可以作为标识符，用于对象的属性名，能保证不会出现同名的属性，注意作为属性名时不能使用点运算符。
##### 内置的 Symbol 值
### Symbol.hasInstance
对象的Symbol.hasInstance属性，指向一个内部方法。当其他对象使用instanceof运算符，判断是否为该对象的实例时，会调用这个方法。比如， `foo instanceof Foo`在语言内部，实际调用的是`Foo[Symbol.hasInstance](foo)`。