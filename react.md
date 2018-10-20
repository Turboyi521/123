##1. react组件对象的3大属性
	1). state: 值为容器对象, 保存的是组件内可变的数据,组件根据state中的数据显示, 要更新界面只要更新state即可 
	2). props: 值为容器对象, 保存的是从组件外传递过来的数据, 当前组件只读, 父组件修改了自动显示新数据
	3). refs: 值为容器对象, 保存的是n个有ref属性的dom元素对象, 属性名是ref指定的标识名称, 值为对应的dom元素

##2. React组件化编码的3步与2个重要问题
	1). 拆分组件
	2). 实现静态组件
	3). 实现动态组件
		a. 动态显示初始化数据
		b. 交互

##3. package.json的结构
	{
		"name": "react-demo", // 标识名称
		"version": "1.0.0", // 版本号
		"scripts": { // 打包运行相关的npm命令
			
		},
		dependencies: {}, // 运行时依赖
		devDependencies: {} // 开发时依赖
	}

##4. 脚手架的理解
	1). 用来创建基于某个特定库(react/vue)的模板项目的工具包
	2). 全局下载脚手架后, 就会多出一个命令, 通过命令就可以创建项目
	3). 创建出的项目已经是有完整配置, 依赖声明的一个模块化/组件化/工程化的项目

##5. 项目的开发环境运行与生产环境打包运行
	1). 开发环境运行
		a. 命令:
			npm start
		b. 背后做了什么
			在内存中生成打包文件(不生成本地打包文件)
			启动服务器运行内存中的打包文件
	2). 生产环境打包运行
		a. 命令
			npm run build
			serve build
		b. 背后做了什么
			在内存中生成打包文件
			生成本地打包文件
			启动服务器加载运行本地打包文件

##6 react应用中如何与后台通信?
	1). 通过ajax请求与后台交互, 但react本身并不包含ajax语法封装, 需要使用第三方ajax库
	2). 可以使用axios/fetch来发送ajax请求
	3). 发请求的时机/位置:
		a. 初始化请求: componentDidMount()
		b. 用户操作后请求: 事件回调函数或相关位置 

##7. 对事件处理机制的理解
	1). DOM事件
		* 绑定事件监听
			* 事件名(类型): 只有有限的几个, 不能随便写
			* 回调函数
		* 用户操作触发事件(event)
			* 事件名(类型)
			* 数据
	2). 自定义事件
		* 绑定事件监听
			* 事件名(类型): 任意
			* 回调函数: 通过形参接收数据, 在函数体处理事件
		* 触发/分发(dispatch)事件(编码)
			* 事件名(类型): 与绑定的事件监听的事件名一致
			* 数据: 会自动传递给回调函数

##8. react组件间通信
	1). 方式一: 通过props传递
		通过props可以传递一般数据和函数数据, 
		一般数据-->父组件向子组件
		函数数据-->子组件向父组件通信
		缺点: 只能一层一层传递/兄弟组件必须借助父组件
	2). 方式二: 使用消息订阅(subscribe)-发布(publish)机制
		实现库: pusub-js
		组件A: 发布消息(相当于触发事件)
		组件B: 订阅消息, 接收消息, 处理消息(相当于绑定事件监听)
		优点: 对组件关系没有限制

##9. 开发中常用的ES6新语法
	定义变量/常量: const/let
	解构赋值: let {a, b} = this.props / import {aa} from 'xxx' / function f ({name}) {}
	对象的简洁表达: {a, b, c () {}}
	箭头函数: 
		组件的自定义方法: xxx = () => {}
		匿名函数作为实参
		优点:
			* 简洁
			* 没有自己的this,使用引用this查找的是外部this
	扩展运算符: ...
		拆解对象:  const MyProps = {}, <Xxx {...MyProps}>
	类: class/extends/constructor/super
	ES6模块化: export/default/import
	异步: promise, async/await
##10. 对react-router的理解
	1). 下载: npm install --save react-router-dom
	2). 是什么: 用来实现SPA的react插件
	3). 相关API:
		a. 组件
            <HashRouter> / <BrowserRouter>
            <Route>
            <Redirect>
            <NavLink> / <Link>
            <Switch>
        b. 对象或函数
            props.history对象
            props.match对象
            props.location对象
            withRouter函数

##11. 区别UI组件与容器组件
	1). react-redux将组件分成2种: UI组件与容器组件
	2). UI组件
		不直接使用任何redux相关API, 
		作用: 主要做界面展现, 需要接受属性显示数据或更新显示
		如果需要与redux交互, 就需要包装生成对应的容器组件
	3). 容器组件
		通过connect函数生成的组件
		作用: 不做任何显示, 责任就是连接redux与UI组件, 向UI组件传递属性

#12. 对redux的理解
	1). redux是一个独立专门用于做状态管理的JS库(不是react插件库)
	2). 可以与任何前端库配合使用, 但最合适的是与react库配合
	3). 作用: 集中式管理react应用中多个组件共享的状态
	4). 提供的API:
		createStore()
		applyMiddleWare()
		combineReducers()
		store.getState()/dispatch()/subscribe()
		
##13. redux结构图
![](https://i.imgur.com/IDGQZRq.png)

##14.  2种类型的数据容器比较
	1). 对象: 包含n个无序数据, 通过标识属性名来操作属性值数据, 如果有属性名可以瞬间得到对应的数据, 否则需要遍历
	2). 数组: 包含n个有序数据, 通过下标来操作元素数据, 如果确定下标可以瞬间得到对应数据, 否则必须遍历
##15. 什么是API接口
	1). url
	2). 请求方式 
	3). 请求参数格式
	4). 响应数据格式

##16. 说说你对路由的理解
	1). 路由是什么?
		就是一个key:value的映射关系
	2). 路由的分类?
	  	a. 后台路由: path---callback
	  	b. 前台路由: path---component
	3). 作用?
	  	a. 后台路由: 当服务器接收到请求时, 根据请求的path找到对应的路由, 由路由的回调函数来处理请求, 返回响应
	  	b. 前台路由: 当请求某个路由地址时, 根据请求的path找到对应的路由, 显示路由对应的组件界面
## 17. 使用git管理你的项目(创建2个分支)
	1). 创建本地仓库
		创建.gitignore文件, 并添加需要忽略的文件/夹
		git init
		git add *
		git commit -m "init"
	2). 创建远程仓库
		登陆github
		new Repository
		指定仓库名
		确认创建
	3). 将本地仓库推送到远程仓库
		关联远程仓库: git remote add origin url
		推送: git push origin master
	4). 在本地创建xxx分支, 并推送到远程xxx分支
		git branch xxx
		git checkout xxx
		git push origin xxx
	5). 克隆仓库(2个分支)
		git clone url
		git checkout -b dev origin/dev
## 18. 后台路由回调函数处理的3步
	1). 获取请求参数数据: 使用req
	2). 处理数据: 逻辑计算和操作数据库
	3). 返回响应数据: 使用res

## 19. GET请求的2种请求参数
	query参数: 
		路由path: /register
		请求path: /register?username=xxx&password=yyy   
		获取参数: req.query.username
	param参数: 
		路由path: /register/:username  
		请求path: /register/xxx   
		获取参数: req.params.username

## 20. 说说你对commonjs模块化规范的理解
	1). 暴露模块
		向外暴露的永远是exports, exports的默认值为{}
		方式一: module.exports = value
		方式二: exports.xxx = value1 exports.yyy = value2
	2). 引入模块
		const module = require('模块名/模块路径')

## 21. 对代理的理解
	1). 是什么?
      	具有特定功能的程序
    2). 运行在哪?
        前台应用端
        只能在开发时使用
    3). 作用?
		解决开发时的ajax请求跨域问题
	        a. 监视并拦截请求(3000)
	        b. 转发请求(4000)
	4). 配置代理
        告诉代理一些信息: 转发的目标地址

## 22. redux的基本编码
	1). redux
		store.js
	      生成并暴露一个store管理对象
	    reducers.js
	      包含n个reducer函数
	      根据老state和指定action来产生返回一个新的state
	    actions.js
	      包含n个action creator函数
	      同步action: 返回一个action对象({type: 'XXX', data: xxx})
	      异步action: 返回一个函数: disptach => {执行异步代理, 结束时dispatch一个同步action}
	    action-types.js
	      包含n个同步action的type名称常量
	2). 入口JS
		<Provider store={store}>
	3). 组件
		export default connect(
              state => ({xxx: state.xxx}),
              {action1, action2}
        )(UI组件)
##23. 区别UI组件与容器组件
	1). react-redux将组件分成2种: UI组件与容器组件
	2). UI组件
		不直接使用任何redux相关API, 
		作用: 主要做界面展现, 需要接受属性显示数据或更新显示
		如果需要与redux交互, 就需要包装生成对应的容器组件
	3). 容器组件
		通过connect函数生成的组件
		作用: 不做任何显示, 责任就是连接redux与UI组件, 向UI组件传递属性

##24. async/await?
	1). 作用?
	    简化pormise的使用(不用再使用then()来指定成功或失败的回调函数)
	    以同步编码的方式实现异步流程(没有回调函数)
	2). 哪里使用await?(在某条语句的左侧加)
	    返回promise对象的语句, 为了直接得到异步返回的结果, 而不是promsie对象
	3). 哪里使用async? (在某个函数定义左侧)
	    使用了await的函数

##25. 比较react中组件间3种通信方式
	1). 方式一: 通过props传递
		通过props可以传递一般数据和函数数据, 
		一般数据-->父组件向子组件
		函数数据-->子组件向父组件通信
		缺点: 只能一层一层传递/兄弟组件必须借助父组件
	2). 方式二: 使用消息订阅(subscribe)-发布(publish)机制
		实现库: pusub-js
		组件A: 发布消息(相当于触发事件)
		组件B: 订阅消息, 接收消息, 处理消息(相当于绑定事件监听)
		优点: 对组件关系没有限制
	3). 方式三: redux
		通过redux可以实现任意组件间的通信
		集中式管理多个组件共享的状态, 而pubsub-js并不是集中式的管理

## 26. 对cookie的理解(分类, 创建, 保存, 使用)
	cookie由key和value组成的文本小数据
	分类: 会话cookie和持久化cookie
	由服务器端创建: res.cookie(key, value, {maxAge: 1000})
	由浏览器端保存: 浏览器接收到新的cookie会自动保存(内存/文件)
	使用: 浏览器发送请求时自动携带对应的cookie, 服务器端通过req读取: req.cookies.key

## 27. 组件的二种分类
	1). 路由组件和非路由组件  ---react-router-dom
	2). 容器组件和UI组件   ---->react-redux

## 28. src下的各个文件/夹及其说明
	|--api          ajax请求后台接口
	|--assets        共用资源文件夹
		|--css
		|--images
	|--components   UI组件
	|--containers   容器组件
	|--redux        redux相关
		|--actions.js
		|--action-types.js
		|--reducers.js
		|--store.js
	|--util         工具
	|--index.js     入口

## 29. chrome调试应用的常用功能(窗口)
	Elements: 查看DOM标签和样式
	Console: 查看打印和错误信息
	NetWork: 查看请求(url, 请求方式, 请求参数)和响应
	Application: 查看浏览器端存储(localStorage, sessionStorage, cookie)
	Sources: debugger调试

	react: 查看react组件(state, props)
	redux: 查看redux管理的state
## 30. 对事件机制与消息机制的理解
	1). 事件机制
		a. 绑定事件监听: 事件名和回调函数
		b. 触发(分发)事件: 事件名和数据
	2). 消息机制
		a. 订阅消息: 消息名和回调函数, 相当于绑定事件监听
		b. 发布消息: 消息名和数据, 相当于分发事件 

## 31. 对变量提升与函数提升的理解
	变量提升: 在变量语句前就可以读取到变量, 值为undefined
	函数提升: 在函数定义语句前就可以调用函数
	原因: JS引擎在运行全局代码或执行函数前有预处理/解析

## 32. 原型链的理解
	作用: 原型链用于查找对象的属性
	什么: 实例对象上都会有一个隐式原型属性(__proto__), 它指向的就是原型对象, 而原型对象也有__proto__属性指向它的原型对象
	为什么__proto__指向的是原型对象?
		构造函数对象上有显式原型属性(prototype), 它指向的就是原型对象
		实例对象的__proto__属性被赋值为构造函数的prototype属性值