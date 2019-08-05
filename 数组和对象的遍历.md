# TechnicalDocumentation
技术相关文档整理

## JavaScript相关
### 针对JavaScrpt各种遍历作的总结和分析

* 1、普通for循环，经常用的数组遍历
```JavaScrpt
var arr = [1,2,0,3,9];
 for ( var i = 0; i <arr.length; i++){
    console.log(arr[i]);
}
```

* 2、优化版for循环:使用变量，将长度缓存起来，避免重复获取长度，数组很大时优化效果明显
```JavaScrpt
for(var j = 0,len = arr.length; j < len; j++){
    console.log(arr[j]);
}
```

* 3、forEach，ES5推出的,数组自带的循环，主要功能是遍历数组，实际性能比for还弱
```JavaScrpt
arr.forEach(function(value,i){
　　console.log('forEach遍历:'+i+'--'+value);

})
```
forEach这种方法也有一个小缺陷：你不能使用break语句中断循环，也不能使用return语句返回到外层函数。

* 4、map遍历，map即是 “映射”的意思 用法与 forEach 相似
```JavaScrpt
arr.map(function(value,index){
    console.log('map遍历:'+index+'--'+value);
});
```
map遍历支持使用return语句，支持return返回值
```JavaScrpt
var temp=arr.map(function(val,index){
  console.log(val);  
  return val*val           
})
console.log(temp);  
```
forEach、map都是ECMA5新增数组的方法，所以ie9以下的浏览器还不支持

* 5、for-of遍历 是ES6新增功能
```JavaScrpt
for( let i of arr){
    console.log(i);
}
```
for-of这个方法避开了for-in循环的所有缺陷
与forEach()不同的是，它可以正确响应break、continue和return语句 
for-of循环不仅支持数组，还支持大多数类数组对象，例如DOM NodeList对象。
for-of循环也支持字符串遍历

JS对象遍历：
* 1、for-in遍历
for-in是为遍历对象而设计的，不适用于遍历数组。
遍历数组的缺点：数组的下标index值是数字，for-in遍历的index值"0","1","2"等是字符串
```JavaScrpt
for (var index in arr){
    console.log(arr[index]);
    console.log(index);
}
```

### 数组的find、filter、forEach、map四种方法的总结

* find()：返回通过测试的数组的第一个元素的值
在第一次调用 callback 函数时会确定元素的索引范围，因此在 find 方法开始执行之后添加到数组的新元素将不会被 callback 函数访问到。如果数组中一个尚未被callback函数访问到的元素的值被callback函数所改变，那么当callback函数访问到它时，它的值是将是根据它在数组中的索引所访问到的当前值。被删除的元素仍旧会被访问到。
语法：
```JavaScrpt
array.find(function(value, index, arr),thisValue)
```
value:必须，代表当前元素;其他四个参数都是可选，index代表当前索引值，arr代表当前的数组，thisValue代表传递给函数的值，一般用this值，如果这个参数为空，undefined会传递给this值
返回值：返回符合测试条件的第一个数组元素的值，如果没有符合条件的则返回undefined。
```JavaScrpt
 var arr = [1,2,3,4,5,6,7];
 var ar = arr.find(function(elem){
     return elem>5;
 });
 console.log(ar);//6
 console.log(arr);//[1,2,3,4,5,6,7]
```
find()方法为数组中的每个元素都调用一次函数执行，当数组中的元素在测试条件时返回true，find()返回符合条件的元素，之后的值不会再执行函数。如果没有符合条件的元素则返回undefined。

* filter()：创建一个新数组，新数组中的元素是通过检查指定数组中符合条件的所有元素
filter 遍历的元素范围在第一次调用 callback 之前就已经确定了。在调用 filter 之后被添加到数组中的元素不会被 filter 遍历到。如果已经存在的元素被改变了，则他们传入 callback 的值是 filter 遍历到它们那一刻的值。被删除或从来未被赋值的元素不会被遍历到。
语法：
```JavaScrpt
array.filter(function(value, index, arr),thisValue)
```
value:必须，代表当前元素;其他四个参数都是可选，index代表当前索引值，arr代表当前的数组，thisValue代表传递给函数的值，一般用this值，如果这个参数为空，undefined会传递给this值
返回值：返回数组，包含了符合条件的所有元素，如果没有符合条件的则返回空数组
```JavaScrpt
 var arr = [1,2,3,4,5,6,7];
 var ar = arr.filter(function(elem){
     return elem>5;
 });
 console.log(ar);//[6,7]
 console.log(arr);//[1,2,3,4,5,6,7]
```

* map()：返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值，map()方法按照原始数组元素顺序依次处理元素
map方法会给原数组中的每个元素都按顺序调用一次callback函数，callback每次执行后的返回值（包括undefined）组合起来形成一个新数组。callback函数只会在有值的索引上被调用，那些从来没被赋过值或者使用delete删除的索引则不会被调用。
使用map方法处理数组时，数组元素的范围是在callback方法第一次调用之前就已经确定了。在map方法执行的过程中，原数组中新增加的元素将不会被callback访问到，若已经存在的元素被改变或删除了，则他们传递到callback的值是map方法遍历到他们的那一刻的值，而被删除的元素将不会被访问到。
语法：
```JavaScrpt
array.map(function(value, index, arr),thisValue)
```
value:必须，代表当前元素;其他四个参数都是可选，index代表当前索引值，arr代表当前的数组，thisValue代表传递给函数的值，一般用this值，如果这个参数为空，undefined会传递给this值
返回值：返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值
```JavaScrpt
 var arr = [1,2,3,4,5,6,7];
 var ar = arr.map(function(elem){
    return elem*4;
 });
 console.log(ar);//[4, 8, 12, 16, 20, 24, 28]
 console.log(arr);//[1,2,3,4,5,6,7]
```

* forEach()：用于调用数组每个元素，并将元素传递给回调函数（注意没有办法跳出或终止forEach语句，除非抛出异常）
forEach 遍历的范围在第一次调用 callback 前就会确定。调用forEach 后添加到数组中的项不会被 callback 访问到。如果已经存在的值被改变，则传递给 callback 的值是 forEach 遍历到他们那一刻的值。已删除的项不会被遍历到
语法：
```JavaScrpt
array.forEach(function(value, index, arr),thisValue)
```
value:必须，代表当前元素;其他四个参数都是可选，index代表当前索引值，arr代表当前的数组，thisValue代表传递给函数的值，一般用this值，如果这个参数为空，undefined会传递给this值
返回值：undefined
```JavaScrpt
 var arr = [1,2,3,4,5,6,7];
 var sum = 0;
 var ar = arr.forEach(function(elem){
    sum+=elem*4;
 });
 console.log(ar);//undefined
 console.log(arr);//[1,2,3,4,5,6,7]
 console.log(sum);//112
```
forEach()返回值为undefined，里面即便有return语句，返回值依然是undefined

总结如下：
> 从上面的内容我们可以看出，上面的四个语法以及参数的意义是一样的，而且都不会对空数组进行检测，也不会改变原始数组
> 现在说说各自的意义：
> * find()方法主要用来返回数组中符合条件的第一个元素（没有的话，返回undefined）；
> * filter()方法主要用来筛选数组中符合条件的所有元素，并且放在一个新数组中，如果没有，返回一个空数组；
> * map()方法主要用来对数组中的元素调用函数进行处理，并且把处理结果放在一个新数组中返回（如果没有返回值，新数组中的每一个元素都为undefined）；
> * forEach()方法也是用于对数组中的每一个元素执行一次回调函数，但它没有返回值（或者说它的返回值为undefined，即便我们在回调函数中写了return语句，返回值依然为undefined）；
