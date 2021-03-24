### ES6教程

兼容性 ES6（ES2015）  IE10+、Chrome、FireFox、移动端、NodeJs

#### catalog

- [变量](####**变量**)

- [数据类型](####**数据类型**)
- [箭头函数](####**箭头函数**)
- [函数的参数](####**函数的参数**)
- [解构赋值](####**解构赋值**)
- [数组](####**数组**)
- [字符串](####**字符串**)
- [面向对象](####**面向对象**)
- 面向对象-应用 React
- JSON
- Promise （同步异步问题）
- async / await （同步异步问题）
- generator
- ES7预览
- babel.js编译
- 模块



#### **变量**

var

1. 可以重复声明同一个变量
2. 无法限制修改
3. 没有块级作用域，只有函数作用域

不初始化的情况下，变量会保存一个特殊值$undefined$

初始化变量不会将它标识类型，只是一个简单的赋值



**let        不能重复声明  变量-可以修改  块级作用域**

使用let在全局作用域中声明的变量不会成为window对象的属性

**const   不能重复声明  常量-不能修改  块级作用域**

声明的同时必须初始化变量，且尝试修改const声明的变量会导致运行时的错误

const声明的限制值适用于它指向的变量的引用（如果const变量引用的是一个对象，那么修改这个对象内部的属性并不违反const的限制）

```javascript
const person = {};
person.name = 'Matt';
console.log(person);

{ name: 'Matt' }

------------------------------------------------------------

for (const key in {a : 1, b : 2}) {
  console.log(key);
}

a
b

------------------------------------------------------------

for (const value of [1, 2, 3, 4, 5]) {
  console.log(value);
}

1
2
3
4
5

```



#### **数据类型**

- typeof操作符用来查看数据的类型

```javascript
console.log(typeof("1231"));  // string
console.log(typeof(23));  // number
console.log(typeof({a: 1, b: 12}));  // object
```



1. **Undefined 类型**：使用var或let声明变量但是还未初始化时，默认赋值undefined

2. **Null 类型**：表示一个空对象指针（定义将来要保存对象值的变量时，建议使用null来初始化）

```javascript
let message = null;
console.log(message);  // null
console.log(!message);  // true
let age;
console.log(age);  // undefined
console.log(!age);  // true
```

3. **Boolean 类型**：true不等于1，false不等于0

True和False是有效的标识符，不是布尔值

其他所有ECMAScript类型的值都有相应的布尔值等价形式（if等流控制语句会自动执行其他类型值到布尔值的转换）

```javascript
console.log(Boolean("hello"));  // true
console.log(Boolean(""));  // false
```

4. **Number 类型**：

```javascript
console.log(0o70);  // ES6中的八进制数表示56
console.log(0x1f);  // ES6中的十六进制数表示31
```

- 浮点值：精确度高达17位小数，但算术计算中远不如整数准确（存在微小的舍入错误，很难测试特定的浮点值）

```javascript
let floatNum1 = 1.1;  // 有效
let floatNum2 = .1;  // 有效但不推荐
let floatNum3 = 1.;  // 小数点后无数字 看成整数1处理
let floatNum4 = 10.0;  // 小数点后是0 看成整数10处理
console.log(3.125e7);  // 科学计数法 31250000
```

- 值的范围：最小值（Number.MIN_VALUE） 最大值（Number.MAX_VALUE）

任何无法表示的负数用-Infinity或Number.NEGATIVE_INFINITY表示，任何无法表示的正数用Infinity或Number.POSITIVE_INFINITY表示（用isFinite()函数判断一个值是否有限大）

- NaN：不是数值（Not A Number）

任何涉及NaN的操作始终返回NaN，NaN不等于包括NaN在内的任何值。

```javascript
console.log(isNaN(NaN));  // true
console.log(isNaN(10));  // false 10
console.log(isNaN("10"));  // false 10
console.log(isNaN("blue"));  // true
console.log(isNaN(true));  // false 1
```

- 数值转换：

  - Number() 

  ```javascript
  console.log(Number("hello world"));  // NaN
  console.log(Number(""));  // 0
  console.log(Number("000011"));  // 11
  console.log(Number(true));  // 1
  ```

  - parseInt() 更专注于字符串是否包含数值模式。可以接收第二个参数用于指定进制数，可以省略前缀。

  ```javascript
  console.log(parseInt("1234Float"));  // 1234
  console.log(parseInt(""));  // NaN
  console.log(parseInt("0xA"));  // 10
  console.log(parseInt(22.5));  // 22
  console.log(parseInt("70"));  // 70
  console.log(parseInt("0xf"));  // 15
  ```

  - parseFloat() 第一个出现的小数点有效，第二次出现会被忽略。始终忽略字符串开头的0。只能解析十进制。

  ```javascript
  console.log(parseFloat("1234blue"));  // 1234
  console.log(parseFloat("0xA"));  // 0 只能识别十进制
  console.log(parseFloat("22.5"));  // 22.5
  console.log(parseFloat("22.34.5"));  // 22.34
  console.log(parseFloat("0908.5"));  // 908.5
  console.log(parseFloat("3.125e7"));  // 31250000
  ```

5. **String 类型**：字符串可以用(“)、(')、(`)来标示。

- 字符字面量（\n换行、\t制表等）

- 字符串不可变（必须先销毁原始字符串，然后将包含新值的另一个字符串保存到该变量）
- 转换为字符串





#### **箭头函数**

1. **如果只有一个参数，()可以省略**
2. **如果只有一个return，{}可以省略**

箭头函数可以改变this的当前环境（取决于声明函数的位置）

```javascript
let show = function (){
	alert('abc');
};

let show = () => {
	alert('abc');
};

------------------------------------------------------------------

let show = function (a, b){
  alert(a+b);
};
show(12, 6);

let show = (a, b) => {
  alert(a+b);
};
show(12, 6);

------------------------------------------------------------------
  
let arr = [12, 5, 8, 99, 33, 14, 26];
arr.sort(function(n1, n2){
  return n1 - n2;
});

arr.sort((n1, n2) => {
  return n1 - n2;
});

arr.sort((n1, n2) => return n1 - n2);

------------------------------------------------------------------

// 只有一个参数时可以省略圆括号
// 只有一个return时可以省略花括号
let show = (a) => {
  return a * 2;
};

let show = a => {
  return a * 2;
};

let show = a => a * 2;
```



#### **函数的参数**

1. 参数扩展/展开

   - Rest Parameter 剩余参数

     收集剩余的参数 不定长参数用...args表示（必须是最后一个形参）可以自行更改剩余参数的名字

     function show (a, b, ...args) {};

   - 展开数组 展开后的效果相当于直接把数组的内容取出（除了直接赋值，其他的都可以）

     let arr = [1, 2, 3];

     ...arr就代表1, 2, 3

```javascript
let arr1 = [1, 2, 3];
let arr2 = [5, 6, 7];
let arr = [...arr1, ...arr2];

arr = [1, 2, 3, 5, 6, 7];

------------------------------------------------------------

function show(...args) {
  fn(...args);
}

function fn(a, b) {
  alert(a + b);
}

show(12, 5);
```

2. 默认参数

```javascript
function show(a, b=5, c=12) {
	console.log(a, b, c);
}
show(99); // 99 5 12
show(99, 19); // 99 19 12
show(99, 19, 13); // 99 19 13
```



#### **解构赋值**

#### （数组和json中都有）

1. 左右两边结构必须相同
2. 右边必须是个东西（例如{}就不是东西）
3. 声明和赋值不能分开（必须在同一句话中完成）

```javascript
let [a, b, c] = [1, 2, 3];

let {a, c, d} = {a: 12, c: 5, d: 6}

let [{a, b}, [n1, n2, n3], num, str] = [{a: 12, b: 5}, [12, 5, 8], 8, 
                                       'cxzxc'];

let [json, arr, num, str] = [{a: 12, b: 5}, [12, 5, 8], 8, 
                                       'cxzxc'];
```



#### 数组

- **map  映射**  一对一

```javascript
[12, 58, 99, 86, 45, 91]
[不及格, 不及格, 及格, 及格, 不及格, 及格]

[45, 57, 135, 28]
[
	{name: 'blue', level: 0, role: 0},
  {name: 'zhangsan', level: 99, role: 3},
  {name: 'aaa', level: 0, role: 0},
  {name: 'blue', level: 0, role: 0},
]

---------------------------------------------------------------------

let arr = [12, 5, 8];
let result = arr.map(function (item) {
  return item * 2;
})
// result为24 10 16
let result = arr.map(item => return item * 2)

---------------------------------------------------------------------

let score = [19, 85, 99, 25, 90];
let score.map(item => item>=60 ? '及格' : '不及格');
// [不及格, 及格, 及格, 不及格, 及格]
```



- **reduce  汇总**  多对一

```javascript
// 计算总数
let arr = [12, 69, 180, 8763];
let result = arr.reduce(function (tmp, item, index) {
  return tmp + item;
})
//  result = 9024

// 计算平均数
let arr = [12, 69, 180, 8763];
let result = arr.reduce(function (tmp, item, index) {
  if (index != arr.length-1) { // 不是最后一次加法
    return tmp + item;
  }
  else { // 最后一次
    return (temp + item) / arr.length;
  }
  return tmp + item;
});
```



- **filter  过滤器**

```javascript
let arr = [12, 5, 8, 99, 27, 36, 75, 11];

let result = arr.filter(item => {
  if (item % 3 ==0){
    return true;
  }
  else {
    return false;
  }
})

let result = arr.filter(item => return item % 3 == 0)

---------------------------------------------------------------------

let arr = [
  {title: "男士衬衫", price: 75},
  {title: "女士包", price: 57842},
  {title: "男士包", price: 65},
  {title: "女士鞋", price: 27531},
]

let result = arr.filter(json => json.price>=10000);
```



- **forEach  循环**（迭代）

```javascript
let arr = [12, 5, 8, 9];

arr.forEach((item, index) => {
  alert(index+":"+item);
})
```



#### 字符串

1. 增加两个新方法

startsWith  判断网址前缀

endsWith  判断邮箱上传附件的扩展名

```javascript
let str = 'asdsffdgfhf';
alert(str.startsWith('a')); // true
let str = '1.txt'
alert(str.endsWith('.txt')); // true
```



2. 字符串模版  字符串连接

```javascript
let a = 12;
let str = `a${a}bc`;
alert(str); // a12bc
```

- 直接将内容加入字符串中  ${a}
- 可以换行



#### 面向对象

1. **class关键字、构造器和类分开**
2. **class里面直接加方法**

```javascript
class User {
  constructor(name, pass) {
    this.name = name;
    this.pass = pass;
  }
  
  showName(){
    alert(this.name);
  }
  showPass(){
    alert(this.pass);
  }
}

// 继承
class VipUser extends User {
  constructor(name, pass, level) {
    super(name, pass); // 执行父类的构造函数
    this.level = level;
  }
  
  showLevel(){
    alert(this.level);
  }
}
```



#### 面向对象-应用 React

1. 组件化
2. 强依赖于JSX（也就是babel、browser.js）

```javascript
class Test extends React.Component {
  constructor(...args) {
    super(...args);
  }
  
  render() {
    return <span>123</span>;
  }
}

window.onload = function (){
  let oDiv = document.getElementById('div1');
  
  ReactDOM.render(
  	<Test></Test>,
    oDiv
  );
};

---------------------------------------------------------------------

class Item extends React.Component {
  constructor(...args) {
    super(...args);
  }
  render() {
    return <li>{this.props.str}</li>;
  }
}

class List extends React.Coponent{
  constructor(...args) {
    super(...args);
  }
  
  render(){
    let aItems = [];
    // 法一
    for(let i=0; i < this.props.arr.length; i++){
      aItems.push(<Item str = {this.props.arr[i]}></Item>)
    }
  	return {aItems};
		// 法二
		return <ul>
      {this.props.arr.map(a => <Item str = {a}></Item>)}
      </ul>;
  }
}

window.onload = function (){
  let oDiv = document.getElementById('div1');
  ReactDOM.render(
  	<List arr={['abc', 'erw', 'asfaa']}></List>,
    oDiv
  );
};
```



#### JSON

json的标准写法：  {"a": 12, "b": 4}    {"a": "snaif", "b": 4}

- 只能用双引号
- 所有的名字都必须用引号包起来



1. JSON对象

```javascript
let json = {a: 12, b: 5};
let str = 'http://it.kaikeba.com/path/user?data='+encodeURIComponent(JSON.stringify(json)); // stringify字符串化

let str = '{"a": 12, "b": 5, "c": "abc"}';
let json = JSON.parse(str); // parse解析
```

2. JSON简写

名字  名字与值相同时可以只写一个（key与value）

方法 （:function都可以删除）



#### Promise

异步：操作之间无关，可以同时进行多个操作   代码复杂

同步：操作之间相关，同时只能做一件事           代码简单



Promise -> 消除异步操作（用同步的方式来书写异步代码）

用法： **Promise.all和Promise.race两种**

```javascript
let p1 = new Promise(function (resolve, reject){
  // 异步代码 resolve-成功 reject-失败
  &.ajax({
    url: 'data/arr.txt',
    dataType: 'json',
    success(arr) {
      resolve(arr);
    },
    error(err){
      reject(err);
    }
  })
});

p1.then(function (arr){
  alert('成功了'+arr);
}, function(err){
  alert('失败了'+err);
});

---------------------------------------------------------------------------

let p1 = new Promise(function (resolve, reject){
  // 异步代码 resolve-成功 reject-失败
  &.ajax({
    url: 'data/arr.txt',
    dataType: 'json',
    success(arr) {
      resolve(arr);
    },
    error(err){
      reject(err);
    }
  })
});
  
let p2 = new Promise(function (resolve, reject){
  // 异步代码 resolve-成功 reject-失败
  &.ajax({
    url: 'data/json.txt',
    dataType: 'json',
    success(arr) {
      resolve(arr);
    },
    error(err){
      reject(err);
    }
  })
});

Promise.all([
  p1, p2
]).then(function () {
  let [res1, res2] = arr;
  alert("全都成功了");
  alert(res1);
  alert(res2);
}, function () {
  alert("至少有一个失败了");
});

--------------------------------------------------------------------------------

function createPromise(url){
  return new Promise(function) (resolve, reject){
  	// 异步代码 resolve-成功 reject-失败
  	&.ajax({
    	url,
    	dataType: 'json',
    	success(arr) {
      	resolve(arr);
    	},
    	error(err){
      	reject(err);
    	}
  	})
	});
}

Promise.all([
  createPromise('data/arr.txt');
  createPromise('data/json.txt');
]).then(function () {
  let [res1, res2] = arr;
  alert("全都成功了");
  alert(res1);
  alert(res2);
}, function () {
  alert("至少有一个失败了");
});

--------------------------------------------------------------------------------

Promise.all([
  $.ajax(url: 'data/arr.txt', dataType: 'json'),
  $.ajax(url: 'data/arr.txt', dataType: 'json'),
]).then(function (results) {
  let [arr, json] = results;
  alert('成功了');
  console.log(arr, json);
}, function () {
  alert("至少有一个失败了");
});

--------------------------------------------------------------------------------

Promise.race 竞速
```



#### async / await

彻底用同步代码来写异步代码（generator和yield已经被取代）

- 普通函数 一直执行到结束停止

- async函数可以暂停

```javascript
async function show() {
  let a = 12;
  let b = 5;
  let data = await $.ajax(url: 'data/1.txt', dataType: 'json');
  alert(a+b+data[0]);
}
```



#### generator 生成器

```javascript
function *show() {
  alert('a');
  yield;
  alert('b');
}
let genObj = show();
genObj.next();  // a
genObj.next();  // b
```

- yield 传参

```javascript
function *show(){
  alert('a');
  let a = yield;
  alert('b');
  alert(a); // a = 5
}
let gen = show();
gen.next(12); // 用yield传参时 第一个yield是废的 想要第一个next中有参数传进去 直接使用正常的函数传参方式
gen.next(5);
```

- yield 返回

```javascript
function *show(){
  alert('a');
  yield 12;
  alert('b');
  return 55;
}
let gen = show();
let result1 = gen.next(); // {value: 12, done: false}
let result2 = gen.next(); // {value: undefined, done: true} 没有return
													// {value: 55, done: true} 有return

------------------------------------------------------------------------

function *炒菜(菜市场买回来的){
  洗菜->洗好的菜
  let 干净的菜 = yield 洗好的菜
  干净的菜->切->丝
  let 切好的菜 = yield 丝
  切好的菜->炒->熟的菜
  return 熟的菜
}
```



#### ES7预览

1. 数组 includes 数组是否包含某个内容

2. 数组 keys/values/entries

   for ... of

   for ... in

   keys 所有的key拿出来

   values 所有的values拿出来

   entries 所有的key-value对拿出来  {key: 0, value: 12}, {key: 1, value: 5}, ...

3. 幂 **

4. padStart/padEnd

5. 语法容忍度 [1, 2, 4, ]多一个逗号可以容忍

6. async await  不依赖于外部的runner、可以使用箭头函数 



#### babel.js编译

将ES6代码编译成低版本浏览器也可以运行的代码



#### 模块

- 定义 export
- 使用 import

语言支持 但是浏览器不支持 需要用webpack编译