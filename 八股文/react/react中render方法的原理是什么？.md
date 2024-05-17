1. 两种形式：
   1. 类组件中的render方法
   2. 函数组件本身的返回值
2. 返回值
   1. 返回JSX
   2. JSX经过编译会调用CreateElement方法，生产虚拟 DOM树
   3. 新旧 DOM树进行 diff ，更新DOM树
3. 触发时机
   1. 类组件调用setState
   2. 函数组件通过useState Hook
4. 父子组件渲染
   1. 父组件重新渲染，子组件也会重新渲染
   2.
