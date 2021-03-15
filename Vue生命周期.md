#### Vue生命周期

vue生命周期总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

> 创建前/后：在beforeCreated阶段，vue实例的挂载元el还没有。
> 载入前/后：在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。在mounted阶段，vue实例挂载完成，data.message成功渲染。
> 更新前/后：当data变化时，会触发beforeUpdate和updated方法。
> 销毁前/后：在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在。

#### Vue双向绑定原理

具体步骤：

> 第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter和getter。这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化
> 第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
> 第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:
> 1、在自身实例化时往属性订阅器(dep)里面添加自己
> 2、自身必须有一个update()方法
> 3、待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。
> 第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

#### Vue.js的template编译的理解

首先，通过compile编译器把template编译成AST语法树（abstract syntax tree 即 源代码的抽象语法结构的树状表现形式），compile是createCompiler的返回值，createCompiler是用以创建编译器的。另外compile还负责合并option。
然后，AST会经过generate（将AST语法树转化成render funtion字符串的过程）得到render函数，render的返回值是VNode，VNode是Vue的虚拟DOM节点，里面有（标签名、子节点、文本等等）

- **event & v-model: 事件和v-model的实现原理**

- **slot & keep-alive: 内置组件的实现原理**

- **transition: 过渡的实现原理**

- **vue-router: 官方路由的实现原理**

- #### **vuex: 官方状态管理的实现原理**

  

tset

