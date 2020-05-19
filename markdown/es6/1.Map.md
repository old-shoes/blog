**`Map`** 对象保存键值对，并且能够记住键的原始插入顺序。任何值(对象或者[原始值](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)) 都可以作为一个键或一个值。

拓展：[迭代协议](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols)

> Map对象间可以进行合并，但是会保持键的唯一性。
>
> 请注意！为Map设置对象属性也是可以的，但是可能引起大量的混乱

#### `new Map([iterable])`

参数：

> `iterable`可以是一个数组或其他的`iterable`对象，其元素为键值对（两个元素的数组，例如：[[1,'one'],[2,'two']]）。每个键值对都会添加到新的Map。null会被当作undefined。

[sameValueZero]([https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness#%E9%9B%B6%E5%80%BC%E7%9B%B8%E7%AD%89](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness#零值相等))

**Objects和maps的区别**

* 一个`Object`的键只能是[`字符串`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)或者 [`Symbols`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)，但一个 `Map` 的键可以是**任意值**，包括函数、对象、基本类型。
* Map 中的键值是有序的，而添加到对象中的键则不是。因此，当对它进行遍历时，Map 对象是按插入的顺序返回键值。

- 你可以通过 `size` 属性直接获取一个 `Map` 的键值对个数，而 `Object` 的键值对个数只能手动计算。
- `Map` 可直接进行迭代，而 `Object` 的迭代需要先获取它的键数组，然后再进行迭代。
- `Object` 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。

这三条提示可以帮你决定用`Map`还是`Object`：

- 如果键在运行时才能知道，或者所有的键类型相同，所有的值类型相同，那就使用`Map`。
- 如果需要将原始值存储为键，则使用`Map`，因为`Object`将每个键视为字符串，不管它是一个数字值、布尔值还是任何其他原始值。
- 如果需要对个别元素进行操作，使用`Object`。

API:

属性：

**`Map.prototype.size`**
 计算一个`Map`中的条目数量

**`get Map[@@species]`**
本构造函数用于创建派生对象

```javascript
Map[Symbol.species]; // function Map()
class MyMap extends Map {
  // 重写覆盖 MyMap species to the parent Map constructor
  static get [Symbol.species]() { return Map; }
}
```



方法：

**`Map.prototype.clear()`**
移除Map对象的所有键值对

**`Map.peototype.delete(key)`**
如果`Map`对象中存在该元素，则一处它并返回`true`；否则如果该元素不存在则返回`false`。随后调用`Map.prototype.has(key)`将返回`false`

**`Map.prototy.entries()`**
返回一个新的`Iterator`对象，他按插在顺序包含了Map对象中每个元素的`[key,value]`数组

```javascript
var myMap = new Map();
myMap.set("0", "foo");
myMap.set(1, "bar");
myMap.set({}, "baz");

var mapIter = myMap.entries();

console.log(mapIter.next().value); // ["0", "foo"]
console.log(mapIter.next().value); // [1, "bar"]
console.log(mapIter.next().value); // [Object, "baz"]
```



**`Map.prototype.forEach(callbackFn[,this.Arg])`**
按插入顺序，为Map对象里的每一键值对调用一次callbackFn函数。如果为forEach提供了thisArg，它将在每次回调中作为this值

```javascript
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
})
```



**`Map.prototype.get(key)`**
返回键对应的值，如果不存在，则返回undefined

**`Map.prototype.has(key)`**
返回一个布尔值，表示Map实例是否包含键对应的值

**`Map.prototype.keys()`**
返回一个新的`Iterator`对象，它按插入顺序包含了Map对象汇总每个元素的**键**

**`Map.prototype.set(key,value)`**
设置Map对象中键的值。返回该Map对象

**`Map.prototype.values()`**
返回一个新的`Iterator`对象，它按插入顺序包含了Map对象中每个元素的**值**。

**`Map.prototype[@@iterator]()`**
返回一个新的`Iterator` 对象，

```javascript
const map1 = new Map();

map1.set('0', 'foo');
map1.set(1, 'bar');

const iterator1 = map1[Symbol.iterator]();
```



**使用for..of方法迭代Map**

```javascript
let myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
for (let [key, value] of myMap) {
  console.log(key + " = " + value);
}
// 将会显示两个log。一个是"0 = zero"另一个是"1 = one"

for (let key of myMap.keys()) {
  console.log(key);
}
// 将会显示两个log。 一个是 "0" 另一个是 "1"

for (let value of myMap.values()) {
  console.log(value);
}
// 将会显示两个log。 一个是 "zero" 另一个是 "one"

for (let [key, value] of myMap.entries()) {
  console.log(key + " = " + value);
}
// 将会显示两个log。 一个是 "0 = zero" 另一个是 "1 = one"
```





