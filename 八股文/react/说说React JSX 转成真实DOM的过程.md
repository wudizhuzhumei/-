JSX => 虚拟 DOM

1. JSX 经过Babel 转为 React.createElement 的形式
2. React.createElement  方法内部会处理props/children 最终返回ReactElement

   * ReactElement包含的属性
     * type
     * key
     * ref
     * props
     * owner
     * 不可见数学 $$typeof ，可用来判断是否是ReactElement

虚拟 DOM => 真实 DOM

1. ReactDOM.render将虚拟DOM渲染到真实DOM上，
