[TOC]



### JavaScript简介

* 脚本语言
  * 必须要有解释器
  * 脚本引擎
  * 不止JavaScript
    * JScript  微软出品  仅支持IE
    * VBScript  微软出品   用于桌面客户端   占比很少
    * PHP  服务端脚本语言

* 占前端的比重(HTML + CSS + JavaScript)
  * 80%   占比前端代码
  * JavaScript编程语言, Html和Css是标记语言

* 特点
  * 易入门, 难深入理解
  * 应用上学习
  * 理解上学习

* 组成

  * ECMAScript    *重心在这里
    * ECMA是欧洲计算机制造联合会
    * 中立
    * 指定脚本语言的规范ECMAScript
    * 语法、变量、关键词、对象...

  * DOM
    * Document Object Model
    * 用来操作文档流(遵循w3c规范)

  * BOM
    * Browser Object Model
    * 用来操作浏览器
      * 滚动条
      * 事件



### JavaScript写在哪里

* 内部引用
  * `<script>`标签内

* 外部引用
  * 通过`script`标签的`src`属性引入js文件

* 注意
  * 不要同时使用内部引用和外部引用, 这样只会生效外部引用
  * `script`标签上可以不写type, 但是写了一定要写对  text/javascript
    * 有时也故意写错, 用于存放html模板

* 推荐使用外部引用的方式
  * 样式, 结构和逻辑分离 



### JavaScript基本语法及术语

```js
var a,b,c,d;//声明变量
3.14//字面量
a='nick';//赋值
a=888;
b=2;
c=3;
d=b+c;//运算
//不可将变量名声明为保留字或关键字
var if
```

* 语句
  * 值、运算符、表达式、关键词和注释
  * 语句会按照它们被编写的顺序逐一执行
  * 以分号结束语句不是必需的, 是代码风格取向

* 字面量
  * 一般固定的值称为字面量
  * 比如`3.14`、`nick`
  * `{}`对象字面量
  * `[]`数组字字面量
  * `function test() {}`函数字面量

* 变量
  * 使用var定义变量
  * 变量声明是弱类型的, 可以随时更改
  * 变量可以通过变量名访问, 字面量是一个恒定的值

* 运算符
  * 赋值、算术和位运算符
  * 条件、比较及逻辑运算符
  * 在运算符旁边( = + - * / ) 添加空格是个好习惯

* 关键字
  * 用于标识要执行的操作
  * 比如`var`是告诉浏览器创建一个变量

* 保留字
  * 以后可能会实现的关键字
  * 不必去记有哪些关键字, 编辑器会变色关键字



### JavaScript中面向对象的概念

* 在js里,万物皆对象!

* JavaScript中怎么创建对象

  ```js
  //创建对象
      var person = new Object({name: 'Nick'});
      //等价写法
      var animal={
  
      };
      console.log(person);
  ```

  

### JavaScript变量

* 栈内存
  * 原始类型保存在栈内存中

* 堆内存

  <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E5%86%85%E5%AD%98%E6%A8%A1%E5%9E%8B.png" alt="内存模型" style="zoom:80%;" />

* 7种原始类型(基本类型、简单类型)

  * Boolean(布尔值)
    * 计算机  非真既假

  * Null
    * 指的是你声明了一个对象未设置值
    * 可以理解为尚未创建的对象

  * Undefined

    * 声明了变量, 但没有赋值

      ```js
      var a = 2;
      var a
      ```

  * Number

    * 超过了一定的范围, 会丢失精度

      ```js
      0.1 + 0.1 === 0.2   //未必会成立
      ```

      

  * String
    * 在js里字符串使用单引号或双引号围住的

  * Symbol

    * es6提出的新概念

    * 如果你的前人写了一个属性名, 你现在想提供一个和这个属性名同名的属性名, 该怎么办?你就可以使用Symbol, 它的作用就是创建唯一变量

      ```js
      //  eg:  name,  Symbol(name)
      const symbol1 = Symbol('foo');
      const symbol2 = Symbol('foo');
      console.log(symbol1 === symbol2);//false
      ```

  * Bigint
    * 当需要用到超级大的数时才会用

* 引用类型(复杂类型)
  * Object
    * 万物皆对象

* 原始类型和引用类型

  * 原始类型 值是保存在栈内存, 按值保存

  * 引用类型 栈内存里保存的指针, 堆内存里保存的值

    ```js
    
        var person = {
            name: 'nick'
        };
        var person2 = person;
        person2.age = 18;
    	console.log('person',person);//console.log支持并行输出,第一个参数为字符串,第二个参数为要输出的变量
        // 现在person内也有age成员了
        //因为person和person2内存储的其实是同一块堆内存的地址, 对任何一个的修改到会修改堆内存中的存储
    ```

    

### 变量声明规范

* 变量声明和变量赋值
  * 单一声明
  * 多个声明

* 声明规范
  * 虽然每个单位都有自己的规范
  * 必须是以字母、下划线 ( _ ) 或者美元符号 ( $ ) 开头
  * 变量是对大小写敏感的
  * 关键字和保留字不能用

* 建议
  * 定一个语义化变量名
  * 小驼峰命名变量  例如: myHeader
  * 构造函数是用每个单词首字母都是大写的
  * 使用英文命名, 不要使用拼音



### js基础之变量运算

* 运算优先级高于赋值
* 同类型的运算
  * 直接值进行运算

* 不同类型的运算

  * 类型转换, 值进行运算

    ```js
    var a = 2, b = '3';
        var c = a + b;//先将a->'a' ,再和b字符串拼接成  '23'
        var d = !a;//先将a->true ,再进行取非运算, 结果为false
    ```

    

### js基础之常见运算符

* 运算符
  * 是一类数学符号, 可以根据两个值(或变量)产生结果

* 算数运算符
  * +
  * -
  * *
  * /
  * %
  * 可以和等号组合(符号赋值运算符)
    * a += 2 => a = a + 2
    * a -= ... ...

* 关系运算符
  * 大小比较
  * 等值比较

* 自增自减
  * ++
  * --

* =
  * =   赋值
  * ==   判断是否相等, 对不同类型会进行类型转换
  * === 判断是否相等, 不会进行类型转换, 直接进行值的判断

* 数组转换字符串

  ```js
      var array = [1, 2, 3];
      var f = 2;
      console.log(a + array);//21, 2, 3
  ```

  

### js中的真真假假

* 真
  * 满足条件即为真
  * 变量可转为布尔值true

* 假
  * 不满足条件就是假
  * 变量可转为布尔值false

* `true`和`false`就是js告诉用户的真真假假

* 真与假的运算  (当目前判断结果已经可以确定最终结果时, 不会再进行后继判断)
  * 与   `&&`    同时为真才为真
    * 当判断变量为真进行下一个判断, 为假时停止, 直接输出
  * 或   `||`    其中一个为真就为真
    * 当判断变量为真, 停止, 直接输出, 否则进行下一个判断
  * 非   `!`     真假颠倒

```js
// 6个假变量
1. false (布尔值)
2. null (用于定义空的或者不存在的引用)
3. undefined (未定义值)
4. 0 (数字类型)
5. ""  ''  (空字符串)  (字符型)
6. NaN (not a Number)  (当其他类型转换为数值失败时返回此数值)
	//例如:parseInt('hahaha') //NaN  
```

```js
var str = 'sss';
var str = 'aaa';//后面声明的变量会覆盖前面声明的变量
var a = 6;
console.log(str || a); // sss
```



### js之调试

* html和css调试技巧

  * 给a元素设置了不同状态下的样式

    <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E4%BC%AA%E7%B1%BB%E6%A3%80%E6%9F%A5.png" alt="伪类检查" style="zoom:67%;" />

  * 快速定位元素

    <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/html%E8%B0%83%E8%AF%95%E6%8A%80%E5%B7%A72.png" alt="html调试技巧2" style="zoom:50%;" />

* 谷歌调试技巧
  * window.console.log   window可省略
  * window.alert     window可省略
  * debugger
    * 暂时程序,  当程序运行到debugger处暂停, (此时可以看到变量的值, 便于检查出错的地方) 只有当点击下一步后才会继续运行.



### js基础之判断

* 语法

  ```js
  if(){
     
  }else if(){
           
  }else{}
  ```

  

* ==和===
  * ===更加严谨

* 注意
  * 判断条件是否互斥
    * else if 的好处就是满足了条件后, 就直接停止了
    * 保证最后有个else, 避免出现异常



### js之三目运算

* ```js
  条件 ? 表达式1 : 表达式2
  ```

* 使用场景

  * 不局限于非真既假的场景
  * 但推荐仅在非真既假的场景使用

* 注意

  * 自带return

    ```js
    str = a > 0 ? 'sss' : 'ss';
    ```

* 条件链

  ```js
  str = a > 0 ? (a > 3 ? '大于3' : '小于等于3') : '小于等于0'
  ```

* 等待用户输入的函数

  ```js
  //此函数会弹出一个对话框并等待用户输入值
  var a = prompt('请输入分数')
  ```

  

### js之switch

* 语法

  ```js
  switch(表达式){
      case n:
          代码块
          break;
      case n:
          代码块
          break;
      default:
          默认代码块
  }
  ```

  

* 和 if 的选择
  * 有3, 4种以上条件的时候, 就可以考虑`switch` 

* 注意
  * 内部严格按照`===`的规则, 一定要值和类型都相等才行
  * break 打断程序, 跳出switch



### js之for

* 前置内容

  ```js
  var str
  console.log(str) //undefined
  ```

  

* for



### js之while

* while () {}
* do {} while ();



### js之零碎的干货

* 获取日期  

  ```js
  //获取当前日期
  const day = new Date();//假如今天是 August 19, 2021 23:15:30
  const today = day.getDate();// 19
  //构造指定的日期
  const birthday = new Date('August 19, 2021 23:15:30')
  const date1 = birthday.getDate();// 19
  
  //返回一个具体日期中一周的第几天
  const week = day.getDay();
  ```

  

* 显示换行

  ```js
  document.write('<br/>');
  ```

  

### js之函数

* 函数没有返回值时, 默认返回undefined

* 语法

  ```js
  function name(参数1, 参数2, 参数3...){
      执行代码
  }
  ```

  

* 示例

  ```js
  function sum(a, b){
      return a + 10 + b
  }
  ```

  

* 注意
  * `return`只能在函数里使用 



### js函数之形参和实参

* 形参
  * 声明函数的时候定义的一个参数

* 实参
  * 调用函数的时候传的一个参数

* 形参和实参是一一对应的
  * 数量可以不对应
  * 函数可以设置默认参数
  * 定义形参的时候需要语义化( 方便理解 )
  * 实参可以是字面量也可以是变量



### js函数之声明的方法

* 声明方式

  * 函数声明

    ```js
    function name(参数){
        
    }
    ```

  * (匿名) 函数表达式

    ```js
    var a = function(){}
    a();//调用
    //下面这样写, 支持调用.name
    var a = function test(){}
    console.log(a.name)// test
    ```

  * new Function()

* 注意
  * 声明函数时, 函数里的语句不会执行
  * 只有当调用函数时, 函数里的语句才会执行



### js函数之返回值

* 函数的作用
  * 在恰当的时机里, 执行一段代码
  * 将值处理后, 返回回来

* `return`的作用
  * 返回值
  * 中断函数
  * 只能写在函数体里面

* 函数是一个封闭的环境, 它不会污染其他环境



### js函数之变量作用域

* 变量
  * 全局变量
    * 挂载到`window`对象上的  (在函数外部直接声明的变量)
  * 局部变量
    * 函数体内部声明的变量

* 作用域链
  * 内层函数是可以访问外层函数声明的变量



### js函数之隐藏的参数

* arguments

  * 是用来取参数的

  * 传入的实参都能在函数体里通过argument类数组获取到

    ```js
    function test(num1, num2 ,num3) {
            for(var i = 3; i <= arguments.length; i++){
                console.log(arguments[i]);
            }
            //输出   4  5  6
            return 1
        }
        var sum = test(1, 2, 3, 4, 5, 6);
    ```

    

### 通用编程思想之递归

* 递归
  * 函数自己调用自己

* 终止条件
  * 使用递归必须有终止递归的条件, 否则就是死循环

```js
function test(num = 1){
    console.log(num)
    num++
    return num < 10 ? test(num) : ''
}
test(1)
```



### js函数之立即执行函数

* 通过 () 将函数声明变成表达式, 进而实现执行
* 使用场景: 某个函数执行一次就够了
* 括号的作用
  * 帮助我们调用函数( 执行 )
  * 括号括起来的被认为是表达式, 所将函数声明用括号包起来,它就变成了表达式, 所以可以被后面的 () 执行

* 什么是立即执行函数
  * IIFE: immediately-invoked function 

* 特点
  * 自动执行
  * 执行完成后销毁

* 写法

  ```js
  (function(params){
      
  })();
  //w3c建议
  (function(params){
      
  }());
  //本质是将函数声明变成表达式, 然后去执行这个表达式
  //通过其他方法也可以将函数声明变成表达式, 比如 !
  !function test4(params){
      
  }();
  ```

  

* 所有的函数或变量声明都是挂载到window对象里的

  ```js
  function test(){//test可以省略
      //立即执行函数又称匿名立即执行函数
  }
  test()
  window.test()
  
  ```

* 可以传参数

* 注意

  * 以`()` `{}`开头的语句, 前面的语句必须加分号, 否则会解析错误

  * () 本质上执行的是表达式  :  表达式()

```js
//简单递归
function factorial(n){
    if(n <= 1){
        return 1
    } else {
        return n * factorial(n-1)
    }
}
```



### js重点知识之闭包

* 函数上下文

  * 上下文
    * 全局上下文
    * 函数上下文

  * 函数上下文在什么时候产生
    * 函数执行(调用)的时候会形成自己的上下文(环境 , 对象)

  * 函数上下文在什么时候销毁
    * 函数执行结束的时候就结束

  * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E5%9B%BE%E8%A7%A3%E5%87%BD%E6%95%B0%E4%B8%8A%E4%B8%8B%E6%96%87.png" alt="图解函数上下文" style="zoom:67%;" />

* 闭包

  * 什么是闭包
    * **JavaScript变量属于本地或全局作用域**
    * **全局变量能够通过闭包实现局部 ( 私有 ) **
      * 只有调用函数才能改变变量

  * 产生闭包

    * 是通过调用函数时返回其内部的函数

      ```js
      function test() {
          var count = 0
          return function inner() {
              count ++
              console.log(count)
          }
      }
      var add = test()
      
      add()  //1
      add()  //2
      add()  //3
      //返回内部函数给变量.  test 函数的上下文已被 inner 抓住, 并完成了实例化, 是可以通过变量来保存这个环境(上下文), 所以add是可以访问到test的上下文(词法环境)
      ```

  * 闭包的副作用
    * 产生内存泄露
      * 例如本来应该被销毁的上下文, 通过闭包被强行保存了下来 ( 保存在内存当中 ) 

  * 通过闭包能实现什么
    * 实现外界访问函数体内部的变量



### js之对象

* js中遗留的一个错误
  * typeof(null)  // object    但null表示的是对象还未创建的变量, 但是要使用到了.  js错误地将它当成了对象

* 除了原始值, 其他都是对象

  * Undefined、Null、Boolean、Number、Symbol、Bigint和String

  * 可以使用`typeof`判断原始类型, 但留意null

    <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%E4%BD%8D%E7%BD%AE.png" alt="对象存储位置" style="zoom:67%;" />

* 语法

  ```js
  //在对象里的函数叫方法 ( methods )
  var person = {
      name: '张三',
      age: 29,
      job: 'teacher',
      eat: function(){}
  }
  //对象的属性名是字符串, 属性的值可以是任意类型的
  //一般情况属性名可以省略"", 但如果是JSON对象, 那么属性名必选用""包起来
  var person1 = person;
  //此时peison1和person都指向同一块存储空间
  ```

  

### js对象之常规操作

* 查

  * 通过`.`运算符可以访问对象属性

  * 或者通过`[]`操作符访问, `[]`里面可以写变量, 也可以写字符串

    ```js
    //仍然使用上节的person
    console.log(person.name)
    
    var key = 'name'
    console.log(person[key])//或者console.log(person['name'])
    
    for(var key in person){
        console.log(person[key])
    }
    ```

* 增

  ```js
  person.sex = 1
  //或者
  person['old'] = 0
  ```

* 改

  ```js
  //与增基本一样, 只不过改的是对象中已有的属性
  person.name = 'Nick'
  ```

* 删

  * `delete`

    ```js
    delete person.sex
    ```

  * 一般不用delete, 多数情况是会清空对象   person = {}



### 对象中的方法怎么访问自己的属性

```js
    var obj = {
        name: 'Nick',
        sayHello: function() {
            console.log(obj.name)
        }
    }
```

* 通过`this`我们能访问对象自己

  ```js
  var obj = {
          name: 'Nick',
          sayHello: function() {
              console.log(this.name)
          },
          speak:function(){
              this.sayHello()
          }
      }
  ```

  在哪里使用this, this指代的就是哪里的对象



### js中创建对象的几种方式

* 对象字面量

  * 声明一个对象, 赋值给一个变量

  ```js
  var obj = {
          name: 'Nick',
          sayHello: function() {
              console.log(obj.name)
          }
      }
  ```

* 构造函数

  * Object
  * 自定义构造函数(命名采用大驼峰的方式)
    * this指向的是对象的本身
    * 使用new实例化一个对象, 就像工厂一样

  ```js
  var obj2 = new Object({
          name: 'Nick',
          sayHello: function() {
              console.log(this.name)
          }
      })
  
      //大驼峰方式创建对象
      function Person(name) {
          this.name = name
          this.sayHello = function() {
              console.log(this.name)
          }
      }
      var obj3 = new Person('Lucy')
  ```

  

### 构造函数的参数应该怎么写

* 固定参数

  * 这种写法会导致用户, 不知道创建对象实例的时候, 传入的参数是什么, 位置也要严格对应

    ```js
    function Car(name, price, size) {
        this.name = name
        this.price = price
        this.size = size
    }
    var audi = new Car('Audi', '30W', 'normal')
    ```

* 不定参数   **推荐**

  ```js
  function Car(obj) {
      this.name = obj.name
      this.price = obj.prize
      this.size = obj.size
  }
  var audi = new Car({
      size: 'large',
      price: '50w',
      name: 'audi'
  })
  //这样一来不仅看起来清晰,而且不需牢牢对齐参数了, 甚至你可以缺少参数(比如你可以不传入size)
  ```

  

### js底层剖析之new做了什么事

* 如果不使用new, 直接调用构造函数

  * 返回undefined, 因为函数没有返回值就会默认返回undefined

  * 不使用new的话, 构造函数内部的this指向的是window

    ```js
    function Student(obj){
        this.name = obj.name
        this.score = obj.score
        this.grade = obj.grade
    }
    var stu1 = Student({
        name: 'Jack',
        score: 99,
        grade: 3
    })
    console.log(stu1)//输出的是undefined, 如果构造函数return this, 则输出的是window对象
    ```

    

* 使用new

  * 创建了一个空的对象

  * 帮助我们把对象返回回来

  * 改变了this的指向, 指向了空对象

    ```js
    //改写构造函数, 代替new
    function Student(obj) {
        var o = {}
        o.name = obj.name
        o.score = obj.score
        o.grade = obj.grade
        return o
    }
    var stu1 = Student({
        name: 'Jack',
        score: 99,
        grade: 3
    })
    console.log(stu1)//正常输出
    ```

### JS重难点之原型全面剖析

* `prototype`

  ```js
  function Person() {}
  console.log(Person.prototype)
  ```

  它是Person的一个属性, 也是一个对象

* 原型的作用

  * 给构造出的对象设置公共的属性或方法

  * 建立了构造函数和实例化出来的对象(new出来的对象)的联系

    ```js
    function Person(obj) {
        this.name = obj.name
        this.age = obj.age
    }
    var person1 = new Person({
        name: 'Tony',
        age: 28
    })
    Person.prototype.country = 'China' //为构造出来的对象提供一个公共的属性
    console.log(person1.country)//China
    console.log(person1)//输出中不包含country
    //你可能不理解为什么称为公共的属性, 你看:
    var person2 = new Person({})
    console.log(person2.country)//China 
    ```

    

### 原型有什么用?

* 重要---笔试
* 原型的作用
  * 给我们构造函数实例化出来的对象设置公共的属性或者方法使用的

* 如何选择性地使用原型?

  * 方法写在原型上

  * 需要配置的属性写在构造函数上

    ```js
    function Person(obj) {
        this.name = obj.name
    }
    Person.prototype.sayHello = function(){
        //...
    }
    var person1 = new Person({
        name: 'Jack',
    })
    person1.sayHello()
    ```

    

* 实例化对象的时候
  * 写在构造函数里的方法和属性会重新克隆一次, 如果实例化次数过多会导致占用内存较高

* 实例化对象能不能对原型上的属性进行改动?
  * 只有构造函数才能对原型上的属性进行改动
  * 构造函数的内部属性, 会覆盖掉原型上的同名属性
  * 原型实质上也是构造函数的属性, 只不过他将构造函数和实例化对象联系起来了



### 面试常考知识之原型链

```js
function Car() {}
var car = new Car()
console.log(car)
console.log(Car.prototype)//构造函数有prototype
console.log(car.prototype)//实例化对象是没有prototype的
//原型链: 是有尽头的, 尽头是null
console.log(car.__proto__.__proto__.__proto__)//null
//  __proto__ 告诉你这是你一个内置属性, 不要对它进行任何更改
```

* 函数才有`prototype`属性, 对象有`__proto__`属性

* 原型链是什么

  * js里万物皆对象, 所以一直访问`__proto__`属性就会产生一条链条

  * 链条的尽头是null

  * 当js引擎查找对象的属性时, 会先判断对象本身是否存在该属性

  * 如果不存在该属性, 那么它就会沿着原型链往上查找

    <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E5%8E%9F%E5%9E%8B%E9%93%BE.png" alt="原型链" style="zoom:67%;" />

    * 从图中也可以看出Object是一切的祖先, Object没有祖先所以它的\__proto__就指向null了



### 插件开发初体验----写一个插件

* 需求: 写一个对两个数字相加的计算器
* 为什么要写在函数里
  * 因为函数里声明的变量或者函数, 对外界无影响
  * 为了让函数在浏览器加载的时候执行, 这需要使用立即函数

* 步骤

  * 写一个立即执行函数

  * 将构造函数写在立即执行函数里

  * 将公共方法写在原型上

  * 将构造函数挂载到window上

    ```js
    // 插件
    ;(function() {//建议在立即函数前写一个;,避免解析出错
        var Computer = function(opt) {} //构造函数
        //将方法写到原型prototype上
        Computer.prototype = {//prototype是一个对象,所以支持以键值对的方式赋值
            plus: function(num1, num2) {
                return num1 + num2 
            }
        }//写在立即执行函数里才能调用到
        window.Computer = Computer //将Computer挂载到对象上才能使用,一般是挂载到window对象
        //使用立即执行函数的另一个好处就是里面声明的变量和方法都是私有,外界访问不到,执行结束就会销毁,不会影响外部环境(这是开发插件需遵守的)
    })()
        //下面来使用一下热乎出炉的插件
    var com = new Computer()
    var sum = com.plus(21, 23)
    console.log(sum)//44
    ```

    

### JS重要数据结构之数组

* 什么是数组
  * 简单讲, 把数据一股脑地放在一起就是数组

* 一些等价写法(或称之为  语法糖)

  ```js
  var obj = {}
  var obj2 = new Object()
  
  var list = [1, 2, 3, true, 'hello']
  var list2 = new Array(
  	1, 2, 3, true, 'list2'
  )
  ```

* 访问数组的数据

  * 通过索引(下标)

    ```js
    console.log(list[index])
    ```

  * 通过length获取数组长度



### JS数组基本操作

* 增删改查

  * 改
    * 索引

  * 查
    * 索引

  * 增
    * 索引
    * push
      * 在数组的后面插入一条数据
    * unshift
      * 在数组的第一位插入一条数据

  * 删
    * pop
      * 删除数组当中最后一个元素
    * shift
      * 删除数组当中第一个元素

```js
var nameList = ['张三', '李四', '王五']
//查
console.log(nameList[2])
//改
nameList[nameList.length - 1] = '666'
//增
nameList.push('lili')
nameList.unshift('lala')
//删
nameList.pop()
nameList.shift()
```



### js之操作数组的常用方法

* splice

  * 用于删除或替换元素

  * 函数有返回值. 返回的是被删除的元素

  * 这个方法还会改变原来的数组

    ```js
    //第一个参数是控制从哪里开始删除或者替换(取决于第三个参数有没有值)
    //第二个参数控制删除的数量
    //第三个参数开始将删除了的元素替换掉, 可以用逗号隔开
    list.splice(2, 2, 'hello', 'Nick')
    ```

    * 使用场景
      * 替换数组中的元素
      * 删除数组的一部分内容
      * 清空数组

* join

  * 将数组类型的数据转换成字符串

  * 和toString(Object的方法)的区别是, 可以自定义元素之间用什么隔开

    ```js
    console.log(list.join('*'))
    //1*2*3*4
    ```

* concat

  * 合并数组(有返回值, 但不会改变原数组)

    ```js
    var list3 = list2.concat(list4, list5)//将list2,list4,list5合并
    ```

    

### 面试常考知识点之复杂类型怎么判断

* 原始数据类型

  `typeof`

  ```js
  var num = 1
  var isShow = true
  //typeof能直接返回原始数据类型的数据类型, 以字符串小写的方式返回(其实也是原型链的终点类型)
  console.log(typeof(num) === 'number')
  ```

  * 判断引用数据类型(数组,new String() ,obj = {})时, 会直接返回原型链上最后的一个对象Object

* 引用数据类型

  `instanceof`

  ```js
  //使用instanceof 判断引用数据类型
  //判断是不是由这个构造函数创建出来的对象实例, 返回的值是布尔类型
  var list = [1, 2, 3, 4]
  console.log(list instanceof Array)
  ```

  * 实质
    * 会查找原型链上存不存在这个构造函数, 存在的话就返回true



### js数组之小例题

```js
//将String转换成数组, 并删除数组中的 jack
var str = 'nick,jack,张三,李四'
console.log(str.split(','))//split()方法使用指定的分隔符字符串将一个Stirng对象分割成子字符串数组
var list = str.split(',')
console.log(list.indexOf('jack'))//indexOf()方法会在数组中查找指定值,如果存在则返回对应下标, 不存在返回 -1 
var findIndex = list.indexOf('jack')
list.splice(findIndex, 1)//删除jack
```

```js
//在排好序的数组中插入新数字
var numList = [23, 32, 45, 53, 62, 68]

function insert(arr, num) {
    for(var i = 0; i < arr.length; i++) {
        if(arr[i] > num) {
            arr.splice(i, 0, num)//在i位置删除0个元素并插入num
            console.log(arr)
            return 
        }
    }
}
insert(numList, 42)
```



### 上手企业开发必须的ajax

* **JSON**

  * JSON是什么
    * JSON是一种轻量级的数据交换格式, 它基于js的一个子集, 易于人的编写和阅读, 也易于机器解析. JSON采用完全独立于语言的文本格式, 但是也使用了类似于C语言家族的习惯(包括C, C++, C#, Java, JavaScript, Perl, Python等). 这些特性使JSON成为理想的数据交换语言.
    * 一言以蔽之
      * JSON是用来做数据交换的一种语言

  * JSON的语法格式

    * 属性名称必须是双引号括起来的字符串

    * 最后一个属性后不能有逗号

      ```js
      var obj = {
          "name" : "zhangsan",
          "age" : "21"
      }
      ```

  * JSON的作用
    * 用于传输数据

  * 序列化和反序列化
    * 对象序列化后可以在网络上传输, 或保存到硬盘上
    * 序列化函数:  JSON.stringify()    将对象转换成String字符串
    * 反序列化函数:  JSON.parse()    将String字符串转换成对象

  * 浏览器的缓存机制
    * 在Application( 应用程序 )内
      * Local Storage  本地存储
      * Session Storage  会话存储---关掉浏览器后会清空, 所以这里面是不能保存对象的,要将数据序列化后保存(或在网络上传输)

* 什么是ajax

  * 以前前后端是后端返回整个html
    * 每更新一些数据, 他都会整个网页刷新

  * 现在
    * ajax帮助我们向服务器发送异步请求

* 同步, 异步
* 原理
  * 通过`XmlHttpRequest`对象向服务器发异步请求, 从服务器获得数据
  * 然后通过`js`来操作`DOM`而更新页面
  * 它是在IE5中首先引入, 是一种支持异步请求的技术
  * 简单而言, javascript 可以及时向服务器提出请求和处理响应, 而不阻塞用户, 达到无刷新的效果

* 注意
  * JavaScript是单线程的, 会阻塞代码运行, 所以引入`XmlHttpRequest`请求处理异步数据

```js
console.log(1)
//js, 有个执行队列的概念, 会等待主线程执行结束后, 才开始执行
setTimeout(function (params) {
    console.log(4)
}, 0)
console.log(2)   //1  2   4
```

* 如何使用ajax

  * 浏览器中查看后台返回的数据

    <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E6%9F%A5%E7%9C%8B%E6%95%B0%E6%8D%AE%E8%AF%B7%E6%B1%82.png" alt="查看数据请求" style="zoom:67%;" />

  * 浏览器中查看传给后台的数据

    <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E6%9F%A5%E7%9C%8B%E8%A6%81%E4%BC%A0%E7%BB%99%E5%90%8E%E5%8F%B0%E7%9A%84%E6%95%B0%E6%8D%AE.png" alt="查看要传给后台的数据" style="zoom:67%;" />

  * 同样, 在header里也可以看到请求地址, 请求方法, 状态码等信息

  * 开始使用

    ```js
    //ajax
        //1. 创建ajax对象
    var xhr
    if (window.XMLHttpRequest){
        xhr = new  XMLHttpRequest();
    } else { // 兼容IE6, IE5---现已2021年了,作废吧
        xhr = new ActiveXObject("Microsoft.SMLHTTP");
    }
        //2. 设置请求地址及方式
    //第一个参数用于指定请求方式, 一般用大写
    //第二个参数代表请求的URL
    //第三个参数表示是否异步发送请求, 默认为true, 表示异步发送
    xhr.open("get" , "https://api/xdclass",true)
        //3. 发送请求(没有需要携带的参数时设为null, 有的话作为参数写入, 不填默认null)
    shr.send(null)
        //4. 等待浏览器返回结果接受响应
    /**
     * on readystate change事件
     *  readyState属性: 请求状态
     *      0   (初始化) 还没有调用open()方法
     *      1   (载入) 已调用send()方法, 正在发送请求
     *      2   (载入完成) send()方法完成, 已收到全部响应内容
     *      3   (解析) 正在解析响应内容
     *      4   (完成) 响应内容解析完成, 可以在客户端调用了
     */
    xhr.onreadystatechange = function() {
        if(xhr.readyState == 4) {
            //容错处理, 网络状态码, 200代码成功, 4XX代表客户端错误, 5XX代表服务器错误
            if(xhr.status == 200) {
                alert(xhr.responseText);//将相应转换成文本
            }else{
                alert('出错了, Err:' +xhr.status);
            }
        }
    }    
    
    ```

    

### js核心之DOM是什么

* DOM(w3c提出的一个标准)
  * DOM就是文档对象模型, 是一个抽象的概念
  * 定义了访问和操作HTML文档的方法

* HTML和txt文本的区别
  * HTML是有组织的结构化文件

* 什么是DOM树
  * 浏览器将结构化的文档以"树"的结构存储在浏览器内存里
  * 每个HTML元素被定义为节点
  * 这个节点有自己的属性(名称、类型、内容... ...)
  * 有自己的层级关系(parent, child, sibling)

* 图解DOM树
  * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/DOM%E6%A0%91%E5%9B%BE%E8%A7%A3.png" alt="DOM树图解" style="zoom:67%;" />



### 对DOM节点的创建、删除和插入

* 查找节点

  | 方法                                  | 描述                                |
  | ------------------------------------- | ----------------------------------- |
  | document.getElementById(id)           | 通过元素id来查找元素                |
  | document.getElementsByTagName(name)   | 通过标签名来查找元素                |
  | document.getElementsByClassName(name) | 通过类名来查找元素                  |
  | document.querySelector(selector)      | 通过css选择器选择元素, 无法选择伪类 |

  * getElementById(id)可直接返回标签内容, 如`<h1>alal<h1>`
  * getElementsByTagName(name)和getElementsByClassName(name)返回的是数组格式, 要获得内容需添加下标: getElementsByTagName(name)[0]

* 改变元素内容

  | 方法                                                         | 描述                  |
  | ------------------------------------------------------------ | --------------------- |
  | element.innerHTML = new html content  element代表获取到的对象 | 改变元素的 inner HTML |
  | element.attribute = new value  attribute代表属性名, 如title  | 改变HTML元素的属性值  |
  | element.setAttribute(attribute, value)                       | 改变HTML元素的属性值  |
  | element.style.property = new style  property代表css属性, 如backgroundColor | 改变HTML元素的样式    |

  

* 添加和删除元素

  | 方法                            | 描述         |
  | ------------------------------- | ------------ |
  | document.createElement(element) | 创建HTML元素 |
  | document.removeChild(element)   | 删除HTML元素 |
  | document.appendChild(element)   | 添加HTML元素 |
  | document.replaceChild(element)  | 替换HTML元素 |
  | document.write(text)            | 可写入HTML   |

  ```js
  var divObj = document.createElement('div')
  divObj.innerHTML = 123
  document.body.append(divObj)//在body的末尾添加节点
  document.write('<h1>12345</h1>')//在body的末尾添加节点
  ```

  

### DOM核心之结合事件对DOM进行操作

* 事件
  * 事件值的是在html元素上发生的事情
  * 比如图片元素被点击
  * 事件触发时, 可设置触发一段js代码, 事件触发后会执行这段js代码

* 常见的HTML事件

  | 事件        | 描述                       |
  | ----------- | -------------------------- |
  | onchange    | HTML元素已被改变           |
  | onclick     | 用户点击了HTML元素         |
  | onmouseover | 用户把鼠标移动到HTML元素上 |
  | onmouseout  | 用于把鼠标移开HTML元素     |
  | onkeydown   | 用户按下键盘按键           |
  | onload      | 浏览器已经完成页面加载     |

* 怎么对事件作出反应

  * 通过元素的事件属性----不利于维护

    ```html
    <h1 onclick="test()">lalala</h1>
    ```

  * 启用事件监听器

    * 什么是事件监听器

      * `addEventListener`给DOM对象添加事件处理程序

        ```js
        var h1Obj = document.getElementById('title')
        h1Obj.addEventListener('click', function() {
            
        })
        ```

        

      * `removeEventListener`删除给DOM对象的事件处理程序

* onclick和addEventListener的区别

  * onclick会被覆盖
    * 通过为对象添加onclick方法可以覆盖通过标签元素事件属性添加的onclick()

  * addEventListener可以同时注册多个(比如你为同一对象注册了10个点击事件), 根据注册顺序, 先后执行



### 深度剖析JS中事件的一些机制

* 事件传播的两种机制
  * 冒泡
  * 捕获

* 图解事件捕获和事件冒泡---默认采用冒泡

  <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/%E4%BA%8B%E4%BB%B6%E6%8D%95%E8%8E%B7%E5%92%8C%E4%BA%8B%E4%BB%B6%E5%86%92%E6%B3%A1.png" alt="事件捕获和事件冒泡" style="zoom:67%;" />

* 什么是事件代理

  * 思考: 父级那么多子元素, 怎么区分事件本应该是哪个子元素的 ?

    ```js
    list.addEventListener('click', function(e){//e只是一个形参
        //通过e.target可以知悉是哪个子元素触发了事件,target内的textContent就是这个子元素对应的序号(下标)
    },true)
    ```

    

* 怎么取消冒泡或者捕获

  ```js
  event.stopPropagation();
  //例子:
  child.addEventListener('click', function(e){//e只是一个形参
      e.stopPropagation();
  })
  ```

  * 拓展方法

    ```js
    //阻止元素行为, 例如a标签的链接跳转
    event.preventDefault()
    ```

    

### js中的定时器

* 延迟执行

  ```js
  setTimeout(function,毫秒);
  ```

  * 停止

    ```js
    clearTimeout(id)//参数必须是有setTimeout()返回的ID值
    ```

    

* 定时执行

  ```js
  setInterval(function,毫秒)
  ```

  * 停止

    ```js
    clearInterval(id)//参数必须是由setInterval()返回的ID值
    ```

    

```js
//案例
	//定时执行
var timer2 = setInterval(function() {
    
},200)
	//延时执行
var timer = setTimeout(function() {
    clearInterval(timer2)//清除定时执行
},2000)
```



### JavaScript核心之Bom

**BOM基础之BOM的概念及内置对象**

* 什么是BOM
  * 浏览器对象模型 ( Browser Object Model )

* 内置对象
  * window
    * 一切调用都发生在window下, 甚至可以说js的运行环境就是整个window
  * screen
    * 它代表的就是客户端的屏幕
  * loaction
    * 刷新操作   location.reload()
    * 跳转页面  location.href = 'http://....'     也可通过location.href获取当前地址栏上的路径
  * history
    * 浏览器对它的支持程度不很好, 尽量少用



### BOM基础之js弹出框

**无论哪种弹出框都会阻断程序运行**

* 警告框

  ```js
  alert(hello)//返回值是undefined
  ```

* 确认框

  ```js
  var isConfirm = confirm('请确认')
  console.log('下一步',isConfirm)
  //点击取消会返回false, 点击确认会返回true
  ```

* 提示框

  ```js
  var isPrompt = prompt('请输入姓名')
  console.log(isPrompt)//点击取消返回null, 点击确认返回用户输入的内容
  ```

  

  

### 浏览器基本概念之Cookie

* 浏览器中
  * 请求是无状态的
  * 比如进入一个网站, 根据传参, 网站的后台会告诉浏览器谁谁谁登录了

* 什么是Cookie

  * Cookie是计算机上存储浏览器的数据用的

  * 容量大小约4KB

  * 基本语法

    ```js
    document.cookie
    ```

    

* 为什么存在Cookie
  * 浏览器关闭后, 服务器会忘记用户的一切
  * 让浏览器记住用户信息

* cookie操作

  * 如何创建和读取cookie

    ```js
    //通过Document对象
    document.cookie="username=Nick; expires=Thu, 18 Dec 2043 12:00:00 GMT";
    ```

  * 删除cookie

    ```js
    //设置过期时间   --只要将过期时间设为以前的时间就可以了, 或者直接将cookie设为null也可以
    document.cookie="username; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;"
    ```

  *  上诉写法太复杂, 实际一般采用封装cookie函数的方法

    ```js
    function setCookie(cname,cvalue){
        var d = new Date();
        d.setTime(d.getTime()+(exdays*24*60*60*1000));
        var expires = "expires="+d.toGMTString(); //日期格式的字符串
        document.cookie = cname+"="+cvalue+"; "+expires;
    }
    function getCookie(cname){
        var name = cname + "=";
        var ca = document.cookie.split(';');//将字符串以 ; 分割成数组
        for(var i=0;i<ca.length; i++){
            var c = ca(i).trim();//把多与空格和回车删掉
            if(c.indexOf(name)==0){
                return c.substring(name.length, c.length);//返回结果
            }
        }
        return "";
    }
    //cookie函数封装方法有多种, 可灵活百度参照其他封装方法, 再自行修改
    ```

    

### 总结

* 课程总结

  * ECMAScript(js语法标准)

    * 原型
      * typeof和instanceof的区别

    * 内置对象---api数量非常多,靠积累
      * String
      * Array
      * Object
      * Date

    * 建议
      * 发现问题, 优先自己解决
      * 百度搜索越简短越好, 动宾结构即可. 例如:  分割字符串 mdn
      * 博文作为参考, 核心是看标准 (mdn)
      * 多实战

  * DOM
    * 记忆性知识, 多使用即可

  * BOM
    * 记忆性知识, 多使用即可

* 规划

  * JavaScript ----深度发展
    * Vue(MVVM)
    * React
    * Angular
      * 三个框架选一个深入
      * 不用丧失原生js能力
      * 空闲时间看点源码
        * 看他的插件是怎么封装的
        * 看他插件的方法是怎么实现的

  * webpack  -----广度发展
    * 项目构建和优化必备

  * 小程序
  * 后台
    * node 

  * App
    * UNI - App
    * React Native (RN)



### 解决问题思路

* 项目代码:  看日志、找核心定位
* 中间件框架: 进官网、github->issue (会有很多人提问以及很多热心的开发人员解答)



其他:  论坛如 csdn、stackoverflow(国外)

* 多充电

