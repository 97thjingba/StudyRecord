
|  |  useCallback|useMemo  |
|--|--|--|
| 返回值|返回缓存的函数的引用  |返回缓存的变量 |
| 使用场景|一般用在父子组件传递props，优化子组件 |一般使用在子组件优化以及含有大量计算逻辑的函数体中|
|通俗来讲|第一个函数体内不含return|函数体内含return|
|空deps[]|意味着方法没有依赖值，将不会更新|没有依赖值，不会进行更新|
||||

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4ODc3MDAwMSwtNTE0NTI4NDc5LDExOD
M3OTE0ODNdfQ==
-->