> &emsp;因为开发中经常用到生命周期的函数,后来查看了Vue的官方文档以及一些博客,结果都不能让自己满意,后续查看了Vue2.0的源码,大致了解了下生命周期的本质,下面来简单分析一下.
<br>
&emsp;关于如何查看Vue源码的，网上已有很多文章,本人不做过多介绍,我参考了360一位工程师的解析目录



<p>这段代码是init.js文件关于Vue的构造函数</p>

```
    initLifecycle(vm)
    initEvents(vm)
    callHook(vm, 'beforeCreate')
    initState(vm)
    callHook(vm, 'created')
    initRender(vm)
```
initLifecycle主要功能是为了初始化一些数据比如_watcher,$parent等

```
  vm.$parent = parent
  vm.$root = parent ? parent.$root : vm

  vm.$children = []
  vm.$refs = {}

  vm._watcher = null
  vm._inactive = false
  vm._isMounted = false
  vm._isDestroyed = false
  vm._isBeingDestroyed = false
```
initEvents主要是调用 _updateListeners更新父元素的监听,在此之后可以调用
$emit触发事件;
```
const listeners = vm.$options._parentListeners
const on = bind(vm.$on, vm)
const off = bind(vm.$off, vm)
vm._updateListeners = (listeners, oldListeners) => {
updateListeners(listeners, oldListeners || {}, on, off)
}
if (listeners) {
vm._updateListeners(listeners)
}
```

```
    vm._watchers = []
    initProps(vm)
    initData(vm)
    initComputed(vm)
    initMethods(vm)
    initWatch(vm)

```


