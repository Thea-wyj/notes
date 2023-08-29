# flutter学习记录总结

### 学习过程

构建项目 封装好工具类 照着钉钉编写页面 随写随添加插件和工具类

### 目录结构介绍与框架搭建

![image-20210219180252594](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210219180252594.png)

![image-20210219180627143](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210219180627143.png)

### 已用插件介绍

https://pub.flutter-io.cn/

![image-20210220120839067](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220120839067.png)

#### sharedPreferences

本地数据存储  

调用异步方法setInstance方法来初始化一个sharePreferences对象

![image-20210220120036097](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220120036097.png)

![image-20210219185248627](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210219185248627.png)

之后通过这个对象调用相应方法来进行存取操作

![image-20210219185301000](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210219185301000.png)

![image-20210219185338641](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210219185338641.png)

#### crypto

包含了一套基于dart的工具集

我们用的是md5 封装了一个string2md5的方法 直接调用即可

![image-20210220120939045](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220120939045.png)

#### toast

![image-20210220121351953](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220121351953.png)

#### easyLoading

加载动画的插件 直接调用显示和退出方法即可

```
EasyLoading.show();
EasyLoading.dismiss();
```

![image-20210220121704305](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220121704305.png)

#### provider

就是便于页面间和页面内数据操作和页面根据数据变化进行刷新的一个工具

如果有页面需要根据数据动态渲染或者某个页面需要其他页面的数据时需要使用

使用步骤：

1. 在provider文件夹里定义provider实体 并定义数据更新方法 

   以loginProvider为例

   ![image-20210220122243566](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210220122243566.png)

2. 在provider.dart文件里面实例化并引入该provider

   ![image-20210220122416836](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220122416836.png)

3. 然后就可以在你想使用的页面中进行使用了

   使用分为两种 一个是修改该provider的值，此时需要用 content.read方法

   ```dart
   context.read<LoginProvider>().updateLoginProvider(
       loginId: this.loginIdController.text,
       password: this.pwdController.text
   );
   ```

   一种是将provider的值与页面内容进行绑定，此时首先要用Consumer组件将想要绑定的内容进行包裹才能达到双向绑定 用的时候直接provider.就行了

   ```dart
   Consumer(builder: (context, LoginProvider provider, child) {
         return TextField(
           controller: this.loginIdController,
           decoration: InputDecoration(
             icon: Icon(Icons.account_circle_rounded),
             labelText: "用户名",
             labelStyle: TextStyle(fontSize: 18),
             suffixIcon: provider.loginId == ""
                 ? null
                 : GestureDetector(
                     onTap: () {
                       this.loginIdController.text = "";
                       changeText();
                     },
                     child: Icon(
                       Icons.cancel,
                       color: Color.fromRGBO(162, 162, 164, 1),
                     ),
                   ),
           ),
           onChanged: (value) {
             changeText();
           },
         );
       });
   ```

   #### giffyDialog

   带动图的提示框

   ![image-20210220123508537](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220123508537.png)

   方法已经封装好 直接调用

   ![image-20210220123343877](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220123343877.png)

   #### getWidget

   https://github.com/ionicfirebaseapp/getwidget

   提供大量组件的UI库 引用完直接使用其中组件即可

   #### flutterAppUpgrade

   提示升级的窗口  使用方法参考文档

   ![image-20210220123931724](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220123931724.png)

   #### 16进制颜色转化

   flutter的color组件只接受int型数据，通过HexUtil类里的方法我们可以通过16进制的数据来获取颜色

   ![image-20210220130352877](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220130352877.png)

   ```dart
   color: Color(HexUtil.getColorFromHex("448AFF"))
   ```

### 页面编写流程及代码规范

首先要在对应的位置**创建**页面对应的文件夹和dart**文件** 

`命名规则： **单词小写 用下划线隔开** 如果是整个页面 就用xxx_page 如果是组件就直接用组件的名字英译 **要直观**`

其次进行页面或者组件的**编写**

此时，引用其他文件的内容时 选择**绝对路径**的方法

```dart
import 'package:sc_oa/util/get_preferences.dart';
```

在编写多个组件组合而成的页面或者组件时  应**将每个单独的组件抽离出来** 定义一个返回该组件的方法 在最外层调用这些方法实现页面的加载  来保证代码的可读性和层次性

![image-20210220125056923](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210220125056923.png)

再次，涉及到**网络请求**的地方 首先要在entity文件夹中定义好请求实体和响应实体

https://javiercbk.github.io/json_to_dart/

再调用post方法进行网络请求，此时参数要以请求实体的形式传入，直接使用实体的构造函数即可

成功的回调函数写在post的.then回调函数里面，成功后要进行响应实体的实例化再进行使用；

post的错误处理写在.then的onError参数里  ，显示错误信息直接调用封装好的错误处理函数即可

```
Code.errorHandle(context,code: e.code, msg: e.msg);
```

涉及到**引用本地资源文件**时 要先将文件放在asset文件夹对应的目录内

还要在.yaml文件内配置好，注意配置文件内的空格表示对应的层次关系 要空对

![image-20210220130254566](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210220130254566.png)

涉及到**引用其他插件**的要记得在配置文件内写好并get后再import进去

如果大量使用可以考虑封装起来放到util文件夹或者widget文件夹中

设计**页面跳转**的时候在route文件里面定义好路由信息

```dart
final routes = {
  '/index': (context) => NavTab(),
  '/search': (context) => ArticleSearch(),
  '/login': (context) => LoginPage(),
  '/settings': (context) => SettingsPage(),
  '/security': (context) => SecurityCenter(),
};
```

使用的时候直接调用这个文件里面的值就可以了

```dart
Navigator.pushNamed(context, '/settings');
```

by the way 我们封装的route也包含了传值路由的功能

大地老师视频：https://www.bilibili.com/video/BV1S4411E7LY?p=4

```dart
//定义
final routes={
  '/productInfo':(context,{arguments})=>ProductInfo(arguments:arguments),
};
//带值跳转
Map pid = {
    "count":123
};
Navigator.pushNamed(context, "/productInfo",arguments: pid);
//取值
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

涉及到**使用provider**的内容要按照前面介绍的步骤按步执行

最后 编写完可以**打包成安装包**供安卓机上机调试 方法自行百度

最后的最后 写代码的时候还是要写好注释 灵活运用ctrl+alt+l啊