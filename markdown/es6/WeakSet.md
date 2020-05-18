### WeakSet

`WeakSet`对像允许你将弱保持对象存储在一个和集中

~~~ javascript
new WeakSet([iterable])
~~~

> iterable 如果传入一个可迭代对象作为参数，则该对象的所有迭代值都会被自动添加进生成的`WeakSet`对象中，null被认为是undefined

**描述**

WeakSet对象是一些对象值的合集,并且其中的每个对象都只能出现一次。在WeakMap的集合中是唯一的

**区别**

* 与Set相比，WeakSet只能是对象的合集，而不能是任何类型的值
* WeakMap持弱引用：集合中对象的引用为弱引用。如果没有其他的对WeakSet中对象的引用，那么这些对象会被当成垃圾回收掉。这也意味着WeakSet中没有存储当前对象的列表。正是因为这样，WeakSet是不可枚举的

**检测循环引用**

递归调用自身的函数需要一种 通过跟踪哪些对象已被处理，来对应循环数据结构的方法。

为此，WeakSet非常适合处理这种情况：

```javascript
// 对 传入的subject对象 内部存储的所有内容执行回调
function execRecursively(fn,subject,_refs=null){
  if(!_refs){
    _refs=new WeakSet();
  }
  //避免无限递归
  if(_refs.has(subject)){
		return false;
  }
  fn(subject);
  if("object"==typeof subject){
		_refs.add(subject);
    for(let key in subject){
      execRecursively(fn ,subject[key],_refs)
    }
  }
}
const foo={
  foo:"Foo",
  bar:{
    bar:"bar"
  }
};
foo.bar.baz=foo;//循环引用！
execRecursively(obj=>console.log(obj),foo)
```



### 方法

- [`WeakSet.prototype.add(value)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WeakSet/add)

   在该 `WeakSet` 对象中添加一个新元素 `value`.

- [`WeakSet.prototype.delete(value)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WeakSet/delete)

  从该 `WeakSet` 对象中删除 `value `这个元素, 之后 `WeakSet.prototype.has(value)` 方法便会返回 `false`.

- [`WeakSet.prototype.has(value)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WeakSet/has)

  返回一个布尔值,  表示给定的值 `value` 是否存在于这个 `WeakSet` 中.









