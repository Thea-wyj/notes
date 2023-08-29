# Flutter基础

Flutter 是谷歌公司基于谷歌的dart 语言开发的一款开源、免费的移动UI 框架，可以让我们快速的在Android 和iOS 上构建高质量App。它最大的特点就是跨平台、以及高性能。

Flutter 是谷歌基于Dart 语言开发的一款跨平台的移动App 开发框架。它针对的开发者是全部开发者。

## 目录结构

![image-20201231161811255](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231161811255.png)

## Flutter 入口文件、入口方法

每一个flutter 项目的lib 目录里面都有一个main.dart 这个文件就是flutter 的入口文件.

其中的main 方法是dart 的入口方法。runApp 方法是flutter 的入口方法。

```dart
void main(){
runApp(MyApp());
}
//也可以简写
void main()=>runApp(MyApp());
```

## 自定义组件

在Flutter 中自定义组件其实就是一个类，这个类需要继承StatelessWidget/StatefulWidget

StatelessWidget 是**无状态**组件，状态不可变的widget
	   StatefulWidget 是**有状态**组件，持有的状态可能在widget 生命周期改变

```dart
import 'package:flutter/material.dart';
void main(){
	runApp(MyApp());
}
class MyApp extends StatelessWidget{
	@override
	Widget build(BuildContext context) {
		// TODO: implement build
		return Center(
			child: Text(
			"我是一个文本内容",
			textDirection: TextDirection.ltr,
			),
		);
	}
}
```



## 官方组件

### MaterialApp 组件

MaterialApp 是一个方便的Widget，它封装了应用程序实现Material Design 所需要的一些Widget。一般作为顶层widget 使用。

常用的属性：
home（主页）
title（标题）
color（颜色）
theme（主题）
routes（路由）
...

### Scaffold组件

Scaffold 是Material Design 布局结构的基本实现。此类提供了用于显示drawer、snackbar 和底部sheet 的API。
Scaffold 有下面几个主要属性：
appBar - 显示在界面顶部的一个AppBar。
body - 当前界面所显示的主要内容Widget。
drawer - 抽屉菜单控件。
...

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Demo'),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
        primarySwatch: Colors.amber
      ),
    );
  }
}
// 导航栏
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Center(child: new Text(
      'Hello Flutter!!',
      textDirection: TextDirection.ltr,
      style: TextStyle(
        fontSize: 40.0, //40px
        color: Color.fromRGBO(244, 233, 121, 0.5),
      ),
    ));
  }

}
```

### Container组件

![image-20201231182221521](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182221521.png)

![image-20201231182237774](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182237774.png)

![image-20201231182248112](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182248112.png)

更多参数：https://api.flutter.dev/flutter/widgets/Container-class.html

### Text组件

![image-20201231182009553](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182009553.png)

TextStyle 的参数：

![image-20201231182145527](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182145527.png)

![image-20201231182154074](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182154074.png)

更多参数：https://docs.flutter.io/flutter/painting/TextStyle-class.html

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hello Flutter!'),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
        primarySwatch: Colors.amber
      ),
    );
  }
}
// 导航栏
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Center(child: Container(
      child: Container(
        child: Text(
            "达拉崩吧斑多贝迪不多笔录翁",
          textAlign: TextAlign.center,
          textDirection: TextDirection.ltr,
          overflow: TextOverflow.ellipsis,
          textScaleFactor: 2.0,
          maxLines: 2,
          style: TextStyle(
            decoration: TextDecoration.underline,
            decorationColor: Colors.black54,
            decorationStyle: TextDecorationStyle.double,
            wordSpacing: 1,
            letterSpacing: 0.1,
            fontStyle: FontStyle.normal,
            fontSize: 13.0,
            color: Colors.amber,
            fontWeight: FontWeight.bold,
          ),
        ),
        alignment: Alignment.center,
        decoration: BoxDecoration(
          color: Colors.white,
          border: Border.all(
            color: Colors.black45,
            width: 2.0,
          ),
          borderRadius: BorderRadius.all(Radius.circular(9.0)),
        ),
        margin: EdgeInsets.all(20.0),
        padding: EdgeInsets.fromLTRB(20, 10, 5, 0),
        transform: Matrix4.rotationX(0.1),
        height: 200.0,
        width: 200.0,
      ),
    ),
    );
  }
  
}
```

![image-20201231182413996](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20201231182413996.png)

### 图片组件

Image.asset， 本地图片
	   Image.network 远程图片

常用属性：

![image-20210101134335471](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210101134335471.png)

![image-20210101134343634](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210101134343634.png)

更多属性参考：https://api.flutter.dev/flutter/widgets/Image-class.html

#### 引入本地图片

![image-20210101143054277](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210101143054277.png)

实例:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 图片
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Center(child: Container(
      child: Container(  /
        child: ClipOval(   //用ClipOval的方法实现圆形图片
        	child: Image.network("https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2386961669,3768175101&fm=26&gp=0.jpg",
             width: 150,
             height: 150,),
         ),
      ),
    ),
    );
  }

}
```

实现：

![image-20210101142741561](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210101142741561.png)

#### 网络图片

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 图片
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Center(child: Container(
      child: Container(  //用边框的形式实现圆形图片
        decoration: BoxDecoration(
          border: Border.all(
            color: Colors.black45,
          ),
          borderRadius: BorderRadius.circular(150),
          image: DecorationImage(
            image: new AssetImage('images/a.jpg'),
            fit: BoxFit.cover
          )
        ),
        width: 150,
        height: 150,
      ),
    ),
    );
  }

}
```

实现：

![image-20210101142438786](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210101142438786.png)

### 列表

列表有以下分类：
1、垂直列表
2、垂直图文列表
3、水平列表
4、动态列表
5、矩阵式列表

列表参数：

![image-20210101164939538](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210101164939538.png)

![image-20210101164958310](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210101164958310.png)

#### 基本列表

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Center(child: Container(
      child: ListView(
        children: <Widget>[
          ListTile(
            leading: Icon(Icons.phone),
            title: Text(
              "this is list",
               style: TextStyle(fontSize: 28),
            ),
            subtitle: Text("this is list this is list"),
          ),
          ListTile(
            title: Text("this is list"),
            subtitle: Text("this is list this is list"),
            trailing: Icon(Icons.phone),
          ),
          ListTile(
            title: Text("this is list"),
            subtitle: Text("this is list this is list"),
          ),
          ListTile(
            title: Text("this is list"),
            subtitle: Text("this is list this is list"),
          ),
          ListTile(
            title: Text("this is list"),
            subtitle: Text("this is list this is list"),
          ),
        ],
      )
    ),
    );
  }

}

```

实现：

![image-20210102150532290](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210102150532290.png)

#### 水平列表

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Center(child: Container(
      height: 200.0,
      margin: EdgeInsets.all(5),
      child: ListView(
        scrollDirection: Axis.horizontal, //水平列表
        children: <Widget>[
          Container(
            width: 180.0,
            color: Colors.red,
          ),
          Container(
            width: 180.0,
            color: Colors.orange,
            child: ListView(
              children: <Widget>[
                Image.network('https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fn.sinaimg.cn%2Fsinacn10108%2F600%2Fw1920h1080%2F20190220%2Fe09d-htfpvza3998118.jpg&refer=http%3A%2F%2Fn.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1612163827&t=793c41e10e9f9379a34cf65d807bc300'
                ),
                SizedBox(height: 16.0),
                Text('这是一个文本信息',
                    textAlign:TextAlign.center,
                  style: TextStyle(
                    fontSize: 16.0
                  ),
                )
              ],
            ),
          ),
          Container(
            width: 180.0,
            color: Colors.yellow,
          ),
          Container(
            width: 180.0,
            color: Colors.green,
          ),
          Container(
            width: 180.0,
            color: Colors.lightBlueAccent,
          ),
          Container(
            width: 180.0,
            color: Colors.blueAccent,
          ),
          Container(
            width: 180.0,
            color: Colors.purple,
          )
        ],
      )
    ),
    );
  }
}
```

实现：

![image-20210102151923268](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210102151923268.png)

#### 动态列表

1. 根据ListViewBuilder()动态生成列表

实例：

```Dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  List list = new List();
  HomeContent() {
    for(var i = 0; i< 20 ; i++) {
      list.add("这是第$i条数据");
    }
  }
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView.builder(
      itemCount: this.list.length,
      itemBuilder: (context,index) {
        return ListTile(
          leading: Icon(Icons.phone),
          title: Text("${list[index]}"),
        );
    },
    );
  }
}

```

实现：

![image-20210103032045817](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103032045817.png)

2. 根据ListViewBuilder动态生成已有列表

   实例：

   ```dart
   List listData=[
     {
       "title": 'Candy Shop',
       "author": 'Mohamed Chahin',
       "imageUrl": 'https://www.itying.com/images/flutter/1.png',
     },
     {
       "title": 'Childhood in a picture',
       "author": 'Google',
       "imageUrl": 'https://www.itying.com/images/flutter/2.png',
     },
     {
       "title": 'Alibaba Shop',
       "author": 'Alibaba',
       "imageUrl": 'https://www.itying.com/images/flutter/3.png',
     },
     {
       "title": 'Candy Shop',
       "author": 'Mohamed Chahin',
       "imageUrl": 'https://www.itying.com/images/flutter/4.png',
     },
     {
       "title": 'Tornado',
       "author": 'Mohamed Chahin',
       "imageUrl": 'https://www.itying.com/images/flutter/5.png',
     },
     {
       "title": 'Undo',
       "author": 'Mohamed Chahin',
       "imageUrl": 'https://www.itying.com/images/flutter/6.png',
     },
     {
       "title": 'white-dragon',
       "author": 'Mohamed Chahin',
       "imageUrl": 'https://www.itying.com/images/flutter/7.png',
     }
   
   ];
   ```

   

   ```dart
   import 'package:flutter/cupertino.dart';
   import 'package:flutter/material.dart';
   import 'package:flutter/widgets.dart';
   import 'res/ListData.dart';
   
   void main() {
     runApp(MyApp());
   }
   //自定义组件
   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return MaterialApp(
         home: Scaffold(
           appBar: AppBar(
             title: Text(
                 'Hello Flutter',
               textAlign: TextAlign.center,
             ),
           ),
           body: HomeContent(),
         ),
         theme: ThemeData(
             primarySwatch: Colors.amber
         ),
       );
     }
   }
   //导航栏 列表
   class HomeContent extends StatelessWidget {
   
     Widget _getListData(context,index) {
       return ListTile(
           leading:Image.network("${listData[index]["imageUrl"]}"),
           title: Text("${listData[index]["title"]}"),
           subtitle: Text("${listData[index]["author"]}"),
         );
     }
   
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return ListView.builder(
         itemCount: listData.length,
         itemBuilder: this._getListData,
       );
     }
   }
   ```
   
实现：
   
![image-20210103032926164](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103032926164.png)
   
3. 利用自定义函数实现引入外来文件的动态列表

   实例：

   ```dart
   import 'package:flutter/cupertino.dart';
   import 'package:flutter/material.dart';
   import 'package:flutter/widgets.dart';
   import 'res/ListData.dart';
   
   void main() {
     runApp(MyApp());
   }
   //自定义组件
   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return MaterialApp(
         home: Scaffold(
           appBar: AppBar(
             title: Text(
                 'Hello Flutter',
               textAlign: TextAlign.center,
             ),
           ),
           body: HomeContent(),
         ),
         theme: ThemeData(
             primarySwatch: Colors.amber
         ),
       );
     }
   }
   //导航栏 列表
   class HomeContent extends StatelessWidget {
   
     List<Widget> _getDataList() {
       var tempList = listData.map((e) {
         return ListTile(
           title: Text(e["title"]),
           subtitle: Text(e["author"]),
           trailing: Image.network(e['imageUrl']),
         );
       });
       return tempList.toList();
     }
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return ListView(
         children: this._getDataList(),
       );
     }
   }
   
   ```

   实现：

   ![image-20210103033839835](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103033839835.png)

### GridView组件

常用属性：

![image-20210103040732356](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103040732356.png)

1. Flutter GridView.count 实现网格布局

   实例：

   ```dart
   import 'package:flutter/cupertino.dart';
   import 'package:flutter/material.dart';
   import 'package:flutter/widgets.dart';
   import 'res/ListData.dart';
   
   void main() {
     runApp(MyApp());
   }
   //自定义组件
   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return MaterialApp(
         home: Scaffold(
           appBar: AppBar(
             title: Text(
                 'Hello Flutter',
               textAlign: TextAlign.center,
             ),
           ),
           body: HomeContent(),
         ),
         theme: ThemeData(
             primarySwatch: Colors.amber
         ),
       );
     }
   }
   //导航栏 列表
   class HomeContent extends StatelessWidget {
   
     List<Widget> _getDataList() {
       var tempList = listData.map((e) {
         return Container(
           child: Column(
             children: <Widget>[
               Image.network(e["imageUrl"]),
               SizedBox(height: 10),
               Text(
                 e["title"],
                 textAlign: TextAlign.center,
                 style: TextStyle(
                   fontSize: 13,
                   color: Colors.blueAccent
                 ),
               )
             ],
           ),
           decoration: BoxDecoration(
             border: Border.all(
               color: Colors.black26,
               width: 1,
             )
           ),
         );
       });
       return tempList.toList();
     }
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return GridView.count(
         padding: EdgeInsets.all(10),
         crossAxisCount: 2,  //列数
         crossAxisSpacing: 10,  //列间距
         mainAxisSpacing: 10,  //行间距
         // childAspectRatio: 0.7,  //子Widget 宽高比例
         children: this._getDataList(),
       );
     }
   }
   
   ```

   实现：

   ![image-20210103042032964](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103042032964.png)

2. Flutter GridView.builder 实现网格布局

   实例：

   ```dart
   import 'package:flutter/cupertino.dart';
   import 'package:flutter/material.dart';
   import 'package:flutter/widgets.dart';
   import 'res/ListData.dart';
   
   void main() {
     runApp(MyApp());
   }
   //自定义组件
   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return MaterialApp(
         home: Scaffold(
           appBar: AppBar(
             title: Text(
                 'Hello Flutter',
               textAlign: TextAlign.center,
             ),
           ),
           body: HomeContent(),
         ),
         theme: ThemeData(
             primarySwatch: Colors.amber
         ),
       );
     }
   }
   //导航栏 列表
   class HomeContent extends StatelessWidget {
   
     Widget _getDataList(context,index) {
       return Container(
         child: Column(
           children: <Widget>[
             Image.network(listData[index]["imageUrl"]),
             SizedBox(height: 10),
             Text(
               listData[index]["title"],
               textAlign: TextAlign.center,
               style: TextStyle(
                   fontSize: 13,
                   color: Colors.black87
               ),
             )
           ],
         ),
         decoration: BoxDecoration(
             border: Border.all(
               color: Colors.black26,
               width: 1,
             )
         ),
       );
     }
     @override
     Widget build(BuildContext context) {
       // TODO: implement build
       return GridView.builder(
           gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
             crossAxisCount: 2,  //列数
             crossAxisSpacing: 10,  //列间距
             mainAxisSpacing: 10,  //行间距
           ),
           itemBuilder: this._getDataList,
       );
     }
   }
   
   ```

   实现：

   ![image-20210103042601922](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103042601922.png)

### Paddiing组件

用Padding 组件处理容器与子元素直接的间距。

![image-20210103184654428](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103184654428.png)

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  Widget _getDataList(context,index) {
    return Container(
      child: Column(
        children: <Widget>[
          Image.network(listData[index]["imageUrl"]),
          SizedBox(height: 10),
          Text(
            listData[index]["title"],
            textAlign: TextAlign.center,
            style: TextStyle(
                fontSize: 13,
                color: Colors.black87
            ),
          )
        ],
      ),
      decoration: BoxDecoration(
          border: Border.all(
            color: Colors.black26,
            width: 1,
          )
      ),
    );
  }
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Padding(
      padding: EdgeInsets.fromLTRB(0, 0, 10, 0),  //最外面的右边距
      child: GridView.count(
          crossAxisCount: 2,//两列
        childAspectRatio: 1.5, //比例
        children: <Widget>[
          Padding(
            padding: EdgeInsets.fromLTRB(10, 10, 0, 0),
            child: Image.network(''
                'https://www.itying.com/images/flutter/1.png',
                 fit: BoxFit.cover
            ),
          ),
          Padding(
            padding: EdgeInsets.fromLTRB(10, 10, 0, 0),
            child: Image.network(''
                'https://www.itying.com/images/flutter/2.png',
                fit: BoxFit.cover
            ),
          ),
          Padding(
            padding: EdgeInsets.fromLTRB(10, 10, 0, 0),
            child: Image.network(''
                'https://www.itying.com/images/flutter/3.png',
                fit: BoxFit.cover
            ),
          ),
          Padding(
            padding: EdgeInsets.fromLTRB(10, 10, 0, 0),
            child: Image.network(''
                'https://www.itying.com/images/flutter/4.png',
                fit: BoxFit.cover
            ),
          ),
          Padding(
            padding: EdgeInsets.fromLTRB(10, 10, 0, 0),
            child: Image.network(''
                'https://www.itying.com/images/flutter/5.png',
                fit: BoxFit.cover
            ),
          ),
          Padding(
            padding: EdgeInsets.fromLTRB(10, 10, 0, 0),
            child: Image.network(''
                'https://www.itying.com/images/flutter/6.png',
                fit: BoxFit.cover
            ),
          ),
        ],
      ),
    );
  }
}

```

实现：

![image-20210103193753606](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103193753606.png)

### Row组件

![image-20210103193840306](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103193840306.png)

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 700,
      width: 500,
      color: Colors.white,
      child: Padding(
        padding: EdgeInsets.all(10),
        child: Row(
          crossAxisAlignment: CrossAxisAlignment.start,    //列内排列方式
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,   //行内排列方式
          children: <Widget>[
            IconContainer(Icons.list, color:Colors.red),
            IconContainer(Icons.add, color:Colors.yellow),
            IconContainer(Icons.phone, color:Colors.blue),
          ],
        ),
      )
    );
  }
}
//自定义组件 IconContainer
class IconContainer extends StatelessWidget {
  double size = 32.0;
  IconData icon;
  Color color = Colors.red;

  IconContainer(this.icon, {this.size, this.color});
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 50,
      height: 50,
      color: this.color,
      child: Center(
        child: Icon(this.icon,
        color: Colors.white,
        size: this.size
        ),
      ),
    );
  }
}
```



实现：

![image-20210103200910282](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103200910282.png)

### Column组件

![image-20210103200954040](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103200954040.png)

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 700,
      width: 500,
      color: Colors.white,
      child: Padding(
        padding: EdgeInsets.all(10),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.center,    //行内排列方式
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,   //列内排列方式 非常常用
          children: <Widget>[
            IconContainer(Icons.list, color:Colors.red),
            IconContainer(Icons.add, color:Colors.yellow),
            IconContainer(Icons.phone, color:Colors.blue),
          ],
        ),
      )
    );
  }
}
//自定义组件
class IconContainer extends StatelessWidget {
  double size = 32.0;
  IconData icon;
  Color color = Colors.red;

  IconContainer(this.icon, {this.size, this.color});
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 50,
      height: 50,
      color: this.color,
      child: Center(
        child: Icon(this.icon,
        color: Colors.white,
        size: this.size
        ),
      ),
    );
  }
}

```

实现：

![image-20210103201111935](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103201111935.png)

### Expanded组件

Expanded 可以用在Row 和Column 布局中综合使用 实现Flex布局的效果

![image-20210103201236305](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103201236305.png)

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
              'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 700,
      width: 500,
      color: Colors.white,
      child: Padding(
        padding: EdgeInsets.all(5),
        child: Row(
          crossAxisAlignment: CrossAxisAlignment.start,    //行内排列方式
          children: <Widget>[
            Expanded(
              flex: 2,
              child: IconContainer(Icons.list, color:Colors.red),
            ),
            Expanded(
              flex: 1,
              child:IconContainer(Icons.add, color:Colors.yellow),
            )
          ],
        ),
      )
    );
  }
}
//自定义组件
class IconContainer extends StatelessWidget {
  double size = 32.0;
  IconData icon;
  Color color = Colors.red;

  IconContainer(this.icon, {this.size, this.color});
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 50,
      height: 50,
      color: this.color,
      child: Center(
        child: Icon(this.icon,
        color: Colors.white,
        size: this.size
        ),
      ),
    );
  }
}
```

实现：

![image-20210103201546066](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103201546066.png)

Flex布局实例：

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}

//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(primarySwatch: Colors.amber),
    );
  }
}

//导航栏 列表
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 320,
      color: Colors.white,
      padding: EdgeInsets.all(5),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start, //行内排列方式
        children: <Widget>[
          Row(
            children: <Widget>[
              Expanded(
                flex: 1,
                child: Container(
                  color: Colors.black,
                  height: 150,
                ),
              ),
            ],
          ),
          SizedBox(height: 5),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Expanded(
                flex: 2,
                child: Container(
                  height: 150,
                  child: Image.network(
                      'https://www.itying.com/images/flutter/1.png',
                       fit: BoxFit.cover,
                  ),
                ),
              ),
              SizedBox(width: 5,),
              Expanded(
                  flex: 1,
                  child: Container(
                    height: 150,
                    child: ListView(
                      children: <Widget>[
                        Container(
                          height: 72.5,
                          child: Image.network(
                            "https://www.itying.com/images/flutter/2.png",
                            fit: BoxFit.cover,
                          ),
                        ),
                        SizedBox(height: 5),
                        Container(
                          height: 72.5,
                          child: Image.network(
                            "https://www.itying.com/images/flutter/3.png",
                            fit: BoxFit.cover,
                          ),
                        ),
                      ],
                    ),
                  ))
            ],
          )
        ],
      ),
    );
  }
}

```

实现：

![image-20210103210026231](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210103210026231.png)

### Stack组件

Stack 表示堆的意思，我们可以用Stack 或者Stack 结合Align 或者Stack 结合Positiond 来实现页面的定位布局

![image-20210104095455533](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104095455533.png)

Stack会使得每个元素都叠在一起

示例：

![image-20210104100238486](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104100238486.png)

### Align组件

Stack 组件中结合Align 组件可以控制每个子元素的显示位置

![image-20210104100353254](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104100353254.png)

示例：

![image-20210104103410459](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104103410459.png)

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}

//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(primarySwatch: Colors.amber),
    );
  }
}

//导航栏 列表
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      color: Colors.blue,
      height: 300,
      child: Stack(
        children: [
          Align(
            alignment: AlignmentDirectional.center,
              child: Icon(
            Icons.add,
            color: Colors.white,
          )),
          Align(
            alignment: AlignmentDirectional.topStart,
              child: Icon(
            Icons.ac_unit_outlined,
            color: Colors.white,
          )),
          Align(
              alignment: AlignmentDirectional.bottomEnd,
              child: Icon(
            Icons.access_alarm,
            color: Colors.white,
          )),
        ],
      ),
    );
  }
}
```

### Positioned组件

Stack 组件中结合Positioned 组件也可以控制每个子元素的显示位置

![image-20210104103511751](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104103511751.png)

示例：

![image-20210104103935961](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104103935961.png)

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}

//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(primarySwatch: Colors.amber),
    );
  }
}

//导航栏 列表
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      color: Colors.blue,
      height: 300,
      child: Stack(
        children: [
          Positioned(
            top: 0,
              child: Icon(
            Icons.add,
            color: Colors.white,)
          ),
          Positioned(
              bottom: 0,
              right: 20,
              child: Icon(
                Icons.access_alarm,
                color: Colors.white,)
          ),
          Positioned(
              top: 150,
              left: 150,
              child: Icon(
                Icons.repeat,
                color: Colors.white,)
          ),
        ],
      ),
    );
  }
}
```

练习：

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  List<Widget> _getDataList() {
    var tempList = listData.map((e) {
      return Container(
        height: 230,
          padding: EdgeInsets.all(5),
          child: Stack(
         children: [
           Align(
             child: Image.network(e['imageUrl'],
             fit: BoxFit.cover,),
           ),
           Align(
             alignment: AlignmentDirectional.bottomCenter,
             child: Text(
                 e['title'],
               style: TextStyle(
                 fontSize: 20,
                 fontWeight: FontWeight.bold,
                 color: Colors.white
               ),
             ),
           )
         ],
       )
      );
    });
    return tempList.toList();
  }
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView(
      children: this._getDataList(),
    );
  }
}
```

示例：

![image-20210104111048324](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104111048324.png)

### AspectRatio 组件

AspectRatio 的作用是根据设置调整子元素child 的宽高比。
AspectRatio 首先会在布局限制条件允许的范围内尽可能的扩展，widget 的高度是由宽度和比率决定的，类似于BoxFit 中的contain，按照固定比率去尽量占满区域。
如果在满足所有限制条件过后无法找到一个可行的尺寸，AspectRatio 最终将会去优先适应布局限制条件，而忽略所设置的比率。

![image-20210104112727768](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104112727768.png)

示例：

![image-20210104113810808](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104113810808.png)

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 100,
      child: AspectRatio(
          child:Image.network("https://www.itying.com/images/flutter/2.png",
            fit: BoxFit.cover,),
          aspectRatio: 3/1),
    );
  }
}
```

### Card组件

Card 是卡片组件块，内容可以由大多数类型的Widget 构成，Card 具有圆角和阴影，这让它看起来有立体感。

![image-20210104113918728](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104113918728.png)

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView(
      children: [
        Card(
          child: Column(
            children: [
              ListTile(
                title: Text("张三",
                  style: TextStyle(
                    fontSize: 25,
                  ),),
                subtitle: Text("高级软件工程师",
                  style: TextStyle(
                      color: Colors.black26
                  ),),
              ),
              ListTile(
                title: Text("电话：xxx"),
              ),
              ListTile(
                  title:Text("地址：xxxxxx"),
              ),
            ],
          )
        ),
        Card(
            child: Column(
              children: [
                ListTile(
                  title: Text("李四",
                    style: TextStyle(
                      fontSize: 25,
                    ),),
                  subtitle: Text("高级软件工程师",
                    style: TextStyle(
                        color: Colors.black26
                    ),),
                ),
                ListTile(
                  title: Text("电话：xxx"),
                ),
                ListTile(
                  title:Text("地址：xxxxxx"),
                ),
              ],
            )
        )
      ],
    );
  }
}
```

示例：

![image-20210104114723073](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104114723073.png)

#### 图文列表布局

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView(
      children: listData.map((e) {
        return Card(
            child: Column(
              children: [
                AspectRatio(
                  aspectRatio: 16/9,
                  child:Image.network(e["imageUrl"],
                    fit: BoxFit.cover,
                  ),
                ),
                ListTile(
                  leading: CircleAvatar(
                    backgroundImage: NetworkImage(e["imageUrl"]),
                  ),
                  title: Text(e["title"]),
                  subtitle: Text(e["description"],
                    overflow: TextOverflow.ellipsis,),
                ),
              ],
            )
        );
      }).toList(),
    );
  }
}
```

示例:

![image-20210104120644704](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104120644704.png)

### Wrap组件

Wrap 可以实现流布局，单行的Wrap 跟Row 表现几乎一致，单列的Wrap 则跟Row 表现几乎一致。但Row 与Column 都是单行单列的，Wrap 则突破了这个限制，mainAxis 上空间不足时，则向crossAxis 上去扩展显示。

![image-20210104150728123](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104150728123.png)

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Wrap(
      spacing: 10,
      runSpacing: 10,
      // direction: Axis.vertical,  //纵向显示
      // textDirection: TextDirection.rtl,  //文字方向
      verticalDirection: VerticalDirection.down,  //纵向显示方向
      alignment: WrapAlignment.spaceEvenly,  //整体对齐方向
      // runAlignment: WrapAlignment.center,
      children: [
        MyButton("第一集"),
        MyButton("第二集"),
        MyButton("第三集第三集第三集第三集第三集"),
        MyButton("第四集"),
        MyButton("第五集"),
        MyButton("第六集第六集第六集"),
        MyButton("第七集"),
        MyButton("第八集"),
        MyButton("第九集"),
        MyButton("第十集"),
      ],
    );
  }
}

//自定义button
class MyButton extends StatelessWidget {
  String context = "第一集";

  MyButton(this.context);

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return RaisedButton(
      child: Text(this.context),
        textColor: Colors.amber,
        onPressed: (){},
    );
  }

}

```

实例：

![image-20210104152150615](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104152150615.png)

### 自定义有状态组件

在Flutter 中自定义组件其实就是一个类，这个类需要继承StatelessWidget/StatefulWidget。
StatelessWidget 是无状态组件，状态不可变的widget，
StatefulWidget 是有状态组件，持有的状态可能在widget 生命周期改变。通俗的讲：如果我们想改变页面中的数据的话这个时候就需要用到StatefulWidget

实例一  动态增加文本内容

代码：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return TestStateful(

    );
  }
}

//自定义动态组件
class TestStateful extends StatefulWidget {
  @override
  _TestStatefulState createState() => _TestStatefulState();
}

class _TestStatefulState extends State<TestStateful> {
  int countNum = 0;
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Column(
      crossAxisAlignment: CrossAxisAlignment.center,
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Text("${this.countNum}"),
        SizedBox(height: 10,),
        RaisedButton(
            child: Text("增加"),
            onPressed: () {
              setState(() {
                 this.countNum ++;
              });
            })
      ],
    );
  }
}

```

实现：

![image-20210104155536490](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104155536490.png)

实例二  动态增加列表数量

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'res/ListData.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text(
            'Hello Flutter',
            textAlign: TextAlign.center,
          ),
        ),
        body: HomeContent(),
      ),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
//导航栏 列表
class HomeContent extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return TestStateful(

    );
  }
}

//自定义button
class TestStateful extends StatefulWidget {
  @override
  _TestStatefulState createState() => _TestStatefulState();
}

class _TestStatefulState extends State<TestStateful> {
  List<String> myList = new List();
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView(
      children: [
        Column(
          children: myList.map((e) {
            return ListTile(
              title: Text(e),
            );
          }).toList(),
        ),
        RaisedButton(
          child: Text("增加新闻"),
            onPressed: () {
            setState(() {
              myList.add("新增新闻1");
              myList.add("新增新闻2");
            });
        })
      ],
    );
  }
}

```

实现：

![image-20210104160529645](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104160529645.png)

### BottomNavigationBar 组件

  BottomNavigationBar 是底部导航条，可以让我们定义底部Tab 切换，bottomNavigationBar是Scaffold 组件的参数。

![image-20210104162041982](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104162041982.png)

代码：

Tabs.dart

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'tab/Category.dart';
import 'tab/Home.dart';
import 'tab/Settings.dart';

class HomeContent extends StatefulWidget{
  @override
  _HomeContentState createState() => _HomeContentState();
}
class _HomeContentState extends State<HomeContent> {
  int _currentIndex = 0;
  List _pageList = [
    Home(),
    Category(),
    Settings()
  ];
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Scaffold(
      appBar: AppBar(
        title: Text(
          'Hello Flutter',
          textAlign: TextAlign.center,
        ),
      ),
      body: this._pageList[this._currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: this._currentIndex,
        fixedColor: Colors.amber,
        type: BottomNavigationBarType.fixed,
        items: [
          BottomNavigationBarItem(
              label: "首页",
              icon: Icon(Icons.home)
          ),
          BottomNavigationBarItem(
              label: "分类",
              icon: Icon(Icons.category)
          ),BottomNavigationBarItem(
              label: "设置",
              icon: Icon(Icons.settings)
          ),
        ],
        onTap: (int index) {
          setState(() {
            this._currentIndex = index;
          });
        },
      ),
    );
  }
}
```

三个页面:

```dart
//Home.dart

import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 300,
      alignment: AlignmentDirectional.center,
      child: Text("我是首页",
        style: TextStyle(
            fontSize: 20,
            color: Colors.amber
        ),),
    );
  }
}

//Category.dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class Category extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 300,
      alignment: AlignmentDirectional.center,
      child: Text("我是分类页",
      style: TextStyle(
          fontSize: 20,
        color: Colors.purple
      ),),
    );
  }
}

//Settings.dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class Settings extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      height: 300,
      alignment: AlignmentDirectional.center,
      child: Text("我是设置页",
        style: TextStyle(
            fontSize: 20,
            color: Colors.blue
        ),),
    );
  }
}
```

main.dart

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'pages/Tabs.dart';

void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: HomeContent(),
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}
```

![image-20210104173713726](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210104173713726.png)

### Navigator 组件（路由）

Flutter 中给我们提供了两种配置路由跳转的方式：1、基本路由2、命名路由

#### 基本路由跳转传值

实例：Home页跳转到Search页

Search.dart

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class Search extends StatelessWidget {
  String title;

  Search({this.title = "表单（默认）"});
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Scaffold(
      appBar: AppBar(
        title: Text(
          this.title,
          textAlign: TextAlign.center,
        ),
      ),
      body: Container(
        height: 300,
        alignment: AlignmentDirectional.center,
        child: Text("我是搜索页",
          style: TextStyle(
              fontSize: 20,
              color: Colors.green
          ),),
      ),
    );
  }
}
```

Home.dart

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import '../Search.dart';

class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Column(
      children: [
        Container(
          height: 100,
          alignment: AlignmentDirectional.center,
          child: Text("我是首页",
            style: TextStyle(
                fontSize: 20,
                color: Colors.amber
            ),),
        ),
        RaisedButton(
          child: Text("点我跳转到搜索页面"),
            onPressed: () {
            Navigator.of(context).push(
                MaterialPageRoute(
                    builder: (BuildContext context) {
                      return Search(title:"搜索页（传值）"); // 跳转传值
                })
            );
        })
      ],
    );
  }
}
```

实现：

![image-20210106105235871](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106105235871.png)

![image-20210106105246965](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106105246965.png)

#### 命名路由跳转传值

官方文档：https://flutter.dev/docs/cookbook/navigation/navigate-with-arguments

实例：

```dart
//routes.dart

import 'package:flutter/material.dart';
import '../Tabs.dart';
import '../product.dart';
import '../product_info.dart';
import '../Search.dart';

final routes={
  '/':(context)=>HomeContent(),

  '/product':(context)=>Product(),
  '/productInfo':(context,{arguments})=>ProductInfo(arguments:arguments),
  '/search':(context)=>Search(),
};
//固定写法
var onGenerateRoute=(RouteSettings settings) {
  // 统一处理
  final String name = settings.name;
  final Function pageContentBuilder = routes[name];
  if (pageContentBuilder != null) {
    if (settings.arguments != null) {
      final Route route = MaterialPageRoute(
          builder: (context) =>
              pageContentBuilder(context, arguments: settings.arguments));
      return route;
    }else{
      final Route route = MaterialPageRoute(
          builder: (context) =>
              pageContentBuilder(context));
      return route;
    }
  }
};


//main.dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'pages/routes/routes.dart';


void main() {
  runApp(MyApp());
}
//自定义组件
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {

    return MaterialApp(
      initialRoute: '/',     //初始化的时候加载的路由
      onGenerateRoute: onGenerateRoute,
      theme: ThemeData(
          primarySwatch: Colors.amber
      ),
    );
  }
}


//product.dart
import 'package:flutter/material.dart';

class Product extends StatefulWidget {
  @override
  _ProductState createState() => _ProductState();
}

class _ProductState extends State<Product> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "商品页",
          textAlign: TextAlign.center,
        ),
      ),
      body: Column(
        children: [
          Container(
            height: 300,
            alignment: AlignmentDirectional.center,
            child: Text("我是商品页",
              style: TextStyle(
                  fontSize: 20,
                  color: Colors.green
              ),),
          ),
          RaisedButton(
              child: Text("点我跳转到商品详情页"),
              onPressed: () {
                Map pid = {
                  "count": 123
                };
                Navigator.pushNamed(context, "/productInfo",arguments: pid);
              })
        ],
      ),
    );
  }
}


//productInfo.dart
import 'package:flutter/material.dart';

class ProductInfo extends StatefulWidget {
  final Map arguments;
  ProductInfo({Key key,this.arguments}) : super(key: key);

  @override
  _ProductInfoState createState() => _ProductInfoState(arguments: this.arguments);
}

class _ProductInfoState extends State<ProductInfo> {
  Map arguments;
  _ProductInfoState({this.arguments});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        child: Text("Back"),
        onPressed: (){
          Navigator.pop(context);
        },
      ),
      appBar: AppBar(
        title: Text(
          "商品详情页",
          textAlign: TextAlign.center,
        ),
      ),
      body: Container(
          height: 100,
          alignment: AlignmentDirectional.center,
          child: Column(
            children: [
              Text("我是商品详情页",
                style: TextStyle(
                    fontSize: 20,
                    color: Colors.green
                ),
              ),
              Text('${this.arguments["count"]}'),
            ],
          )
      ),
    );
  }
}
```

实现：

![image-20210106131311349](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106131311349.png)

#### 返回到上一级页面

```dart
Navigator.of(context).pop();
```

#### 替换路由

```dart
Navigator.of(context).pushReplacementNamed('/registerSecond');
```

#### 返回到根路由

```dart
Navigator.of(context).pushAndRemoveUntil(
new MaterialPageRoute(builder: (context) => new Tabs(index:1)),
(route) => route == null
);
```

### AppBar组件

![image-20210106141642732](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106141642732.png)

### TabBar组件

![image-20210106141710903](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106141710903.png)

实例：

```dart
//main
debugShowCheckedModeBanner: false,  //取消debug标签


import 'package:flutter/material.dart';

class AppBarTest extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
        length: 3,
        child: Scaffold(
          appBar: AppBar(
            leading: IconButton(
              icon: Icon(
                  Icons.list
              ),
              onPressed: () {
                Navigator.pushNamed(context, '/formPage');
              },
            ),
            title: Text(
              "AppBarTest",
            ),
            centerTitle: true,
            actions: [
              IconButton(
                icon: Icon(
                    Icons.accessibility
                ),
                onPressed: () {
                  Navigator.pushNamed(context, '/product');
                },)
            ],
            bottom: TabBar(
              tabs: <Widget>[
                Tab(text: "推荐"),
                Tab(text: "精选"),
                Tab(text: "广告"),
              ],
            ),
            backgroundColor:Colors.orange,

          ),
          body: TabBarView(
            children: <Widget>[
              Column(
                children: [
                  Container(
                    height: 300,
                    alignment: AlignmentDirectional.center,
                    child: Text("我是推荐页",
                      style: TextStyle(
                          fontSize: 20,
                          color: Colors.green
                      ),),
                  ),
                ],
              ),
              Column(
                children: [
                  Container(
                    height: 300,
                    alignment: AlignmentDirectional.center,
                    child: Text("我是精选页",
                      style: TextStyle(
                          fontSize: 20,
                          color: Colors.blueGrey
                      ),),
                  ),
                ],
              ),
              Column(
                children: [
                  Container(
                    height: 300,
                    alignment: AlignmentDirectional.center,
                    child: Text("我是广告页",
                      style: TextStyle(
                          fontSize: 20,
                          color: Colors.cyan
                      ),),
                  ),
                ],
              ),
            ],
          )
        ),
    );
  }
}

```

实现：

![image-20210106150211367](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106150211367.png)

实现AppBar中AppBar

实例：

```dart
//Category
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class Category extends StatefulWidget {
  @override
  _CategoryState createState() => _CategoryState();
}

class _CategoryState extends State<Category> {
  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
        length: 7,
        child: Scaffold(
            appBar: AppBar(
              title: Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Expanded(
                      child: TabBar(
                        isScrollable: true,
                        tabs: <Widget>[
                          Tab(text: "首页"),
                          Tab(text: "推荐"),
                          Tab(text: "精选"),
                          Tab(text: "广告"),
                          Tab(text: "同城"),
                          Tab(text: "字典"),
                          Tab(text: "猜我喜欢"),
                        ],
                      ),
                  )
                ],
              ),
            ),
            body: TabBarView(
              children: <Widget>[
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是首页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.green
                        ),),
                    ),
                  ],
                ),
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是精选页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.blueGrey
                        ),),
                    ),
                  ],
                ),
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是广告页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.cyan
                        ),),
                    ),
                  ],
                ),
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是推荐页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.green
                        ),),
                    ),
                  ],
                ),
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是同城页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.green
                        ),),
                    ),
                  ],
                ),
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是字典页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.green
                        ),),
                    ),
                  ],
                ),
                Column(
                  children: [
                    Container(
                      height: 100,
                      alignment: AlignmentDirectional.center,
                      child: Text("我是猜我喜欢页",
                        style: TextStyle(
                            fontSize: 20,
                            color: Colors.green
                        ),),
                    ),
                  ],
                ),
              ],
            )
        ),
      );
    /*Column(
      children: [
        Container(
          height: 100,
          alignment: AlignmentDirectional.center,
          child: Text(
            "我是分类页",
            style: TextStyle(fontSize: 20, color: Colors.purple),
          ),
        ),
        RaisedButton(
            child: Text("点我跳转到商品页面"),
            onPressed: () {
              Navigator.pushNamed(context, "/product");
            })
      ],
    );*/
  }
}


```

实现：

![image-20210106153036489](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106153036489.png)

自定义组件的方式实现TabBar

实例：

```dart
import 'package:flutter/material.dart';

class TabBarController extends StatefulWidget {
  @override
  _TabBarControllerState createState() => _TabBarControllerState();
}

class _TabBarControllerState extends State<TabBarController> with SingleTickerProviderStateMixin{
  TabController _tabController;

  @override
  void initState() {
    super.initState();
    _tabController = new TabController(length: 3, vsync: this);
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text(
            "TabBarTest",
          ),
          centerTitle: true,
          bottom: TabBar(
            tabs: <Widget>[
              Tab(text: "推荐"),
              Tab(text: "精选"),
              Tab(text: "广告"),

            ],
            controller: _tabController,
          ),
          backgroundColor:Colors.blue,
        ),
        body: TabBarView(
          controller: _tabController,
          children: <Widget>[
            Column(
              children: [
                Container(
                  height: 100,
                  alignment: AlignmentDirectional.center,
                  child: Text("我是推荐页",
                    style: TextStyle(
                        fontSize: 20,
                        color: Colors.green
                    ),),
                ),
              ],
            ),
            Column(
              children: [
                Container(
                  height: 100,
                  alignment: AlignmentDirectional.center,
                  child: Text("我是精选页",
                    style: TextStyle(
                        fontSize: 20,
                        color: Colors.blueGrey
                    ),),
                ),
              ],
            ),
            Column(
              children: [
                Container(
                  height: 100,
                  alignment: AlignmentDirectional.center,
                  child: Text("我是广告页",
                    style: TextStyle(
                        fontSize: 20,
                        color: Colors.cyan
                    ),),
                ),
              ],
            ),
          ],
        )
    );
  }
}
```

实现：

![image-20210106160016289](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106160016289.png)

### Drawer 侧边栏

在Scaffold 组件里面传入drawer 参数可以定义左侧边栏，传入endDrawer 可以定义右侧边栏。侧边栏默认是隐藏的，我们可以通过手指滑动显示侧边栏，也可以通过点击按钮显示侧边栏。

#### DrawerHeader属性

![image-20210106163032601](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106163032601.png)

#### UserAccountsDrawerHeader属性

![image-20210106163053442](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106163053442.png)

#### 侧边栏路由跳转

```dart
onTap: (){
    Navigator.of(context).pop();
    Navigator.pushNamed(context, '/search');
}
```

实例：

```dart
//①
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'tab/Category.dart';
import 'tab/Home.dart';
import 'tab/Settings.dart';

class HomeContent extends StatefulWidget{
  int index;
  HomeContent({this.index = 0});
  @override
  _HomeContentState createState() => _HomeContentState(this.index);
}
class _HomeContentState extends State<HomeContent> {
  int _currentIndex;
  List _pageList = [
    Home(),
    Category(),
    Settings()
  ];
  _HomeContentState(this._currentIndex);

  @override
  Widget build(BuildContext context) {

    return Scaffold(
      drawer: Drawer(
        child: ListView(
          children: <Widget>[
            DrawerHeader(
                child: Text("你好 Flutter！"),
              decoration: BoxDecoration(
                color: Colors.amber,
                image: DecorationImage(
                  image: NetworkImage("https://www.itying.com/images/flutter/2.png",),
                  fit: BoxFit.cover
                ),
              ),
            ),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.people),
              ),
              title: Text("个人中心"),
            ),
            Divider(),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.settings),
              ),
              title: Text("设置中心"),
            ),
            Divider(),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.home),
              ),
              title: Text("家园中心"),
            ),
            Divider(),
          ],
        ),
      ),
      appBar: AppBar(
        title: Text(
          'Hello Flutter',
          textAlign: TextAlign.center,
        ),
      ),
      body: this._pageList[this._currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: this._currentIndex,
        fixedColor: Colors.amber,
        type: BottomNavigationBarType.fixed,
        items: [
          BottomNavigationBarItem(
              label: "首页",
              icon: Icon(Icons.home)
          ),
          BottomNavigationBarItem(
              label: "分类",
              icon: Icon(Icons.category)
          ),BottomNavigationBarItem(
              label: "设置",
              icon: Icon(Icons.settings)
          ),
        ],
        onTap: (int index) {
          setState(() {
            this._currentIndex = index;
          });
        },
      ),
    );
  }
}
//②
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'tab/Category.dart';
import 'tab/Home.dart';
import 'tab/Settings.dart';

class HomeContent extends StatefulWidget{
  int index;
  HomeContent({this.index = 0});
  @override
  _HomeContentState createState() => _HomeContentState(this.index);
}
class _HomeContentState extends State<HomeContent> {
  int _currentIndex;
  List _pageList = [
    Home(),
    Category(),
    Settings()
  ];
  _HomeContentState(this._currentIndex);

  @override
  Widget build(BuildContext context) {

    return Scaffold(
      drawer: Drawer(
        child: ListView(
          children: <Widget>[
            UserAccountsDrawerHeader(
              accountName: Text("Dorothea"),
              accountEmail: Text("123@123.com"),
              currentAccountPicture: CircleAvatar(
                backgroundImage: NetworkImage("https://www.itying.com/images/flutter/3.png")
              ),
              otherAccountsPictures: [
                CircleAvatar(
                  backgroundImage: NetworkImage("https://www.itying.com/images/flutter/1.png"),
                ),
                CircleAvatar(
                  backgroundImage: NetworkImage("https://www.itying.com/images/flutter/2.png"),
                ),
              ],
              decoration: BoxDecoration(
                image: DecorationImage(
                  image: NetworkImage("https://www.itying.com/images/flutter/4.png"),
                  fit: BoxFit.cover,
                )
              ),
            ),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.people),
              ),
              title: Text("个人中心"),
            ),
            Divider(),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.settings),
              ),
              title: Text("设置中心"),
            ),
            Divider(),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.home),
              ),
              title: Text("家园中心"),
            ),
            Divider(),
          ],
        ),
      ),
      appBar: AppBar(
        title: Text(
          'Hello Flutter',
          textAlign: TextAlign.center,
        ),
      ),
      body: this._pageList[this._currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: this._currentIndex,
        fixedColor: Colors.amber,
        type: BottomNavigationBarType.fixed,
        items: [
          BottomNavigationBarItem(
              label: "首页",
              icon: Icon(Icons.home)
          ),
          BottomNavigationBarItem(
              label: "分类",
              icon: Icon(Icons.category)
          ),BottomNavigationBarItem(
              label: "设置",
              icon: Icon(Icons.settings)
          ),
        ],
        onTap: (int index) {
          setState(() {
            this._currentIndex = index;
          });
        },
      ),
    );
  }
}
```

实现：

①![image-20210106164855831](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210106164855831.png)

②

![image-20210106170125004](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210106170125004.png)

### 按钮组件

属性：

![image-20210108103034738](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108103034738.png)

![image-20210108103047446](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108103047446.png)

#### RaiseButton

凸起的按钮，其实就是Material Design 风格的Button

#### FlatButton

扁平化的按钮

#### OutlineButton

线框按钮

#### IconButton

图标按钮

#### ButtonBar

按钮组

实例：

```dart
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

class ButtonPage extends StatefulWidget {
  ButtonPage({Key key}) : super(key: key);

  @override
  _ButtonPageState createState() => _ButtonPageState();
}

class _ButtonPageState extends State<ButtonPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton:FloatingActionButton(

          child: Text("圆形浮动按钮"),
          onPressed: (){}
      ),
      appBar: AppBar(
        title: Text(
          '按钮页',
          textAlign: TextAlign.center,
        ),
      ),
      body: Container(
        child: ListView(
          children: [
            ListTile(
              title: Text("RaisedButton"),
            ),
            Divider(),
            Wrap(
              spacing: 10,
              runSpacing: 10,
              children: [
                RaisedButton(
                  child: Text("内边距普通按钮"),
                    padding: EdgeInsets.all(20),
                    textColor: Colors.amber,
                    color: Colors.blue,
                    onPressed: (){

                    }
                ),
                RaisedButton(
                    child: Text("禁用按钮"),
                    disabledTextColor: Colors.deepOrangeAccent,
                    disabledColor: Colors.black26,
                    onPressed: null
                ),
                RaisedButton(
                    child: Text("水泼纹颜色改变按钮"),
                    splashColor: Colors.redAccent,
                    onPressed: () {},
                ),
                RaisedButton(
                  child: Text("长按颜色改变按钮"),
                  highlightColor: Colors.greenAccent,
                  onPressed: () {},
                ),
                RaisedButton(
                  child: Text("阴影按钮"),
                  elevation: 10,
                  onPressed: () {},
                ),
                RaisedButton(
                  child: Text("圆角按钮"),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(10),
                  ),
                  onPressed: () {},
                ),
                RaisedButton.icon(
                  icon: Icon(
                      Icons.category
                  ),
                  label: Text("图标凸起按钮"),
                  highlightColor: Colors.greenAccent,
                  onPressed: () {},
                ),
                RaisedButton(
                  child: Text("圆形"),
                  shape: CircleBorder(
                    side: BorderSide(
                      color: Colors.white,
                    ),
                ),
                  onPressed: () {},
                ),
                Container(
                  child:RaisedButton(
                    child: Text("Container控制大小按钮"),
                    onPressed: () {},
                  ),
                  height: 80,
                  width: 80,
                ),
              ],
            ),
            Divider(),
            ListTile(
              title: Text("FlatButton"),
            ),
            Divider(),
            Wrap(
              spacing: 10,
              runSpacing: 10,
              children: [
                FlatButton(
                    child: Text("内边距普通按钮"),
                    padding: EdgeInsets.all(20),
                    textColor: Colors.amber,
                    color: Colors.blue,
                    onPressed: (){

                    }
                ),
                FlatButton(
                    child: Text("禁用按钮"),
                    disabledTextColor: Colors.deepOrangeAccent,
                    disabledColor: Colors.black26,
                    onPressed: null
                ),
                FlatButton(
                  color: Colors.blue,
                  child: Text("水泼纹颜色改变按钮"),
                  splashColor: Colors.redAccent,
                  onPressed: () {},
                ),
                FlatButton(
                  color: Colors.blue,
                  child: Text("长按颜色改变按钮"),
                  highlightColor: Colors.greenAccent,
                  onPressed: () {},
                ),
                FlatButton.icon(
                  color: Colors.blue,
                  icon: Icon(
                    Icons.category
                  ),
                  label: Text("图标扁平按钮"),
                  highlightColor: Colors.greenAccent,
                  onPressed: () {},
                ),
                FlatButton(
                  child: Text("圆角按钮"),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(10),
                    side: BorderSide(
                      color:Colors.blue,
                    )
                  ),
                  onPressed: () {},
                ),
                FlatButton(
                  color: Colors.blue,
                  child: Text("圆形"),
                  shape: CircleBorder(
                    side: BorderSide(
                      color: Colors.white,
                    ),
                  ),
                  onPressed: () {},
                ),
                Container(
                  child:FlatButton(
                    color: Colors.blue,
                    child: Text("Container控制大小按钮"),
                    onPressed: () {},
                  ),
                  height: 80,
                  width: 80,
                ),
              ],
            ),
            Divider(),
            ListTile(
              title: Text("OutlineButton"),
            ),
            Divider(),
            Wrap(
              spacing: 10,
              runSpacing: 10,
              children: [
                OutlineButton(
                    child: Text("内边距普通按钮"),
                    padding: EdgeInsets.all(20),
                    textColor: Colors.amber,
                    borderSide: BorderSide(
                      color: Colors.blue
                    ),
                    onPressed: (){
                    },
                ),
                OutlineButton(
                    child: Text("禁用按钮"),
                    disabledTextColor: Colors.deepOrangeAccent,
                    disabledBorderColor: Colors.green,
                    onPressed: null
                ),
                OutlineButton(
                  borderSide: BorderSide(
                      color: Colors.blue
                  ),
                  child: Text("水泼纹颜色改变按钮"),
                  splashColor: Colors.redAccent,
                  onPressed: () {},
                ),
                OutlineButton(
                  borderSide: BorderSide(
                      color: Colors.blue
                  ),
                  child: Text("长按颜色改变按钮"),
                  highlightedBorderColor: Colors.greenAccent,
                  highlightElevation: 10,
                  onPressed: () {},
                ),
                OutlineButton(
                  borderSide: BorderSide(
                      color: Colors.blue
                  ),
                  child: Text("圆角按钮"),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(10),
                  ),
                  onPressed: () {},
                ),
                OutlineButton(
                  borderSide: BorderSide(
                      color: Colors.blue
                  ),
                  child: Text("圆形"),
                  shape: CircleBorder(
                    side: BorderSide(
                      color: Colors.white,
                    ),
                  ),
                  onPressed: () {},
                ),
                Container(
                  child:OutlineButton(
                    borderSide: BorderSide(
                        color: Colors.blue
                    ),
                    child: Text("Container控制大小按钮"),
                    onPressed: () {},
                  ),
                  height: 80,
                  width: 80,
                ),
              ],
            ),
            Divider(),
            ListTile(
              title: Text("IconButton"),
            ),
            Divider(),
            Wrap(
              spacing: 10,
              runSpacing: 10,
              children: [
                IconButton(
                  padding: EdgeInsets.all(20),
                    icon: Icon(Icons.accessibility),
                    color: Colors.blue,
                  onPressed: (){

                    },
                ),
                IconButton(
                    icon: Icon(Icons.home),
                  disabledColor: Colors.redAccent,
                  onPressed: null,
                ),
                IconButton(
                    icon: Icon(Icons.settings),
                  splashColor: Colors.amber,
                  splashRadius: 40,
                  onPressed: (){},
                ),
                IconButton(
                    icon: Icon(Icons.people),
                  highlightColor: Colors.green,
                  onPressed: (){},
                ),
              ],
            ),
            Divider(),
            ListTile(
              title: Text("ButtonBar"),
            ),
            Divider(),
            Wrap(
              spacing: 10,
              runSpacing: 10,
              children: [
                ButtonBar(
                  alignment: MainAxisAlignment.center,
                  overflowDirection:VerticalDirection.up,
                  overflowButtonSpacing: 20,
                  children: [
                    RaisedButton(
                        child: Text("内边距普通按钮"),
                        padding: EdgeInsets.all(20),
                        textColor: Colors.amber,
                        color: Colors.blue,
                        onPressed: (){

                        }
                    ),
                    RaisedButton(
                        child: Text("禁用按钮"),
                        disabledTextColor: Colors.deepOrangeAccent,
                        disabledColor: Colors.black26,
                        onPressed: null
                    ),
                    RaisedButton(
                      child: Text("水泼纹颜色改变按钮"),
                      splashColor: Colors.redAccent,
                      onPressed: () {},
                    ),
                  ],
                )
              ],
            ),
          ],
        )
      ),
    );
  }
}
```

实现：

![image-20210108120015668](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108120015668.png)

![image-20210108120028288](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108120028288.png)

![image-20210108120041968](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108120041968.png)

![image-20210108120053353](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108120053353.png)

#### FloatingActionButton

浮动按钮 FloatingActionButton 简称FAB ,可以实现浮动按钮，也可以实现类似闲鱼app 的地步凸起导航

![image-20210108153919556](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108153919556.png)

底部凸起按钮：

实例：

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'tab/Category.dart';
import 'tab/Home.dart';
import 'tab/Settings.dart';

class HomeContent extends StatefulWidget{
  int index;
  HomeContent({this.index = 0});
  @override
  _HomeContentState createState() => _HomeContentState(this.index);
}
class _HomeContentState extends State<HomeContent> {
  int _currentIndex;
  List _pageList = [
    Home(),
    Category(),
    Settings()
  ];
  _HomeContentState(this._currentIndex);

  @override
  Widget build(BuildContext context) {

    return Scaffold(
      drawer: Drawer(
        child: ListView(
          children: <Widget>[
            UserAccountsDrawerHeader(
              accountName: Text("Dorothea"),
              accountEmail: Text("123@123.com"),
              currentAccountPicture: CircleAvatar(
                backgroundImage: NetworkImage("https://www.itying.com/images/flutter/3.png")
              ),
              otherAccountsPictures: [
                CircleAvatar(
                  backgroundImage: NetworkImage("https://www.itying.com/images/flutter/1.png"),
                ),
                CircleAvatar(
                  backgroundImage: NetworkImage("https://www.itying.com/images/flutter/2.png"),
                ),
              ],
              decoration: BoxDecoration(
                image: DecorationImage(
                  image: NetworkImage("https://www.itying.com/images/flutter/4.png"),
                  fit: BoxFit.cover,
                )
              ),
            ),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.people),
              ),
              title: Text("个人中心"),
            ),
            Divider(),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.settings),
              ),
              title: Text("设置中心"),
            ),
            Divider(),
            ListTile(
              leading: CircleAvatar(
                child: Icon(Icons.home),
              ),
              title: Text("家园中心"),
            ),
            Divider(),
          ],
        ),
      ),
      floatingActionButton: Container(
        height: 70,
        width: 70,
        decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(35),
            color: Color.fromARGB(255, 250, 250, 250),
        ),
        padding: EdgeInsets.all(8),
        // margin: EdgeInsets.only(top: 1),
        child: FloatingActionButton(
          elevation: 0,
          child: Icon(
            Icons.add,
            color: this._currentIndex==1?Colors.amber:Color.fromARGB(255, 115, 115, 115),
            size: 40,
          ),
          backgroundColor: this._currentIndex==1?Colors.white:Colors.amber,
          onPressed: () {
            setState(() {
              this._currentIndex = 1;
            });
          },
        ),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
      appBar: AppBar(
        title: Text(
          'Hello Flutter',
          textAlign: TextAlign.center,
        ),
      ),
      body: this._pageList[this._currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: this._currentIndex,
        fixedColor: Colors.amber,
        type: BottomNavigationBarType.fixed,
        items: [
          BottomNavigationBarItem(
              label: "首页",
              icon: Icon(Icons.home)
          ),
          BottomNavigationBarItem(
              label: "分类",
              icon: Icon(Icons.category)
          ),BottomNavigationBarItem(
              label: "设置",
              icon: Icon(Icons.settings)
          ),
        ],
        onTap: (int index) {
          setState(() {
            this._currentIndex = index;
          });
        },
      ),
    );
  }
}
```

实现：

![image-20210108160535373](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108160535373.png)

#### 去除水波纹

```dart
MaterialApp(
  theme: ThemeData(
    // 禁用水波纹效果
    highlightColor: Colors.transparent,
    splashFactory: const NoSplashFactory(),
    primaryColor: Colors.white,
  ),
)
class NoSplashFactory extends InteractiveInkFeatureFactory {
  const NoSplashFactory();

  InteractiveInkFeature create({
    @required MaterialInkController controller,
    @required RenderBox referenceBox,
    @required Offset position,
    @required Color color,
    TextDirection textDirection,
    bool containedInkWell: false,
    RectCallback rectCallback,
    BorderRadius borderRadius,
    ShapeBorder customBorder,
    double radius,
    VoidCallback onRemoved,
  }) {
    return new NoSplash(
      controller: controller,
      referenceBox: referenceBox,
      color: color,
      onRemoved: onRemoved,
    );
  }
}

class NoSplash extends InteractiveInkFeature {
  NoSplash({
    @required MaterialInkController controller,
    @required RenderBox referenceBox,
    Color color,
    VoidCallback onRemoved,
  })  : assert(controller != null),
        assert(referenceBox != null),
        super(
            controller: controller,
            referenceBox: referenceBox,
            onRemoved: onRemoved) {
    controller.addInkFeature(this);
  }

  @override
  void paintFeature(Canvas canvas, Matrix4 transform) {}
}
```

### TextField 文本框组件

![image-20210108165604147](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210108165604147.png)

实例：

```dart
import 'package:flutter/material.dart';

class FormDemo extends StatefulWidget {
  @override
  _FormDemoState createState() => _FormDemoState();
}

class _FormDemoState extends State<FormDemo> {
  var name = new TextEditingController();
  var psd;

  @override
  void initState() {
    // TODO: implement initState
    this.name.text = "用户名";
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '表单页',
          textAlign: TextAlign.center,
        ),
      ),
      body: Container(
        padding: EdgeInsets.all(20),
        child: ListView(
          children: [
            TextField(
                decoration: InputDecoration(
                  hintText: "单行文本框组件",
                )
            ),
            Divider(),
            TextField(
              maxLines: 3,
              decoration: InputDecoration(
                hintText: "多行文本框组件",
              ),
            ),
            Divider(),
            TextField(
              obscureText: true,
              decoration: InputDecoration(
                hintText: "密码文本框组件",
              ),
            ),
            Divider(),
            TextField(
              controller: this.name,
              decoration: InputDecoration(
                hintText: "请输入用户名",
                labelText: "用户名",
                labelStyle: TextStyle(
                  color: Colors.amber
                ),
                border: OutlineInputBorder(

                )
              ),
              onChanged: (value) {
                this.name.text = value;
              },
            ),
            Divider(),
            TextField(
              obscureText: true,
              decoration: InputDecoration(
                hintText: "请输入密码",
                labelText: "密码",
                labelStyle: TextStyle(
                  color: Colors.blue
                ),
                border: OutlineInputBorder(
                )
              ),
              onChanged: (value) {
                this.psd =value;
              },
            ),
            Divider(),
            SizedBox(height: 40),
            RaisedButton(
              child: Text("登录"),
                onPressed: () {
                print(this.name.text);
                print(this.psd);
            },
            ),
          ],
        ),
      )
    );
  }
}

```

实现：

![image-20210108211615842](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108211615842.png)

### Checkbox 多选框组件

![image-20210108211643458](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108211643458.png)

![image-20210108211652681](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108211652681.png)

### CheckboxListTile 多选框组件

![image-20210108211740337](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108211740337.png)

实例：

```dart
import 'package:flutter/material.dart';

class FormDemo extends StatefulWidget {
  @override
  _FormDemoState createState() => _FormDemoState();
}

class _FormDemoState extends State<FormDemo> {
  bool isSelected = false;
  bool isSelected2 = false;
  bool isSelected3 = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '表单页',
          textAlign: TextAlign.center,
        ),
      ),
      // body: TextFiledDemo(),
      body: Container(
        child: ListView(
          children: [
            Checkbox(
                value: isSelected,
                onChanged: (value){
                  setState(() {
                    this.isSelected = value;
                    print(this.isSelected);
                  });
                },
              activeColor: Colors.amber,
              checkColor: Colors.blue,
            ),
            Wrap(
              children: [
                CheckboxListTile(
                  value: this.isSelected2,
                  onChanged: (value) {
                    setState(() {
                      this.isSelected2 = value;
                    });
                  },
                  title: Text(
                      "多选框1"
                  ),
                  subtitle: Text("多选框1副标题"),
                  secondary: Icon(
                      Icons.category
                  ),
                  selected: this.isSelected2,
                ),
                CheckboxListTile(
                  value: this.isSelected3,
                  onChanged: (value) {
                    setState(() {
                      this.isSelected3 = value;
                    });
                  },
                  title: Text(
                      "多选框2"
                  ),
                  subtitle: Text("多选框2副标题"),
                  secondary: Icon(
                      Icons.settings
                  ),
                  selected: this.isSelected3,
                ),
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

实现：

![image-20210108215709533](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210108215709533.png)

### Radio单选按钮组件

![image-20210108215755405](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108215755405.png)

### RadioListTile 单选按钮组件

![image-20210108215804774](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210108215804774.png)

实例：

```dart
import 'package:flutter/material.dart';

class FormDemo extends StatefulWidget {
  @override
  _FormDemoState createState() => _FormDemoState();
}

class _FormDemoState extends State<FormDemo> {
  var groupValue;
  var groupValue2;


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '表单页',
          textAlign: TextAlign.center,
        ),
      ),
      // body: TextFiledDemo(),
      // body: CheckedDemo(),
      body: Container(
        child: ListView(
          children: [
            Container(
              child: Row(
                children: [
                  Text("男"),
                  Radio(
                    value: 1,
                    groupValue: this.groupValue,
                    onChanged: (v) {
                      setState(() {
                        this.groupValue = v;
                      });
                    },
                    activeColor: Colors.blue,
                  ),
                ],
              ),
            ),
            Container(
              child: Row(
                children: [
                  Text("女"),
                  Radio(
                    value: 2,
                    groupValue: this.groupValue,
                    onChanged: (v) {
                      setState(() {
                        this.groupValue = v;
                      });
                    },
                    activeColor: Colors.amber,
                  ),
                ],
              ),
            ),
            Wrap(
              children: [
                RadioListTile(
                    value: 1,
                    groupValue: this.groupValue2,
                    onChanged: (v) {
                      setState(() {
                        this.groupValue2 = v;
                      });
                    },
                  activeColor: Colors.blue,
                  title: Text("男"),
                  subtitle: Text("副标题1"),
                  secondary: Icon(
                    Icons.people
                  ),
                ),
                RadioListTile(
                    value: 2,
                    groupValue: this.groupValue2,
                    onChanged: (v) {
                      setState(() {
                        this.groupValue2 = v;
                      });
                    },
                  activeColor: Colors.amber,
                  title: Text("女"),
                  subtitle: Text("副标题2"),
                  secondary: Icon(
                    Icons.pregnant_woman
                  ),
                ),
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

实现：

![image-20210108221344517](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108221344517.png)

### Switch组件

![image-20210108221418477](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108221418477.png)

实例：

```dart
import 'package:flutter/material.dart';

class FormDemo extends StatefulWidget {
  @override
  _FormDemoState createState() => _FormDemoState();
}

class _FormDemoState extends State<FormDemo> {
  bool switchValue = false;


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '表单页',
          textAlign: TextAlign.center,
        ),
      ),
      // body: TextFiledDemo(),
      // body: CheckedDemo(),
      // body: RadioDemo(),
      body: Container(
        child: Switch(
          value: this.switchValue,
          onChanged: (v) {
            setState(() {
              this.switchValue = v;
            });
          },
          activeColor: Colors.blue,
        ),
      ),
    );
  }
}
```

实现：

![image-20210108222014354](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210108222014354.png)

### 日期和时间组件

日期转化为时间戳：

```dart
var now = new DateTime.now();
print(now.millisecondsSinceEpoch); //单位毫秒，13为时间戳
```

时间戳转化为日期：

```dart
var now = new DateTime.now();
var a = now.millisecondsSinceEpoch;
print(DateTime.fromMillisecondsSinceEpoch(a));
```

date_format 时间格式转换

文档：https://pub.dev/packages/date_format

```dart
dependencies:
  date_format: ^1.0.9



import 'package:date_format/date_format.dart';

main() {
  print(formatDate(DateTime(1989, 2, 21), [yyyy, '-', mm, '-', dd]));
  print(formatDate(DateTime(1989, 2, 21), [yy, '-', m, '-', dd]));
  print(formatDate(DateTime(1989, 2, 1), [yy, '-', m, '-', d]));

  print(formatDate(DateTime(1989, 2, 1), [yy, '-', MM, '-', d]));
  print(formatDate(DateTime(1989, 2, 21), [yy, '-', M, '-', d]));

  print(formatDate(DateTime(1989, 2, 1), [yy, '-', M, '-', d]));

  print(formatDate(DateTime(2018, 1, 14), [yy, '-', M, '-', DD]));
  print(formatDate(DateTime(2018, 1, 14), [yy, '-', M, '-', D]));

  print(formatDate(DateTime(1989, 02, 1, 15, 40, 10), [HH, ':', nn, ':', ss]));

  print(formatDate(
      DateTime(1989, 02, 1, 15, 40, 10), [hh, ':', nn, ':', ss, ' ', am]));

  print(formatDate(
      DateTime(1989, 02, 1, 15, 40, 10), [hh, ':', nn, ':', ss, ' ', am]));

  print(formatDate(DateTime(1989, 02, 1, 15, 40, 10), [hh]));
  print(formatDate(DateTime(1989, 02, 1, 15, 40, 10), [h]));

  print(formatDate(DateTime(1989, 02, 1, 5), [am]));
  print(formatDate(DateTime(1989, 02, 1, 15), [am]));

  print(
      formatDate(DateTime(1989, 02, 1, 15, 40, 10), [HH, ':', nn, ':', ss, z]));

  print(formatDate(
      DateTime(1989, 02, 1, 15, 40, 10), [HH, ':', nn, ':', ss, ' ', Z]));

  print(formatDate(DateTime(1989, 02, 21), [yy, ' ', w]));
  print(formatDate(DateTime(1989, 02, 21), [yy, ' ', W]));

  print(formatDate(DateTime(1989, 12, 31), [yy, '-W', W]));
  print(formatDate(DateTime(1989, 1, 1), [yy, '-', mm, '-w', W]));

  print(formatDate(
      DateTime(1989, 02, 1, 15, 40, 10), [HH, ':', nn, ':', ss, ' ', Z]));

  print(formatDate(DateTime(2020, 04, 18, 21, 14), [H, '\\h', n]));
}
```

组件国际化：

https://blog.csdn.net/u010960265/article/details/98731720

#### 第三方日期组件

实例：

```dart
import 'package:flutter/material.dart';
import 'package:date_format/date_format.dart';
import 'package:flutter_cupertino_datetime_picker/flutter_cupertino_datetime_picker.dart';

class DateTimeDemo extends StatefulWidget {
  DateTimeDemo({Key key}) : super(key: key);

  @override
  _DateTimeDemoState createState() => _DateTimeDemoState();
}


class _DateTimeDemoState extends State<DateTimeDemo> {
  bool _showTitle = true;
  DateTimePickerLocale _locale = DateTimePickerLocale.en_us;
  List<DateTimePickerLocale> _locales = DateTimePickerLocale.values;
  String _format = 'yyyy-MMMM-dd';
  TextEditingController _formatCtrl = TextEditingController();

  DateTime _dateTime;

  @override
  void initState() {
    super.initState();
    _formatCtrl.text = _format;
    _dateTime = DateTime.now();
  }

  void _showDatePicker() {
    DatePicker.showDatePicker(
      context,
      onMonthChangeStartWithFirstDate: true,
      pickerTheme: DateTimePickerTheme(
        showTitle: _showTitle,
        confirm: Text('确认', style: TextStyle(color: Colors.red)),
      ),
      minDateTime: DateTime(1970-1-1),
      maxDateTime: DateTime(2100-12-31),
      initialDateTime: DateTime.now(),
      dateFormat: 'yyyy-MMMM-dd',
      locale: DateTimePickerLocale.zh_cn,

      onChange: (dateTime, List<int> index) {
        setState(() {
          _dateTime = dateTime;
        });
      },
      onConfirm: (dateTime, List<int> index) {
        setState(() {
          _dateTime = dateTime;
        });
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '时间组件页',
          textAlign: TextAlign.center,
        ),
      ),
      body: Container(
        padding: EdgeInsets.all(16.0),
        child: Column(
          children: <Widget>[
            // selected date
            Container(
              margin: EdgeInsets.only(top: 40.0),
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.center,
                children: <Widget>[
                  Text('Selected Date:',
                      style: Theme.of(context).textTheme.subhead),
                  Container(
                      padding: EdgeInsets.only(left: 12.0),
                      child: InkWell(
                        child: Row(
                          mainAxisAlignment: MainAxisAlignment.center,
                          children: [
                            Text(
                              '${_dateTime.year}-${_dateTime.month.toString().padLeft(2, '0')}-${_dateTime.day.toString().padLeft(2, '0')}',
                            ),
                            Icon(Icons.arrow_drop_down),
                          ],
                        ),
                        onTap: _showDatePicker,
                      )),
                ],
              ),
            ),
          ],
        ),
      ),
      // display DatePicker floating action button
    );
  }
}
```

实现：

![image-20210110151215158](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210110151215158.png)

### Swiper组件

官方文档：https://pub.dev/packages/flutter_swiper#build-in-layouts

实例：

```dart
import 'package:flutter/material.dart';
import 'package:flutter_swiper/flutter_swiper.dart';

class SwiperDemo extends StatefulWidget {
  SwiperDemo({Key key}) : super(key: key);

  @override
  _SwiperDemoState createState() => _SwiperDemoState();
}

class _SwiperDemoState extends State<SwiperDemo> {
  List imgList = [{
      "url":'https://www.itying.com/images/flutter/1.png'
    },
    {
      "url":'https://www.itying.com/images/flutter/2.png'
    },
    {
      "url":'https://www.itying.com/images/flutter/3.png'
    },
    {
      "url":'https://www.itying.com/images/flutter/4.png'
    },
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '表单页',
          textAlign: TextAlign.center,
        ),
      ),
      body:  new Swiper(
        itemBuilder: (BuildContext context,int index){
          return new Image.network(imgList[index]["url"],fit: BoxFit.fill,);
        },
        itemCount: 4,
        pagination: new SwiperPagination(),
        control: new SwiperControl(),
      ),
    );
  }
}
```

实现：

![image-20210110160259315](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210110160259315.png)

实例二

```dart
import 'package:flutter/material.dart';
import 'package:flutter_swiper/flutter_swiper.dart';

class SwiperDemo extends StatefulWidget {
  SwiperDemo({Key key}) : super(key: key);

  @override
  _SwiperDemoState createState() => _SwiperDemoState();
}

class _SwiperDemoState extends State<SwiperDemo> {
  List imgList = [{
      "url":'https://www.itying.com/images/flutter/1.png'
    },
    {
      "url":'https://www.itying.com/images/flutter/2.png'
    },
    {
      "url":'https://www.itying.com/images/flutter/3.png'
    },
    {
      "url":'https://www.itying.com/images/flutter/4.png'
    },
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          '表单页',
          textAlign: TextAlign.center,
        ),
      ),
      body: Column(
        children: [
          Container(
            child: AspectRatio(
              aspectRatio: 16/9,
              child: Swiper(
                itemBuilder: (BuildContext context,int index){
                  return new Image.network(imgList[index]["url"],fit: BoxFit.fill,);
                },
                itemCount: 4,
                pagination: new SwiperPagination(),
                control: new SwiperControl(),
                autoplay: true,
                loop: true,
              ),
            ),
          )
        ],
      )
    );
  }
}
```

实现：

![image-20210110160512071](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210110160512071.png)

### Dialog组件

#### AlertDialog

实例：

```dart
_alertDialogShow() async{
  var result = await showDialog(
      context: context,
      builder:(context) {
        return AlertDialog(
            title:Text("我是alertDialog"),
            content: Text("请问您确定要删除吗？"),
          actions: [
            RaisedButton(
                child: Text("取消"),
                onPressed: () {
                  Navigator.pop(context,0);
                }
            ),
            RaisedButton(
                child: Text("确定"),
                onPressed: () {
                  Navigator.pop(context,1);
                }
            ),
          ],
        );
      }
  );
  print(result);
}
```

实现：

![image-20210111121922512](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111121922512.png)

#### SimpleDialog

实例：

```dart
_simpleDialogShow() async{
  var result = await showDialog(
      context: context,
      builder:(context) {
        return SimpleDialog(
            title: Text("我是SimpleDialog,请选择内容"),
          children: [
            SimpleDialogOption(
                child:Text("选项A"),
              onPressed: () {
                Navigator.pop(context,"A");
              },
            ),
            Divider(),
            SimpleDialogOption(
                child:Text("选项B"),
              onPressed: () {
                Navigator.pop(context,"B");
              },
            ),
            Divider(),
            SimpleDialogOption(
                child:Text("选项C"),
              onPressed: () {
                Navigator.pop(context,"V");
              },
            ),
            Divider(),
            SimpleDialogOption(
                child:Text("选项D"),
              onPressed: () {
                Navigator.pop(context,"D");
              },
            ),
            Divider(),
          ],

        );
      }
  );
  print(result);
}
```

实现：

![image-20210111121936858](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111121936858.png)

#### showModalBottomSheet

实例：

```dart
_modalBottomSheetShow() async{
  var result = await showModalBottomSheet(
      context: context,
      builder: (context) {
        return Container(
          height: 300,
          child: ListView(
            children: [
              ListTile(
                title: Text("分享A"),
                onTap: () {
                  Navigator.pop(context,"A");
                },
              ),
              Divider(),
              ListTile(
                title: Text("分享B"),
                onTap: () {
                  Navigator.pop(context,"B");
                },
              ),
              Divider(),
              ListTile(
                title: Text("分享C"),
                onTap: () {
                  Navigator.pop(context,"C");
                },
              ),
              Divider(),
              ListTile(
                title: Text("分享D"),
                onTap: () {
                  Navigator.pop(context,"D");
                },
              ),
            ],
          ),
        );
      }
  );
  print(result);
}
```

实现：

![image-20210111122002424](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111122002424.png)

#### showToast

实例：

```dart
toastShow() {
  Fluttertoast.showToast(
      msg: "我是toast！",
      toastLength: Toast.LENGTH_LONG,
      gravity: ToastGravity.BOTTOM,
      backgroundColor: Colors.black,
      textColor: Colors.white,
      fontSize: 16.0
  );
}
```

实现：

![image-20210111122036792](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111122036792.png)

#### 自定义dialog（添加定时）

实例：

```dart
_showMyDialog () {
  _showTimer(context);
  showDialog(
      context: context,
    builder: (context) {
        return MyDialog(title:"关于我们",content:"请认准我的唯一联系qq：337845818(3秒后关闭)");
      }
  );
}

_showTimer(context) {
  var timer;
  timer = Timer.periodic(Duration(milliseconds: 3000), (t) {
           Navigator.pop(context);
           t.cancel();
        }
    );
}
```

实现：

![image-20210111131017331](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111131017331.png)

## 网络请求

### JSON字符串和Map类型转换

json字符串——Map

```
print(json.decode(jsonData));
```

Map——json字符串

```
print(json.encode(mapData));
```

### 使用http库进行网络请求

#### get请求

```dart
List dataList = [];

_getData() async {
  var apiUrl = "http://a.itying.com/api/productlist";
  var result = await http.get(apiUrl);
  if (result.statusCode == 200) {
    print("请求成功 ${result.statusCode}");
    setState(() {
      this.dataList = json.decode(result.body)["result"];
    });
  } else {
    print("请求失败 ${result.statusCode}");
  }
}
```

实现：

![image-20210111141028335](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111141028335.png)

#### post请求

```dart
_postData() async {
  var apiUrl = "http://a.itying.com/api/productlist";
  var result =
      await http.post(apiUrl, body: {'name': 'doodle', 'color': 'blue'});
  if (result.statusCode == 200) {
    print("上传成功 ${result.statusCode}");
  } else {
    print("上传失败 ${result.statusCode}");
  }
}
```

### Dio库实现网络请求

#### get请求

```dart
List dataList = [];
_getData() async {
    var apiUrl = "http://a.itying.com/api/productlist";
    try {
      Response result = await Dio().get(apiUrl);
      print("请求成功 ${result.statusCode}");
      setState(() {
        this.dataList = result.data["result"];
      });
    } catch (e) {
      print(e);
    }
  }
```

实现：

![image-20210111145342663](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210111145342663.png)

#### post请求

```dart
_postData() async {
    var apiUrl = "http://a.itying.com/api/productlist";
    try{
      Response result = await Dio().post(apiUrl, data: {"id": 12, "name": "wendu"});
      print("上传成功 ${result.statusCode}");
    } catch(e) {
      print(e);
    }
  }
```