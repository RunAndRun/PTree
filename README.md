说明：

iview 本身也有tree组件。但是 iview的tree， 子节点都不选中时，父节点会自动变为不选中状态。
跟我的项目实际需求不符合（需求：1级菜单/2级菜单/2级菜单页面上的按钮。这时有可能存在：没有按钮权限，但是有查看页面权限的情况）。
所以写了一个simple版的tree组件。样式可以根据具体场景自己调整。至少需要 title/checked/children 3个字段。 还可以添加字段，用来判断有没有勾选的权限。

使用场景：

例如：项目后台的菜单权限管理

![Image text](https://raw.githubusercontent.com/RunAndRun/PTree/master/src/assets/style.png)

要求的数据格式：

![Image text](https://raw.githubusercontent.com/RunAndRun/PTree/master/src/assets/data.png)
