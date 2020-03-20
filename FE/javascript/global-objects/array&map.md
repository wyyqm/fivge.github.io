### Array

#### 数组遍历

##### for(;;)

遍历数组推荐使用

```js
for (let i = 0, len = arr.length; i < len; i++) {}
```

##### for of

##### for in

遍历数组或对象不要使用 `for in`

遍历 Map 使用 `for in` 加模式匹配

#### 数组方法 prototype

<https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array#>

##### map()

map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```js
let arr = ["1", "2", "3", "4"];
let arr2 = arr.map(x => parseInt(x) + 1);
```

```js
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
 // Return element for new_array
}[, thisArg])
```

- 当你不打算使用返回的新数组却使用 map 是违背设计初衷的
- callback 函数会被自动传入三个参数：数组元素，元素索引，原数组本身
- map 不修改调用它的原数组本身

---

<https://es6.ruanyifeng.com/#docs/array>