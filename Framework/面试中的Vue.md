# 面试中的Vue

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## Vue

### MVVM

MVVM 是 Model-View-ViewModel 的缩写 ：

- Model代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑
- View 代表UI 组件，它负责将数据模型转化成UI 展现出来
- ViewModel 监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步View 和 Model的对象，连接Model和View。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

### 生命周期

![lifecycle](./images/lifecycle.png)

Vue生命周期：Vue 实例从创建到销毁的过程，从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、销毁等一系列过程，称之为 Vue 的生命周期。

作用：它的生命周期中有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。

生命周期钩子：8个，beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、beforeDestory、destoryed

第一次页面加载会触发哪些钩子函数：beforeCreate、created、beforeMount、mounted

Dom 渲染在哪个周期中就已经完成：mounted
