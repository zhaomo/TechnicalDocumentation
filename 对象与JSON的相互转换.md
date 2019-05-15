# json对象和字符串的相互转换
## 推荐的转换方法
在Firefox，chrome，opera，safari，ie9，ie8等高级浏览器直接可以用JSON对象的stringify()和parse()方法。
```JavaScript
//使用json中的parse方法转换；
var str='{"name":"fendouer", "age":23}';      //这是一个json字符串''
var ob=JSON.parse(str) ;  //返回一个新对象
console.log(ob.name)

//把json中的stringify对象转换成字符串 
var obj={"student":[{"name":"cyl","age":"21"},{"name":"hyj","age":"23"}]};      //这是一个json对象
var str=obj.student[0].name;
var newstr=JSON.stringify(str); //返回一个新字符串
console.log(newstr);
```

JSON.stringify(obj)       将JSON对象转为字符串。<br />
JSON.parse(string)       将字符串转为JSON对象格式。
## 其他的转换方法
* 使用jQuery插件将字符串转换为对象<br />
$.parseJSON( jsonstr )      将字符串转为JSON对象格式。
jQuery3.0以后被弃用，不建议使用
* JSON官方的转换方式<br />
[JSON官网] (http://www.json.org) 提供了一个json2.js。
该文件使ie8(兼容模式),ie7和ie6可以支持JSON对象以及其stringify()和parse()方法； 
请见本仓库json2.js。
