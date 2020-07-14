### Undefined/Null
- 这两个类型的值都是只有一个值，前者唯一值是`undefined` 后者唯一值是 `null`;
- undefined 不是JavaScript 的关键字,是全局变量，表示**未定义**可以被篡改，用 void 0 代替;
- null 是JavaScript 的关键字,是全局变量，表示**值为空**;


### Boolean
- Boolean 类型有两个值，true和false，表示逻辑上的真和假；

### String
- string 有最大长度 `2^53 - 1`，这里的长度是字符的长度；因为 String 的意义并非“字符串”，而是字符串的 UTF16 编码，我们字符串的操作 charAt、charCodeAt、length 等方法针对的都是 UTF16 编码。所以，字符串的最大长度，实际上是受字符串的编码长度影响的。

### Number 
- `number` 的范围是 `2^64-2^53+3` 个值；
- `NaN`，占用了 `9007199254740990`，这原本是符合 IEEE 规则的数字；`Infinity`，无穷大；`-Infinity`，负无穷大；
- `Number.EPSILON` 是浮点运算精度的最小精度；

### Symbol
- 为一值，可以用Symbol.for()，判断其来源字符串；

### Object 
- 对象有两种属性：数据属性 和 访问器属性
> 数据属性： value：就是属性的值；writable：决定属性能否被赋值；enumerable：决定 for in 能否枚举该属性；configurable：决定该属性能否被删除或者改变特征值；
> 访问器属性：getter：函数或 undefined，在取属性值时被调用；setter：函数或 undefined，在设置属性值时被调用；enumerable：决定 for in 能否枚举该属性；configurable：决定该属性能否被删除或者改变特征值；
- 我们通常用于定义属性的代码会产生数据属性，其中的 writable、enumerable、configurable 都默认为 true。我们可以使用内置函数 getOwnPropertyDescripter 来查看，如以下代码所示：
```javascript
    var o = { a: 1 };
    o.b = 2;
    //a和b皆为数据属性
    Object.getOwnPropertyDescriptor(o,"a") // {value: 1, writable: true, enumerable: true, configurable: true}
    Object.getOwnPropertyDescriptor(o,"b") // {value: 2, writable: true, enumerable: true, configurable: true}
```
- 如果我们要想改变属性的特征，或者定义访问器属性，我们可以使用 Object.defineProperty，示例如下: 
```javascript
    var o = { a: 1 };
    Object.defineProperty(o, "b", {value: 2, writable: false, enumerable: false, configurable: true});
    //a和b都是数据属性，但特征值变化了
    Object.getOwnPropertyDescriptor(o,"a"); // {value: 1, writable: true, enumerable: true, configurable: true}
    Object.getOwnPropertyDescriptor(o,"b"); // {value: 2, writable: false, enumerable: false, configurable: true}
    o.b = 3;
    console.log(o.b); // 2
```