### react 异步请求应该放在哪个生命周期中
  - 有人说请求放在componentWillMount中执行，可以提前加载数据，在React 16之后有三个生命周期被废弃(但并未删除)。再者，服务端进行渲染时会执行一次componentWillMount，浏览器环境也会执行一次componentWillMount，这就造成了2次请求，在React 16进行React Fiber重写后,componentWillMount可能在一次渲染中多次调用.
  - 由于JavaScript异步的特效，执行一次生命周期，并不会等到componentWillMount中完成所有的事情，去render，并没办法等到数据返会，暂停渲染；
  - 官方推荐异步请求放在componentDidMount周期中；

### setState是异步还是同步
  有时候是异步，有时候是同步
  1. 在合成事件和生命周期中setState是异步的，在原声事件和定时器中setState是同步的；
  2. setState异步并不是说代码是异步的，其实本身执行是过程和代码是同步的，
  合成事件和生命周期的调用顺序在更新之前，导致在它们之中，不能立马拿到改变后的值。即形成了所谓的‘异步’，但是setState(partialState, callback)中的callback可以立马拿到更新后的值；
  3. setState的批量更新优化，就是建立在合成事件和生命周期之上的，多次设置同一个值时，只会对最后一次设置有效，把其他的值合并，再更新；但是原生事件和定时器中setState会立马更新；

### React组件通信如何实现
  1.父向子组件通过props传递；
  2.子向父组件通过props+回调的方式，子组件调用父组件的方法（把子组件中的信息作为参数）;
  3.兄弟组件通信,找到最近的父节点，通过上面的2种方式进行通信；
  4.跨层级组件通信，可以使用Context为组件树共享全局的数据；
  5.发布订阅模式（事件驱动）,通过订阅事件，加上发布事件进行通信；
  6.全局状态管理工具: 借助Redux或者Mobx等全局状态管理工具进行通信,这种工具会维护一个全局状态中心Store,并根据不同的事件产生新的状态；

### React逻辑复用
  1.高阶组件
    - 属性代理
    - 反向劫持（super.render() super指向继承的组件，并且指向子组件的this）
  2.属性渲染
  3.react-hook      
