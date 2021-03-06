# javascript运算符及优先级

> JavaScript中运算符主要用于连接简单表达式，组成一个复杂的表达式。常见的有算数表达式、比较表达式、逻辑表达式、赋值表达式等，也有单目运算符，指操作原始表达式。

有些操作符对不同的数据类型有不同的含义，比如 `+`

- 在两个操作数都是数字的时候，会做加法运算
- 两个参数都是字符串或在有一个参数是字符串的情况下会把另外一个参数转换为字符串做字符串拼接
- 在参数有对象的情况下会调用其valueOf或toString
- 在只有一个字符串参数的时候会尝试将其转换为数字
- 在只有一个数字参数的时候返回其正数值

## 运算符类型

### 算数运算符

- 减法运算符（Subtraction）： x - y
- 乘法运算符（Multiplication）： x * y
- 除法运算符（Division）：x / y
- 余数运算符（Remainder）：x % y
- 自增运算符（Increment）：++x 或者 x++
- 自减运算符（Decrement）：--x 或者 x--
- 求负运算符（Negate）：-x
- 数值运算符（Convert to number）： +x

### 赋值运算符

赋值运算符用于给变量赋值，最常见的赋值运算符，当然就是等号，表达式x=y表示将y赋值给x。除此之外，JavaScript还提供其他11个赋值运算符。

- x += y // 等同于 x = x + y
- x -= y // 等同于 x = x - y
- x *= y // 等同于 x = x * y
- x /= y // 等同于 x = x / y
- x %= y // 等同于 x = x % y
- x >>= y // 等同于 x = x >> y
- x <<= y // 等同于 x = x << y
- x >>>= y // 等同于 x = x >>> y
- x &= y // 等同于 x = x & y
- x |= y // 等同于 x = x | y
- x ^= y // 等同于 x = x ^ y

### 比较运算符

比较运算符比较两个值，然后返回一个布尔值，表示是否满足比较条件。JavaScript提供了8个比较运算符。

- == 相等
- === 严格相等
- !=不相等
- !== 严格不相等
- < 小于
- <= 小于或等于
- > 大于
- >= 大于或等于

### 布尔运算符

- ! 取反运算符
- && 且运算符
- || 或运算符
- condition? true case : false case 三元条件运算符

### 位运算符

- 或运算（or）：符号为|，表示两个二进制位中有一个为1，则结果为1，否则为0。
- 与运算（and）：符号为&，表示两个二进制位都为1，则结果为1，否则为0。
- 否运算（not）：符号为～，表示将一个二进制位变成相反值。
- 异或运算（xor）：符号为ˆ，表示两个二进制位中有且仅有一个为1时，结果为1，否则为0。
- 左移运算（left shift）：符号为<<
- 右移运算（right shift）：符号为>>
- 带符号位的右移运算（zero filled right shift）：符号为>>>

### 其他

#### 小括号

在JavaScript中，圆括号是一种运算符，它有两种用法：如果把表达式放在圆括号之中，作用是求值；如果跟在函数的后面，作用是调用函数。

把表达式放在圆括号之中，将返回表达式的值。
#### void

void运算符的作用是执行一个表达式，然后返回undefined。

#### 逗号运算符

逗号运算符用于对两个表达式求值，并返回后一个表达式的值。

## 运算符优先级与结合性

1. typeof的优先级相当的高，比加减乘除神马的都高，所以虽然是操作符，在在复杂表达式的时候我们还是习惯加括号，看个例子

```JavaScript
    typeof 2*3;//NaN
    typeof (2*3);//"number"
    typeof 2+3;// "number3"
```

2. ++、--是右结合的操作符（优先级最高的几个都是右结合），而且比加减乘除优先级高。同时自增、自减运算符的运算数得是左值（可以放在赋值符号左边的值），而不能是常数
```JavaScript
    4++; //ReferenceError: Invalid left-hand side expression in postfix operation
    var a=0,b=0;
    a+++b;//0
    a;//1，++优先级比+高，所以相当于(a++)+b
    b;//0
```
3. 赋值运算符的优先级相当的低

```JavaScript
a = b == c; //等同于a = (b==c)
```

4. 逻辑非`!`也在优先级队列的前端，比加减乘除高，但逻辑与、逻辑或优先级很低，不如加减乘除
```JavaScript
    !2*0; //0, 等价于(!2)*0
```

5. 一个关于逻辑运算符的有意思地方是其“短路”功能，相信大家都有所了解，但有些题目不那么单纯，会结合表达式计算值来考察

```JavaScript
    1 && 3;
    1 && "foo" || 0;
    1 || "foo" && 0；
```

## 相等

我们知道可以使用==或===判断两个值的相等性，其中区别相信大家清楚，===是严格意义的相等，只需注意NaN和NaN不等就行了。而使用==的时候，javascript会帮我们做类型转换，造成一些匪夷所思的结果，那么使用==的时候会在哪些情况下做类型转换，又会换成什么样子？


- 如果两个值类型相同，则执行严格相等的运算
- 如果两个值的类型不同
    - 如果一个是null，一个是undefined，那么相等
    - 如果一个是数字，一个是字符串，先将字符串转为数字，然后比较
    - 如果一个值是true/false则将其转为1/0比较
    - 如果一个值是对象，一个是数字或字符串，则尝试使用valueOf和toString转换后比较
    - 其它就不相等了