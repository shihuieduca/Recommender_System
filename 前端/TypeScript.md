### TypeScript

---

- `ts-node`插件，可以省去对`.ts`文件编译成`.js`文件的过程，直接运行`.ts`得到结果。

- `ts-node`的安装：

```typescript
npm install -g ts-node
```

- 运行：

```typescript
ts-node Demo.ts
```

---

#### catalogue

- 静态类型
- 类型注释和类型推断
- 函数参数和返回类型定义
- 数组类型定义
- 元组的使用和类型约束
- interface接口
- 类的概念和使用
- 类的访问类型
- 类的构造函数
- 类的Getter、Setter和static使用
- 类的只读属性和抽象类
- 配置文件tsconfig.json

- 联合类型和类型保护
- Enum枚举类型
- 函数泛型
- 类中泛型

- 命名空间Namespace（未完）
- TypeScript使用import语法（未完）
- 用Parcel打包TypesScript代码（未完）
- 在TypeScript中使用Jquery库（未完）



---



#### 静态类型

- 定义静态类型（定义变量为const后不能再改变其类型）

```typescript
const count: number = 1;
```

- 自定义静态类型

```typescript
interface Person {
	  uname: string;
	  age: number;
}

const xiaohong: Person = {
	  uname: 'xiaohong',
	  age: 18,
}
```

- 优点：变量的类型、属性和方法都确定了，大大提高了程序的健壮性。



- 静态类型的分类

  - 基础静态类型：

    `number`、`string`、`null`、`undefined`、`symbol`、`boolean`、`void`等

  - 对象类型

```typescript
// 经典对象类型
const Person: {
    name: string,
    age: number,
} = {
    name: 'xiaohong',
    age: 18,
};
console.log(Person.name)

——————————————————————————————————————————————————

// 数组类型
const persons: string[] = ['xiaohong', 'sanlun', 'Levi'];

——————————————————————————————————————————————————

// 类类型
class Person {}
const person: Person = new Person();

——————————————————————————————————————————————————

// 函数类型
const person: () => string = () => {
  return 'Levi';
}
```



---



#### 类型注释和类型推断

- 类型注释主动说明变量的类型
- 类型推断自动尝试分析变量类型
- 宗旨：每个变量每个对象的属性类型应该固定，如果能够推断就可以省略不写，如果不能推断则需要进行注释。



---



#### 函数参数和返回类型定义

- 返回类型定义：

```typescript
// 简单返回类型定义
function getTotal(one: numbee, two: number): number {
	  return one + two;
}

——————————————————————————————————————————————————

// 无返回值时定义（void）
function sayHello(): void {
   console.log('hello');
}

——————————————————————————————————————————————————

// 函数永远执行不完时定义返回值类型never
// 抛出异常
function errFunction(): never {
  throw new Error();
  console.log('hello');
}

// 死循环
function forNever(): never {
  whilw (true) {}
  console.log('hello');
}
```

- 函数参数（为对象或解构时）

```typescript
function add({ one, two }: { one: number, two: number }): number {
  return one + two;
}

const three = add({ one: 1, two: 2 });

——————————————————————————————————————————————————

function getNumber({ one }: { one: number }): number {
  return one;
}

const one = getNumber({ one: 1 });
```



---



#### 数组类型定义

- 一般数组类型的定义

```typescript
const numberArr: number[] = [1, 2, 3];
const stringArr: string[] = ["a", "b", "c"];
const undefinedArr: undefined[] = [undefined, undefined];

const arr: (number | string)[] = [1, "string", 2];
```

- 数组中对象类型的定义（类型别名type 或 类class）

```typescript
type Person = { name: string, age: Number };
const persons: Person[] = [
  { name: "Levi1", age: 18 },
  { name: "Levi2", age: 28 },
];

——————————————————————————————————————————————————

class Person {
  name: string;
  age: number;
}
const persons: Person[] = [
  { name: "Levi1", age: 18 },
  { name: "Levi2", age: 28 },
];
```



---



#### 元组的使用和类型约束

- 元组不常用，一般只在数据源是csv的时候用。元组相当于数组的加强版，可以更好地控制或规范里面的类型。

```typescript
const person: [string, string, number] = ["dajiao", "teacher", 28];

——————————————————————————————————————————————————

const persons: [string, string, number][] = [
  ["dajiao", "teacher", 28],
  ["liuying", "teacher", 18],
  ["cuihua", "teacher", 25],
];
```



---



#### interface接口

- 用于规范类型

```typescript
interface Girl {
  name: string;
  age: number;
  bust: number;
}

const screenResume = (girl: Girl) => {
  girl.age < 24 && girl.bust >= 90 && console.log(girl.name + "进入面试");
  girl.age > 24 || (girl.bust < 90 && console.log(girl.name + "你被淘汰"));
};

const getResume = (girl: Girl) => {
  console.log(girl.name + "年龄是：" + girl.age);
  console.log(girl.name + "胸围是：" + girl.bust);
};

const girl = {
  name: "大脚",
  age: 18,
  bust: 94,
};

screenResume(girl);
getResume(girl);
```

- 接口和类型别名的区别：类型别名可以直接指定类型，比如string等，但是接口必须代表对象。

- interface接口中的可选值

```typescript
interface Girl {
  name: string;
  age: number;
  bust: number;
  // 可选值
  waistline?: number;
}

const getResume = (girl: Girl) => {
  console.log(girl.name + "年龄是：" + girl.age);
  console.log(girl.name + "胸围是：" + girl.bust);
  // 如果有腰围值 则输出
  girl.waistline && console.log(girl.name + "腰围是：" + girl.waistline);
};
```

- 允许加入任意值

```typescript
interface Girl {
  name: string;
  age: number;
  bust: number;
  // 可选值
  waistline?: number;
  // 允许任意值
  [propname: string]: any;
}

const girl = {
  name: "Levi",
  age: 18,
  bust: 94,
  waistline: 21,
  sex: "女",
};

const getResume = (girl: Girl) => {
  console.log(girl.name + "年龄是：" + girl.age);
  console.log(girl.name + "胸围是：" + girl.bust);
  girl.waistline && console.log(girl.name + "腰围是：" + girl.waistline);
  girl.sex && console.log(girl.name + "性别是：" + girl.sex);
};
```

- 接口里的方法

```typescript
interface Girl {
  name: string;
  age: number;
  bust: number;
  waistline?: number;
  [propname: string]: any;
  say(): string;
}

const girl = {
  name: "Levi",
  age: 18,
  bust: 94,
  waistline: 21,
  sex: "女",
  say() {
    return "欢迎光临";
  },
};

const getResume = (girl: Girl) => {
  console.log(girl.name + "年龄是：" + girl.age);
};
```

- 接口和类的约束

```typescript
class XiaoJieJie implements Girl {
  name = "Levi";
  age = 18;
  bust = 90;
  say() {
    return "欢迎光临";
  }
}
```

- 接口间的继承

```typescript
// 继承并增加一个teach函数
interface Teacher extends Girl {
  teach(): string;
}

const getResume = (girl: Teacher) => {
  console.log(girl.name + "年龄是：" + girl.age);
  console.log(girl.name + "胸围是：" + girl.bust);
  girl.waistline && console.log(girl.name + "腰围是：" + girl.waistline);
  girl.sex && console.log(girl.name + "性别是：" + girl.sex);
};

const girl = {
  name: "Levi",
  age: 18,
  bust: 94,
  waistline: 21,
  sex: "女",
  say() {
    return "欢迎光临";
  },
  teach() {
    return "我是一个老师";
  },
};

getResume(girl);
```

- TypeScript可以作为语法校验的工具，编译成正式的js代码之后就没有任何用处了。



---



#### 类的概念和使用

- 简单的类

```typescript
class Lady {
  content = "Hi";
  sayHello() {
    return this.content;
  }
}

const goddess = new Lady();
console.log(goddess.sayHello());
```

- 类的继承

```typescript
class Lady {
  content = "Hi";
  sayHello() {
    return this.content;
  }
}
// 类的继承
class Person extends Lady {
  sayLove() {
    return "I love you";
  }
}

const goddess = new Person();
console.log(goddess.sayHello());
console.log(goddess.sayLove());
```

- 类的重写

```typescript
class Person extends Lady {
  sayLove() {
    return "I love you!";
  }
  // 重写函数
  sayHello() {
    return "Hi , honey!";
  }
}
```

- super关键字的使用

```typescript
class XiaoJieJie extends Lady {
  sayLove() {
    return "I love you!";
  }
  sayHello() {
    // super.可以直接使用父类中的方法
    return super.sayHello() + "。你好！";
  }
}
```



---



#### 类的访问类型

- 三个关键字：`private`、`protected`、`public`

  - `public`在程序中允许在类的内部和外部被调用

    不在类里对变量或函数的访问属性进行定义就默认为`public`访问属性

  - `private`只允许在类的内部被调用，外部不允许调用

  - `protected`允许在类内以及继承的子类中使用



---



#### 类的构造函数（constructor）

- 构造函数的应用场景：在类内定义变量，但是不直接赋值，而是希望在new出对象的时候，直接通过传递参数的形式来实现对变量的赋值。

```typescript
class Person{
    public name :string ;
  	// 构造函数
    constructor(name:string){
        this.name=name
    }
  	// 简写
  	// constructor(public name:string){}
}

const person= new Person('jspang')
console.log(person.name)
```

- 继承类中的构造函数写法

```typescript
class Person{
    constructor(public name:string){}
}

class Teacher extends Person{
    constructor(public age:number){
      	// 子类中写构造函数时必须用super()调用父类的构造函数，如果需要传值，也必须进行传值操作。即使父类没有构造函数，子类也要使用super()进行调用，否则就会报错。
        super('jspang')
    }
}

const teacher = new Teacher(18)
console.log(teacher.age)
console.log(teacher.name)
```



---



#### 类的Getter、Setter和static使用

- 类的Getter属性（关键字是get）和Setter属性（关键字是set）

```typescript
class Person {
  constructor(private _age:number){}
  get age(){
    	// 可以对返回值进行修改处理
      return this._age - 10
  }
  set age(age:number){
    	// 也可以对值进行修改处理
    	this._age=age
  }
}

const dajiao = new Person(28)
dajiao.age=25
console.log(dajiao.age)
```

- static（不用new出对象就可以直接使用类中的方法）

```typescript
class Girl {
  static sayLove() {
    return "I Love you";
  }
}
console.log(Girl.sayLove());
```



---



#### 类的只读属性和抽象类

- 类的只读属性`readonly`

```typescript
class Person {
  	// 由于_name只读 所以程序在外部修改了_name会报错
    public readonly _name :string;
    constructor(name:string ){
        this._name = name;
    }
}

const person = new Person('jspang')
person._name= '谢广坤'
console.log(person._name)
```

- 抽象类的使用

```typescript
// 抽象类
abstract class Girl{
    abstract skill()  //因为没有具体的方法，所以我们这里不写括号
}

// 分别继承抽象类 要求必须实现skill()方法
class Waiter extends Girl{
    skill(){
        console.log('请喝水！')
    }
}

class BaseTeacher extends Girl{
    skill(){
        console.log('来个按摩')
    }
}

class seniorTeacher extends Girl{
    skill(){
        console.log('来个SPA')
    }
}
```



---



#### 配置文件tsconfig.json

- 生成tsconfig.json文件 `tsc --init`
- tsconfig.json文件用来配置如何对ts文件进行编译，也叫做TypeScript的编译配置文件。
- 生成配置文件后使用`tsc`进行编译，得到js文件。
- 配置文件不支持单引号，文件内必须使用双引号。



- include、exclude、files 选择编译的文件

```typescript
// include
{
  "include":["demo.ts"],
  "compilerOptions": {
      //any something
      //........
  }
}

// exclude
{
   "exclude":["demo2.ts"],
  "compilerOptions": {
      //any something
      //........
  }
}

// files
{
  "files":["demo.ts"],
  "compilerOptions": {
      //any something
      //........
  }
}
```

- compilerOptions配置项
  - removeComments 设置TypeScript编译出的js文件是否显示注释
  - strict 设置TypeScript是否按照最严格的规范来写
  - noImplicitAny 设置就算是any（任意值），也需要进行类型注释
  - strictNullChecks 不强制检查NULL类型
  - rootDir和outDir 设置根路径和打包（编译）路径
  - sourceMap 存储转换后代码与转换前代码的对应位置
  - noUnusedLocals和noUnusedParameters 设置是否允许有只定义但没使用的变量/函数

- 完整信息查询：https://www.tslang.cn/docs/handbook/compiler-options.html



---



#### 联合类型和类型保护

- 只有联合类型存在的情况下才需要类型保护。
- 联合类型：允许变量可能有两种或两种以上的类型
- 类型保护：类型断言、in语法、typeof语法、instanceof语法

```typescript
interface Waiter {
  anjiao: boolean;
  say: () => {};
}

interface Teacher {
  anjiao: boolean;
  skill: () => {};
}

// 类型保护-类型断言
function judgeWho(animal: Waiter | Teacher) {
  if (animal.anjiao) {
    (animal as Teacher).skill();
  }else{
    (animal as Waiter).say();
  }
}

// 类型保护-in语法
function judgeWhoTwo(animal: Waiter | Teacher) {
  if ("skill" in animal) {
    animal.skill();
  } else {
    animal.say();
  }
}

// 类型保护-typeof语法
function add(first: string | number, second: string | number) {
  if (typeof first === "string" || typeof second === "string") {
    return `${first}${second}`;
  }
  return first + second;
}

// 类型保护-instanceof语法
function addObj(first: object | NumberObj, second: object | NumberObj) {
  if (first instanceof NumberObj && second instanceof NumberObj) {
    return first.count + second.count;
  }
  return 0;
}
```



---



#### Enum枚举类型

- 枚举类型有对应的数字值，默认从0开始，也可以打印出枚举的值（下标）

```typescript
enum Status {
  MASSAGE,
  SPA,
  DABAOJIAN,
}

function getServe(status: any) {
  if (status === Status.MASSAGE) {
    return "massage";
  } else if (status === Status.SPA) {
    return "spa";
  } else if (status === Status.DABAOJIAN) {
    return "dabaojian";
  }
}

const result = getServe(Status.SPA);

console.log(`我要去${result}`);
```



---



#### 函数泛型

- 泛型用<>进行定义，正式调用方法时，就要具体指明泛型的类型。

```typescript
function join<JSPang>(first: JSPang, second: JSPang) {
  return `${first}${second}`;
}
join < string > ("jspang", ".com");
join < number > (1, 2);


——————————————————————————————————————————————————

// 泛型中的数组
function myFun<ANY>(params: ANY[]) {
  return params;
}
myFun < string > ["123", "456"];

function myFun<ANY>(params: Array<ANY>) {
  return params;
}
myFun < string > ["123", "456"];


——————————————————————————————————————————————————

// 多个泛型的定义
function join<T, P>(first: T, second: P) {
  return `${first}${second}`;
}
join < number, string > (1, "2");

——————————————————————————————————————————————————

// 泛型的类型推断（但是不推荐大量使用，会降低代码的易读性和健壮性）
function join<T, P>(first: T, second: P) {
  return `${first}${second}`;
}
join(1, "2");
```



---



#### 类中泛型

```typescript
class SelectGirl<T> {
  constructor(private girls: T[]) {}
  getGirl(index: number): T {
    return this.girls[index];
  }
}

const selectGirl = new SelectGirl() < string > ["大脚", "刘英", "晓红"];
console.log(selectGirl.getGirl(1));
```

- 泛型中的继承

```typescript
interface Girl {
  name: string;
}

class SelectGirl<T extends Girl> {
  constructor(private girls: T[]) {}
  getGirl(index: number): string {
    return this.girls[index].name;
  }
}

const selectGirl = new SelectGirl([
  { name: "大脚" },
  { name: "刘英" },
  { name: "晓红" },
]);
console.log(selectGirl.getGirl(1));
```

- 泛型约束

```typescript
class SelectGirl<T extends number | string> {
  constructor(private girls: T[]) {}
  getGirl(index: number): T {
    return this.girls[index];
  }
}

const selectGirl = new SelectGirl<string>(["大脚", "刘英", "晓红"]);
console.log(selectGirl.getGirl(1));
```



---



####  命名空间Namespace

- 搭建基础TypeScript开发环境

```
1、建立好文件夹后，打开 VSCode，把文件夹拉到编辑器当中，然后打开终端，运行npm init -y,创建package.json文件。
2、生成文件后，接着在终端中运行tsc -init,生成tsconfig.json文件。
3、新建src和build文件夹，再建一个index.html文件。
4、在src目录下，新建一个page.ts文件，这就是我们要编写的ts文件了。
5、配置tsconfig.json文件，设置outDir和rootDir(在 15 行左右)，也就是设置需要编译的文件目录，和编译好的文件目录。
6、然后编写index.html，引入<script src="./build/page.js"></script>,当让我们现在还没有page.js文件。
7、编写page.ts文件，加入一句输出console.log('jspang.com'),再在控制台输入tsc,就会生成page.js文件
8、再到浏览器中查看index.html文件，如果按F12可以看到jspang.com，说明我们的搭建正常了。
```