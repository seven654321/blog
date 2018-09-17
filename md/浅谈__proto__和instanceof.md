>  先引入一段代码
```
const rootObj=Object.prototype;
console.log(rootObj.valueOf,rootObj.__proto__);
//native code,null
```
> Object.prototype对应的地址设为根对象,记为rootObj,接下来我们来分段查看一下另外几组对照


```
console.log(Function.prototype.__proto__===Object.prototype);//true
```
> Function.prototype对应的是rootObj作为原型创建的实例,包含rootObj的所有方法,命名为fnObj,然后我们就有了这两个基础fnObj

``` 
console.log(Function.__proto__===Function.prototype);//true
```
>  Function函数是Function类的实例 (包含 fnObj 的所有方法),这个是设计上的一大错误
```
console.log(Array.__proto__===Function.prototype);//true
console.log(Object.__proto__===Function.prototype);//true
```
> Array函数是Function类的实例 (包含 fnObj 的所有方法),Object是Function类的实例(包含 fnObj 的所有方法)
```
console.log(Object.__proto__.__proto__===Object.prototype);//true
```
> Object作为实例，(它的类的原型)的类是它自身,这个是第二个设计上的错误,真正起源在于Object.__proto__===Function.prototype

> <b>总结</b>
<br>
其实总结起来很简单,只有两个特别的Obj,一个是fnObj,一个是rootObj,所有的这些都是这两个搞出来的

>下面来谈谈为什么instanceof为什么不靠谱，instanceof 不是一个靠谱的实例判断关键词,参见如下代码,可以看出instanceof是递归查找__proto__*/
```
  // function instance_of(L, R) {//L 表示左表达式，R 表示右表达式
//  var O = R.prototype;// 取 R 的显示原型
//  L = L.__proto__;// 取 L 的隐式原型
//  while (true) { 
//    if (L === null) 
//      return false; 
//    if (O === L)// 这里重点：当 O 严格等于 L 时，返回 true 
//      return true; 
//    L = L.__proto__; 
//  }   

```
```
// console.log(Object instanceof Object);//true 
// console.log(Function instanceof Function);//true 
// console.log(Function instanceof Object);//true 
// console.log(Function instanceof Object);//true 

```

>  这里就看出来为什么不靠谱了,鸡生蛋蛋生鸡的问题,涉及到伦理问题了,稍微有点乱

> 再来谈谈__proto__为什么靠谱,看如下代码
```
let str3=new String('dd');  str3.__proto__={a:1}; str3 instanceof String;
```

> __pro__居然是可写的,所以用它来判断类貌似也不对哦,很弱的判断,那么基于__pro__的instance我就不说有多不靠谱了


















