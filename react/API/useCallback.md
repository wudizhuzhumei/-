### 要点

1. 不会阻止创建新函数，只是返回缓存的函数引用
2.

### 有意义的使用方法

1. 传递函数到一个被 memo 包裹的组件，这时候不希望这个函数一直是新的，可以使用useCallback包裹
2. 一个函数被其他hook作为依赖
