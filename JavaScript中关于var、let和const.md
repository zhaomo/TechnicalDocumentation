###变量声明和初始化

在比较它们的区别之前，我们先来看一下变量声明和初始化。变量声明：
```javascript
var declaration
```
变量声明会引入了一个新的标识符 declaration，在 JavaScript 中，新创建的变量的默认值都是 undefined。我们再来看一下变量赋值：
```javascript
var declaration
console.log(declaration)  //undefined
declaration = 'this is an initialization.'
```
declaration 变量现在被我们赋予了一个值。

###作用域

JavaScript 的世界共有两种作用域：全局作用域和方法作用域。使用 var 声明的变量的作用域是方法作用域，如下 date 变量在方法外面不可访问的：
```javascript
Function getDate() {
  var date = new Date(); //date变量在函数getDate()外不可访问
  return date
}

getDate();
console.log(date) //ReferenceError: date is undefined
```
看起来蛮正常的。var 变量关键字的真正问题在于其在方法内部的定义变量开始的任何地方都可以访问到这个变量。如下所示，i、discountedPrice、finalPrice 这三个变量是定义在一个 for 循环体中的 (即位于块作用域中)，按照正常思维来讲，在循环结束后，这三个变量是不可访问的，但是现在在这个整个大的方法中，依然是可以访问的：
```javascript
Function discountPrices(prices, discount) {
  var discounted = [];
  
  for(var i = 0, i < prices.length, i++) {
    var discountedPrice = prices[i] * (1 - discount);
    var finalPrice = Math.round(discountedPrice * 100) / 100;
    discounted.push(finalPrice);
  }
  
  console.log(i)  //3
  console.log(discountedPrice)  //150
  console.log(finalPrice)  //150
  
  return discounted
}
```

###var 和 let 对比

var 和 let 第一点不同就是 let 是块作用域，即其在整个大括号 {} 之内可见。如果使用 let 来重写上面的 for 循环的话，会报错：
```javascript
Function discountPrices(prices, discount) {
  let discounted = [];
  
  for(let i = 0, i < prices.length, i++) {
    let discountedPrice = prices[i] * (1 - discount);
    let finalPrice = Math.round(discountedPrice * 100) / 100;
    discounted.push(finalPrice);
  }
  
  console.log(i)  //ReferenceError: i is undefined
  console.log(discountedPrice)  //ReferenceError: discountedPrice is undefined
  console.log(finalPrice)  //ReferenceError: finalPrice is undefined
  
  return discounted
}
```
let 和 var 的第二点不同是，在变量声明之前就访问变量的话，会直接提示 ReferenceError，而不像 var 那样使用默认值 undefined:
```javascript
Function discountPrices(prices, discount) {
  console.log(discounted)  //ReferenceError: discounted is undefined
  let discounted = [];
  
  for(let i = 0, i < prices.length, i++) {
    let discountedPrice = prices[i] * (1 - discount);
    let finalPrice = Math.round(discountedPrice * 100) / 100;
    discounted.push(finalPrice);
  }
  
  console.log(i)  //ReferenceError: i is undefined
  console.log(discountedPrice)  //ReferenceError: discountedPrice is undefined
  console.log(finalPrice)  //ReferenceError: finalPrice is undefined
  
  return discounted
}
```

###let 和 const 对比

const 和 let 的作用域是一致的，不同的是 const 变量一旦被赋值，就不能再改变了：
```javascript
let name1 = 'luis';
const name2 = 'luis';

name1 = 'luis enrique';
name2 = 'luis enrique';  //TypeError: Assignment to constant variable
```
但是这并不意味着使用 const 声明的变量本身不可变，只是说它不可被再次赋值了：
```javascript
const person = {
  name = 'luis'
}

person.name = 'luis enrique'  //依然可以改名
person = {}  //TypeError: Assignment to constant variable
```

###使用场景

我们已经讲解了它们的主要不同，但是什么时候用 var、let 或 const 呢？我的建议是，大多数情况下都使用 const，除非你知道你的变量的值还会被改变，这样的话，别人阅读你的代码不用老想着这个变量的值会不会有改变。如果这个变量的值的确需要改变，例如在 for 循环里面，那么就是用 let。这也同时意味着你以后就不要用 var 了。

关于 const 的使用，一些程序员还倾向于只用来声明常量，其它情况下一律使用 let 关键字，我觉得这样也是可行的。
