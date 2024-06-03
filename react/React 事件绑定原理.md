#### 为什么要有合成事件

* 浏览器兼容
* 更好的支持跨平台
* 方便 React 进行统一管理，更好的控制事件的执行链路

#### 事件特性

* 17之后事件委托到 root节点上，之前委托在document节点上
* 去除事件池
* onscroll事件不再冒泡
* react的 onFouce、onBlur切换为原生事件
* 捕获事件使用的是浏览器中的捕获监听器

#### 事件注册

registerEvents 初始化原生事件，react事件和原生事件的对应关系，并给 allNativeEvents 集合注入原生事件名

#### 事件绑定

1. ReactDOM.render 时调用 listenToAllSupportedEvents来绑定所有事件到根节点上
   1. 细节：支持冒泡的事件，在捕获和冒泡阶段都绑定事件，不支持的就只绑定捕获事件
   2. 调用 addEventListener 绑定事件
   3. 获取不同事件的优先级，在绑定事件时使用不同的回调函数，底层都是调用dispatch函数
2. react对不支持冒泡的事件，都是直接绑定在元素本身

#### 事件触发

1. dispatchEvent调用链路
   1. attemptToDispatchEvent 尝试调度事件
      1. 获取事件触发dom元素
      2. 获取 dom元素对应的fiber节点
      3. 通过react事件系统，进行事件派发
   2. dispatchEventForPluginEventSystem 会收集fiber节点上事件，并派发，批量更新
2. 合成事件
   遍历fiber树，收集同类事件到dispatchQueue队列
   1. 根据原生事件名得到react事件名，获取不同的事件构造函数
   2. 从当地fiber节点触发，分别在捕获和冒泡节点完成事件的收集
   3. 往事件派发队列添加事件 dispatchQueue添加事件
3. 事件派发
   遍历dispatchQueue队列，执行listener事件
   react模拟捕获冒泡，正是对dispathQueue的正序倒叙遍历实现的
4. 核心流程


1. React 代码执行时，顶层会自动执行事件的注册，初始化事件插件。
2. React 首次渲染时，会在根节点上绑定所有原生事件。支持冒泡的事件，React 会同时绑定捕获阶段和冒泡阶段的事件；不支持冒泡的事件，会将事件绑定在具体 DOM 元素上。
3. 事件触发前会从目标元素的 Fiber 节点向上收集同类型事件队列，构造合成对象，同类型的事件会复用同一个合成事件实例对象。
4. 根据监听的事件阶段，决定顺序还是倒序遍历执行事件处理函数（模拟事件的冒泡捕获机制）。
