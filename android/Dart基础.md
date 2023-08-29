# Dart基础

## 入口方法main

定义方法I

```dart
main() {
  print('你好 dart');
  print('你好 dart1');
} 
```

定义方法II  表示main方法没有返回值

```dart
void main() {
  print('你好 dart');
  print('你好 dart1');
}
```

## 数据类型

弱类型语言 直接var 也有String int等  有类型校验

```dart 
void main() {

  var str = 'Hello dart!';
  var num = 1234;
  print(str);
  print(num);

}
```

## 命名规则

1. 变量名称必须由数字、字母、下划线和$组成
2. 标识符不能以数字开头
3. 不能是保留字和关键字 
4. 变量名区分大小写
5. 语义性

## 常量

const== 值不变 定义时赋值==

final可以不赋值 只能赋一次 运行时的常量 还是惰性常量 运行时第一次使用前才初始化

## 常用数据类型

**int** 

**double** 

num 数字类型 , 其有两个子类 , int 和 double 类型  既可以接受 整型变量 , 又可以接受浮点型变量

abs() 

toInt() 

toDouble() 

toString() 

**String** 

```dart
//定义不区分单双引号  三个单引号/双引号可以跨行写

void main() {

  String str2 = '''nihao
  123
  
  
  456
  789''';

  print(str2);
}
//拼接

void main() {
  String str1 = 'Hello';  
  String str2 = 'Dart!';  
  print('$str1 $str2');
  print("$str1 $str2");
  print(str1+ " "+ str2);
}
```

**bool** true/false

**List** 

```dart
void main() {
  //定义方法I
  var l1 = [1,2,3];
  //定义方法II
  var l2 = new List();
  //定义方法III 已知数组类型
  var l3 = new List<String>();
  l2.add(4);
  l2.add(5);
  l3.add('123');
  l3.add('456');
  print(l1);
  print(l2);
  print(l3);
}
```

**Maps**

```dart
void main() {
  //定义方法I
  var person = {
    'name' : 'mike',
    'age' : 12,
    'work': ["程序员","外卖员"]
  };

  //定义方法II
  var person2 = new Map();

  person2['name'] = 'john';
  person2['age'] = 34;
  person2["work"] = ["程序员","外卖员"];

  print(person);
  print(person2);
  print(person['name']);
  print(person2['name']);
  print(person['work']);
  print(person2['work']);

}
```

**Runes** UTF-32编码的字符串 

**Symbol** 在程序中声明的运算符或者标识符 用#开头来表示 

### 判断数据类型

is关键词

```dart
void main() {
  var str = 1234.2;

  if(str is String) {
    print("是String");
  } else if (str is int){
    print("是int");
  } else {
    print("是其他");
  }
}
```

## 运算符

1. 算术运算符    +   - * / %  ~/取整

2. 关系运算符   == != > < >= <=

3. 逻辑运算符

   ！ 取反

   && 并且

   || 或者

4. 赋值运算符

    ① 基础赋值运算符

    = 直接赋值

    ??= b??= 23 //表示如果b为空的话 23赋值给b

   ```dart
   void main() {
   
     int b ;
     b ??= 23;
     print(b); 
   
   }
   ```

   ② 复合赋值运算符

    += -= *= /= %= ~/=

5. 三目运算符

   a?b:c

6. ??运算符

   ```dart
   void main() {
     var a; 
     var b = a ?? 10;
     print(b);
   
     a = 23;
     b = a ?? 10;
     print(b);
   }
   ```

## 类型转换

### number与String类型转换

```dart
num.toSring() //number -- String  
int.parse(str) //String  --  int
double.parse(str) //String  --  double
//类型转换出错用try catch接
try {  

} catch(err) {

}
```

### 其他类型转化成bool类型

str.isEmpty //判断字符串是否为空 true空 false否

num.isNaN //判断是否为非数字 true空 false否

## List Set Map forEach

### List

#### 属性

length

reversed

```dart
void main() {
  List myList = ['apple','orange','watermelon'];
  //非集合
  print(myList.reversed);
  print(myList.reversed.toList());
}
```

#### 方法

1. 增加数据

   ```dart
   .add(value);  //增加一个数据
   .addAll(arr);  //拼接数组
   void main() {
     List myList = ['apple','orange','watermelon'];
     print(myList);
     myList.add('grape');
     print(myList);
     myList.addAll(['peach','banana']);
     print(myList);
     List myList2 = ['lemon'];
     myList.addAll(myList2);
     print(myList);
   }
   ```

2. 判空

   isEmpty

   isNotEmpty

3. 查找数据

   ```dart
   list.indexOf('name');
   void main() {
     List myList = ['apple','orange','watermelon'];
     print(myList.indexOf('apple'));  //查找到返回索引值
     print(myList.indexOf('apple2'));  //查不到返回-1
   }
   ```

4. 删除数据

   list.remove("name")   //按照值删除

   list.removeAt(index)  //按照索引删除

5. 修改数据

   fillRange

   ```dart
   void main() {
     List myList = ['apple','orange','watermelon'];
     myList.fillRange(1, 3,'aaa');
     print(myList);
   }
   ```

6. 插入数据

   list.insert(index,value)  //在指定下标位置插入一个数据

   list.insertAll(index,arry) //在指定下标位置插入一个数组

7. 和String之间的转换

   list.join(",") //list转换为字符串 用，分割开 

   ```dart
   void main() {
     List myList = ['apple','orange','watermelon'];
     print(myList.join(","));
   }
   ```

   ![image-20201230151548438](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20201230151548438.png)

   字符串转换为list

   arr.split("-")  //根据-切割字符串为数组

   ```dart
   void main() {
     var str = "apple,orange,watermelon";
     print(str.split(","));
   }
   ```

   ![image-20201230151819203](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230151819203.png)

### Set

没有顺序且不能重复的集合，不能通过索引获取值

功能：去除数组重复内容

```dart
void main() {
  //第一种赋值方式
  var s = new Set();
  List myList = ['apple','orange','watermelon','orange','peach'];
  s.add("banana");
  s.add("apple");
  s.add("apple");
  print(s);
  print(s.toList());

  //第二种赋值方式
  s.addAll(myList);
  print(s);
  print(s.toList());
}
```

![image-20201230152623955](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230152623955.png)

### Map

无序的键值对

```dart
void main() {
  //方法1
  var person = {
    'name' : 'Mike',
    'age' : 12,
    'work': ["程序员","外卖员"]
  };
  //方法2
  var person2 = new Map();
  person2["name"] = 'John';
  //方法3
  Map person3 = {
    'name' : 'Bob',
    'age' : 45,
    'work': ["程序员","外卖员"]
  };
  print(person);
  print(person2);
  print(person3);
}
```

![image-20201230153139199](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230153139199.png)

#### 属性

keys  // myMaps.keys --- key的所有值 myMaps.keys.toList() 可以转化为数组

values   // myMaps.values   --- value的所有值 myMaps.values.toList() 可以转化为数组

isEmpty

isNotEmpty

#### 方法

1. 增加属性

   myMaps.addAll(addMaps);

2. 删除属性

   myMaps.remove("key");

3. 查找value值

   myMaps.containsValue(value);

   myMaps.containsKey(key);

```dart
void main() {
  var person = {
    'name' : 'Mike',
    'age' : 12,
    'work': ["程序员","外卖员"]
  };
  person.addAll({
    'sex':"man",
    'height': 160
  });
  print(person);
  person.remove('sex');
  print(person);
  print(person.containsValue('Mike'));
  print(person.containsKey('sex'));

}
```

![image-20201230155908676](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230155908676.png)

### forEach等循环方法

1. for(::)
2. for(var item in myList)
3. list.forEach

```dart
void main() {
  //数组forEach
  List myList = ['apple','orange','watermelon'];
  myList.forEach((element) {
    print("$element");
  });

  //map
  var person = {
    'name' : 'Mike',
    'age' : 12,
    'work': ["程序员","外卖员"]
  };
  person.forEach((key, value) {
    print("$key -- $value");
  });
}
```

![image-20201230155837481](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230155837481.png)

4. map  //修改集合数据

```dart
void main() {
  List myList = [1,3,5];
  
  var newList = myList.map((e) => e*2);
  print(newList.toList());
}
```

![image-20201230155735001](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230155735001.png)

5. where  //寻找集合中满足where条件的集合组成新的集合

```dart
void main() {
  List myList = [1,3,5,7,8,9];
  
  var newList = myList.where((element) => element > 5);
  print(newList.toList());
}
```

![image-20201230155702993](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230155702993.png)

6. any  //寻找集合中是否存在满足给定any子句中条件的数据，返回相应bool值

```dart
void main() {
  List myList = [1,3,5,7,8,9];
  var newList = myList.any((element) => element > 10);
  print(newList);
}
```

![image-20201230160149949](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230160149949.png)

7. every  //判断集合中是否每一个值都满足给定every子句中条件的数据，返回相应bool值

```dart
void main() {
  List myList = [1,3,5,7,8,9];
  var newList = myList.every((element) => element > 4);
  print(newList);
}
```

![image-20201230160335100](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230160335100.png)

## 函数

### 内置方法

print()

### 自定义方法

方法定义可以放在main函数里面或者外面 放在外面是绝对函数

返回类型 方法名 （参数,[可选参数]） {   //可在此初始化参数表示默认参数

方法体

return 返回值

}

```dart
void printInfo() {
  print("自定义方法");
}
void main() {
  printInfo();
}
```

 **命名参数**

```dart
String printUserInfo(String username, {int age,String sex = '男'}) {
  if(age != null) {
    return "姓名：$username---性别：$sex---年龄：$age";
  } 
  return  "姓名：$username---性别：$sex---年龄保密";
}
void main() {
  print(printUserInfo('张三',age:20,sex:'未知'));
}
```

![image-20201230164215793](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230164215793.png)

**方法做参数**

```dart
fn1() {
 print("fn1");
}

fn2(fn) {
 fn();
}

void main() {
 fn2(fn1);
}
```

![image-20201230170433729](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230170433729.png)

### 箭头函数

```dart
void main() {
  List myList = ['apple','orange','watermelon'];
  //第一种
  myList.forEach((element) => print(element));
  //第二种
  myList.forEach((element) => {
    print(element)  //不能写分号，只能写一句话
  });
  List myNumList = [1,2,3,4,5,6,7,8];
  var newList = myNumList.map((e) => e > 4? e*2:e);
  print(newList.toList());
}
```

![image-20201230170349234](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230170349234.png)

### 匿名方法

可以在main函数的外面或者里面

```dart
var fn=() {
 print("fn");
};

void main() {
 fn();
}
```

![image-20201230170504936](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230170504936.png)

### 自执行方法



```dart
void main() {
  ((int n) {
    print(n);
    print("自执行方法");
  })(12);
}
```

![image-20201230170850689](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230170850689.png)

### 闭包

全局变量特点：常驻内存，污染全局

局部变量特点：不常驻内存，会被垃圾回收，不会污染全局

闭包：常驻内存，不污染全局

闭包写法： 函数嵌套函数，并return里面的函数，形成闭包

```dart
fn() {
  var a = 123;
  return () {
    a++;
    print(a);
  };
}
void main() {
  var b = fn();
  b();
  b();
  b();
}
```

![image-20201230171451056](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201230171451056.png)

## Dart中的类与对象

Dart是一门使用类和单继承的面向对象语言 类似于java

### 构造函数

**注意：**

1. 构造函数  只能有一个
2. 可以利用可选参数实现函数重载
3. 简写的构造函数
4. 命名构造函数  可定义多个

```dart
class Person {
  //属性
  String name = '张三';
  int age = 23;
  //方法

  // //构造函数  只能有一个
  // Person() {
  //   print("无参构造函数，在实例化的时候触发");
  // }
  //利用可选参数实现函数重载
  Person([String name,int age]) {  
    if(name != null) {
      this.age = age;
      this.name = name;
      print("有参构造函数");
    } else {
        print("无参构造函数，在实例化的时候触发");
    }
  }
  //简写的构造函数
  // Person(this.name,this.age);
  void getInfo() {
    // print("$name---$age");
    print("${this.name}---${this.age}");  //推荐
  }
  void setInfo(int age) {
    this.age = age;
  }
  //命名构造函数  可定义多个
  Person.now() {
    print("我是命名构造函数");
  }
}
void main() {
  //实例化
  Person p1 = new Person();
  Person p2 = new Person("John",34);
  Person p3 = new Person.now();
  
  print(p1.name);
  p1.getInfo();
  p2.getInfo();
  p3.getInfo();

  p1.setInfo(12);
  p1.getInfo();
}
```

对应的类可以单独抽离出一个文件

![image-20201231101733245](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231101733245.png)

### 私有属性和方法

Dart中没有public等访问修饰符，默认为公有，但是可以使用_把一个属性或者方法定义为私有，但是需要把需要设置的类抽离成文件

Animal.dart中

```dart
class Animal{
  //私有属性
  String _name;
  String category;

  Animal(this._name,this.category);
  void printInfo() {
    print("$_name---$category");
  }
  //私有方法
  void _run() {
    print("私有方法");
  }
  void excRun() {
    this._run();
  }
}
```

index.dart

```dart
import 'lib/Animal.dart';
void main() {
  //实例化
  Animal a1 = new Animal("猫","猫科");
  
  // print(a1._name);
  print(a1.category);
  a1.printInfo();
  // a1.run();
  a1.excRun();
}
```

![image-20201231103740060](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231103740060.png)

![image-20201231103759985](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231103759985.png)

### getter和setter

```dart
class Rectangle {
  double width;
  double height;

  Rectangle(this.width,this.height);

  get area {
    return this.height*this.height;
  }

  set areaHeight(height) {
    this.height = height;
  }
}

void main() {
  //实例化
  Rectangle r1 = new Rectangle(2,4);
  
  print("area: ${r1.area}");

  r1.areaHeight = 5.0;
  print("area: ${r1.area}");

}
```

### 初始化列表

```dart
class Rectangle {
  double width;
  double height;
    //在实例化之前，先赋值 再实例化
  Rectangle():height = 2,width =10 {
      
  };
  get area {
    return this.height*this.height;
  }

  set areaHeight(height) {
    this.height = height;
  }
}
```

## 静态成员与继承

### 静态成员与静态方法

使用static关键字，静态方法不能访问非静态成员，反之则可以

```dart
class StaticPerson {
  static String name = "John";
  static void show() {
    print(name);
  }
}
void main() {
  //实例化
  StaticPerson p1 = new StaticPerson();
  StaticPerson.show();
  print(StaticPerson.name);
}
```

![image-20201231111909026](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231111909026.png)

### 对象操作符

#### 条件运算符？

判断对象是否为空，如果为空 不进行操作，不为空则继续进行

```dart
class Person {
  String name;
  num age;
  Person(this.name,this.age);
  void printInfo() {
    print("${this.name}---${this.age}");  
  }
}

main(){ 
  Person p;
  p?.printInfo();  //不可以打印出
    
  Person p=new Person('张三', 20);
  p?.printInfo();  //可以打印
}
```



#### 类型转换 as

强制转化为类

(p1 as Person).printInfo();

#### 类型判断 is

if(p is person)

#### ==级联操作(连缀)..==

 ```dart
   Person p1=new Person('张三1', 20);

   p1.printInfo();

   p1..name="李四"
     ..age=30
     ..printInfo();
 ```

### 简单继承

1. 子类使用extends关键词来继承父类

2. 子类会继承父类里面可见的属性和方法，但**不会继承构造函数**

3. 子类能重写父类的方法getter和setter

```dart
class Person {
  String name='张三';
  num age=20; 
  void printInfo() {
    print("${this.name}---${this.age}");  
  } 
}
class Web extends Person{

}

main(){   

  Web w=new Web();
  print(w.name);
  w.printInfo();
 
}
```

### super

```dart
class Person {
  String name;
  num age; 
  Person(this.name,this.age);
  Person.xxx(this.name,this.age);  //命名函数
  void printInfo() {
    print("${this.name}---${this.age}");  
  }
}

class Web extends Person{
  String sex;
  Web(String name, num age,String sex) : super.xxx(name, age){   //通过命名参数传参
    this.sex=sex;
  }
  run(){
   print("${this.name}---${this.age}--${this.sex}");  
  }
}

main(){ 

  // Person p=new Person('李四',20);
  // p.printInfo();

  // Person p1=new Person('张三',20);
  // p1.printInfo();

  Web w=new Web('张三', 12,"男");
  w.printInfo();
  w.run();
}
```

### 重写父类方法

```dart
class Person {
  String name;
  num age; 
  Person(this.name,this.age);
  void printInfo() {
    print("${this.name}---${this.age}");  
  }
  work(){
    print("${this.name}在工作...");
  }
}

class Web extends Person{
  Web(String name, num age) : super(name, age);

  run(){
    print('run');
  }
  //覆写父类的方法
  @override       //可以写也可以不写  建议在覆写父类方法的时候加上 @override 
  void printInfo(){
     print("姓名：${this.name}---年龄：${this.age}"); 
  }
  @override
  work(){
    print("${this.name}的工作是写代码");
  }

}

main(){ 

  Web w=new Web('李四',20);
  w.printInfo();
  w.work();
}
```

### 子类中调用父类的方法

用super.来实现

```dart
class Person {
  String name;
  num age; 
  Person(this.name,this.age);
  void printInfo() {
    print("${this.name}---${this.age}");  
  }
  work(){
    print("${this.name}在工作...");
  }
}

class Web extends Person{
  Web(String name, num age) : super(name, age);

  run(){
    print('run');
    super.work();  //自类调用父类的方法
  }
}


main(){ 

  Web w=new Web('李四',20);
  w.run();
}
```

## 抽象类、多态以及接口

### 抽象类

Dart中抽象类: Dart抽象类主要用于定义标准，子类可以继承抽象类，也可以实现抽象类接口。

 1、抽象类通过abstract 关键字来定义

 2、Dart中的抽象方法不能用abstract声明，Dart中没有方法体的方法我们称为抽象方法。

 3、如果子类继承抽象类必须得实现里面的抽象方法

 4、如果把抽象类当做接口实现的话必须得实现抽象类里面定义的所有属性和方法。

 5、抽象类不能被实例化，只有继承它的子类可以

**==extends抽象类 和 implements的区别==**：

 1、如果要复用抽象类里面的方法，并且要用抽象方法约束自类的话我们就用extends继承抽象类

 2、如果只是把抽象类当做标准的话我们就用implements实现抽象类

```dart
abstract class Animal{
  eat();   //抽象方法
  run();  //抽象方法  
  printInfo(){
    print('我是一个抽象类里面的普通方法');
  }
}

class Dog extends Animal{
  @override
  eat() {
     print('小狗在吃骨头');
  }

  @override
  run() {
    // TODO: implement run
    print('小狗在跑');
  }  
}
class Cat extends Animal{
  @override
  eat() {
    // TODO: implement eat
    print('小猫在吃老鼠');
  }

  @override
  run() {
    // TODO: implement run
    print('小猫在跑');
  }

}

main(){

  Dog d=new Dog();
  d.eat();
  d.printInfo();
  Cat c=new Cat();
  c.eat();
  c.printInfo();
  // Animal a=new Animal();   //抽象类没法直接被实例化

}
```

### 多态

Datr中的多态：

1. 允许将子类类型的指针赋值给父类类型的指针, 同一个函数调用会有不同的执行效果 。

2.  子类的实例赋值给父类的引用。

3. 多态就是父类定义一个方法不去实现，让继承他的子类去实现，每个子类有不同的表现。

```dart
abstract class Animal{
  eat();   //抽象方法 
}

class Dog extends Animal{
  @override
  eat() {
    print('小狗在吃骨头');
  }
  run(){
    print('run');
  }
}
class Cat extends Animal{
  @override
  eat() {   
    print('小猫在吃老鼠');
  }
  run(){
    print('run');
  }
}

main(){

  Animal d=new Dog();
  d.eat();
  // d.run()  //没有run方法

  Animal c=new Cat();
  c.eat();

}
```

### 接口

和Java一样，dart也有接口，但是和Java还是有区别的。

1.  首先，dart的接口**没有interface**关键字定义接口，而是普**通类或抽象类都可以作为接口**被实现。

2. 同样使用**implements关键字**进行实现。

3. 但是dart的接口有点奇怪，**如果实现的类是普通类，会将普通类和抽象中的属性的方法全部需要覆写一遍**。

4. 而因为抽象类可以定义抽象方法，普通类不可以，所以一般如果要实现像Java接口那样的方式，一般会使用抽象类。

5.  **建议使用抽象类定义接口**。

```dart
//Db.dart
abstract class Db{   //当做接口   接口：就是约定 、规范
    String uri;      //数据库的链接地址
    add(String data);
    save();
    delete();
}
//MsSql.dart
import 'Db.dart';
class MsSql implements Db{
  @override
  String uri;
  @override
  add(String data) {
    print('这是mssql的add方法'+data);
  }

  @override
  delete() {
    // TODO: implement delete
    return null;
  }

  @override
  save() {
    // TODO: implement save
    return null;
  }
}
//MySql.dart
import 'Db.dart';
class Mysql implements Db{
  
  @override
  String uri;

  Mysql(this.uri);

  @override
  add(data) {
    // TODO: implement add
    print('这是mysql的add方法'+data);
  }

  @override
  delete() {
    // TODO: implement delete
    return null;
  }

  @override
  save() {
    // TODO: implement save
    return null;
  }

  remove(){
      
  }
}
//index.dart
import 'lib/Mysql.dart';
import 'lib/MsSql.dart';

main() {

  Mysql mysql=new Mysql('xxxxxx');
  mysql.add('1243214');
  MsSql mssql=new MsSql();
  mssql.uri='127.0.0.1';
  mssql.add('增加的数据');

}
```

## 一个类实现多个接口以及mixins

### 一个类实现多个接口

注意实现多个接口要将接口中所有方法都是先

```dart
abstract class A{
  String name;
  printA();
}

abstract class B{
  printB();
}

class C implements A,B{  
  @override
  String name;  
  @override
  printA() {
    print('printA');
  }
  @override
  printB() {
    // TODO: implement printB
    return null;
  }
}
```

### mixins

mixins的中文意思是混入，就是在类中混入其他功能。

在Dart中可以使用mixins实现**类似多继承**的功能

因为mixins使用的条件，随着Dart版本一直在变，这里讲的是Dart2.x中使用mixins的条件：

 1、作为mixins的类只能继承自Object，**不能继承其他类**

 2、作为mixins的类**不能有构造函数**

 3、一个类**可以mixins多个mixins类**

 4、mixins绝不是继承，也不是接口，而是一种**全新的特性**

```dart
 class Person{
  String name;
  num age;
  Person(this.name,this.age);
  printInfo(){
    print('${this.name}----${this.age}');
  }
  void run(){
    print("Person Run");
  }
}

class A {
  String info="this is A";
  void printA(){
    print("A");
  }
  void run(){
    print("A Run");
  }
}

class B {  
  void printB(){
    print("B");
  }
  void run(){
    print("B Run");
  }
}

class C extends Person with B,A{
  C(String name, num age) : super(name, age);
  
}

void main(){  
  var c=new C('张三',20);  
  c.printInfo();
  // c.printB();
  // print(c.info);

   c.run();  //按照声明顺序 所以运行A的方法
}
```

**mixins的类型**

```dart
class A {
  String info="this is A";
  void printA(){
    print("A");
  }
}

class B {
  void printB(){
    print("B");
  }
}

class C with A,B{
  
}

void main(){  
  var c=new C();  
  print(c is C);    //true  B和A是C的超类
  print(c is A);    //true
  print(c is B);   //true
  // var a=new A();
  // print(a is Object);
}
```

## 泛型

泛型就是解决 类 接口 方法的复用性、以及对不特定数据类型的支持(类型校验)

### 泛型方法

```dart
getData<T>(T value){
   return value;
}

void main(){
    print(getData<int>(12));
}

```

### 泛型类

List就是泛型类

```dart
class PrintClass<T>{  
      List list=new List<T>();
      void add(T value){
          this.list.add(value);
      }
      void printInfo(){          
          for(var i=0;i<this.list.length;i++){
            print(this.list[i]);
          }
      }
}

main() {  
  PrintClass p=new PrintClass<int>();  
  p.add(12);
  p.add(23);
  p.printInfo();

}
```

### 泛型接口

 ```dart
abstract class Cache<T>{
  getByKey(String key);
  void setByKey(String key, T value);
}

class FlieCache<T> implements Cache<T>{
  @override
  getByKey(String key) {    
    return null;
  }

  @override
  void setByKey(String key, T value) {
   print("我是文件缓存 把key=${key}  value=${value}的数据写入到了文件中");
  }
}

class MemoryCache<T> implements Cache<T>{
  @override
  getByKey(String key) {   
    return null;
  }

  @override
  void setByKey(String key, T value) {
       print("我是内存缓存 把key=${key}  value=${value} -写入到了内存中");
  }
}
void main(){
     MemoryCache m=new MemoryCache<Map>();
     m.setByKey('index', {"name":"张三","age":20});
}
 ```

## 库

### Dart中的库

在Dart中，库的使用时通过import关键字引入的。

library指令可以创建一个库，每个Dart文件都是一个库，即使没有使用library指令来指定。

Dart中的库主要有三种：

  1、我们自定义的库   

​     import 'lib/xxx.dart';

  2、系统内置库    

​     import 'dart:math';  

​     import 'dart:io'; 

​     import 'dart:convert';

  3、Pub包管理系统中的库 

​    https://pub.dev/packages

​    https://pub.flutter-io.cn/packages

​    https://pub.dartlang.org/flutter/

​    1、需要在自己项目根目录新建一个pubspec.yaml

​    2、在pubspec.yaml文件 然后配置名称 、描述、依赖等信息

​    3、然后运行 pub get 获取包下载到本地 

​    4、项目中引入库 import 'package:http/http.dart' as http; 看文档使用

### 导入系统内置库 math库

```dart
import "dart:math";
main(){
 
    print(min(12,23));
    print(max(12,25));
  
}
```

### 实现请求数据httpClient

```dart
import 'dart:io';
import 'dart:convert';


void main() async{
  var result = await getDataFromZhihuAPI();
  print(result);
}


//api接口： http://news-at.zhihu.com/api/3/stories/latest
getDataFromZhihuAPI() async{   //异步方法
  //1、创建HttpClient对象
  var httpClient = new HttpClient();  
  //2、创建Uri对象
  var uri = new Uri.http('news-at.zhihu.com','/api/3/stories/latest');
  //3、发起请求，等待请求
  var request = await httpClient.getUrl(uri);
  //4、关闭请求，等待响应
  var response = await request.close();
  //5、解码响应的内容
  return await response.transform(utf8.decoder).join();
}
```

### Async和await

async和await

 这两个关键字的使用只需要记住两点：

 **只有async方法才能使用await关键字调用方法**

  **如果调用别的async方法必须使用await关键字**

  async是让方法变成异步。

  await是等待异步方法执行完成。

```dart
void main() async{
  var result = await testAsync();
  print(result);

}

//异步方法
testAsync() async{
  return 'Hello async';
}
```

### 引入第三方模块Pub包

pub包管理系统:

1、从下面网址找到要用的库

​    https://pub.dev/packages

​    https://pub.flutter-io.cn/packages

​    https://pub.dartlang.org/flutter/

2、创建一个pubspec.yaml文件，内容如下

  name: xxx

  description: A new flutter module project.

  dependencies: 

​    http: ^0.12.0+2

​    date_format: ^1.0.6

3、配置dependencies

4、运行pub get 获取远程库

5、看文档引入库使用

### 库的重命名以及冲突的解决

通过as关键字

```dart
import 'lib/Person1.dart';
import 'lib/Person2.dart' as lib;

main(List<String> args) {
  Person p1=new Person('张三', 20);
  p1.printInfo();
  lib.Person p2=new lib.Person('李四', 20);
  p2.printInfo();
}
```

### 库的部分导入

部分导入

 如果只需要导入库的一部分，有两种模式：

   模式一：只导入需要的部分，使用show关键字，如下例子所示：

   import 'package:lib1/lib1.dart' show foo;

   模式二：隐藏不需要的部分，使用hide关键字，如下例子所示：

   import 'package:lib2/lib2.dart' hide foo;  

```dart
// import 'lib/myMath.dart' show getAge;
import 'lib/myMath.dart' hide getName;

void main(){
//  getName();
  getAge();
}
```

### 延迟加载

延迟加载

  也称为懒加载，可以在需要的时候再进行加载。

  懒加载的最大好处是可以减少APP的启动时间。

  懒加载使用deferred as关键字来指定，如下例子所示：

  import 'package:deferred/hello.dart' deferred as hello;

  当需要使用的时候，需要使用loadLibrary()方法来加载：

```dart
greet() async {
   await hello.loadLibrary();
   hello.printGreeting();
}
```



## 代码风格

### 命名规范

大驼峰：

Classes（类名）、 enums（枚举类型）、 typedefs（类型定义）、以及 type parameters（类型参数）扩展名

单词间用下划线隔开：

要 在库，包，文件夹，源文件中使用

小驼峰：

其他标识符、常量、包括枚举的值

### 顺序

 要把 “dart:” 导入语句放到其他导入语句之前。

要 把 “package:” 导入语句放到项目相关导入语句之前。

要把导出（export）语句作为一个单独的部分放到所有导入语句之后。

要 按照字母顺序来排序每个部分中的语句。

例：

```dart
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'util.dart';

export 'src/error.dart';
```