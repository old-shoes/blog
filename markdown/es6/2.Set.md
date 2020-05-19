**`Set`** 对象允许你存储任何类型的唯一值，无论是[原始值](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)或者是对象引用。

Eg:

```javascript
const set1 = new Set([1,2,3,4,5,6])
console.log(set1.has(1));//true
set1.add(7)//在set对象尾部田间一个元素
set1.size  //返回set对象的值的个数
set1.delete(1)//移除set的中与这个值相等的元素
set1.entries() //返回一个迭代器 entries.next()
set1.forEach(function (aa){
  console.log(aa)  //打印：1，2，3，4，5，6
})
set1.has(1)//返回一个布尔值，表示该值在set中存在与否
set1.keys()//返回一个新的迭代器对象，该对象包含set对象中按插入顺序排列的所有元素的值
set1.value()//跟keys()方法相同
Set.[@@iterator]()//返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。

```

set的实际应用

数组去重：

```javascript
var arr=[1,2,1,2,1,2,1,2,2,3,4,4,5,5,6,6]
arr=[...new Set(arr)]
```



















