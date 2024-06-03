1. beginWork 递
   * mount
     * 生成fiber树
   * update
     * 标记flags
     * 可复用存在的fiberNode
     * diff生成fiberNode
2. completeWork 归
   * mount
     * 从下到上生成离屏DOM树
   * update
     * 跟新DOM节点属性等
     * flags冒泡
3. commit
