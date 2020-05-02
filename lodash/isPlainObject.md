```js
function getTag(value) {
  if (value == null) {
    return value === undefined ? "[object Undefined]" : "[object Null]";
  }
  return Object.prototype.toString.call(value);
}

function isObjectLike(value) {
  return typeof value === "object" && value !== null;
}

function isPlainObject(value) {
  if (!isObjectLike(value) || getTag(value) != "[object Object]") {
    return false;
  }
  if (Object.getPrototypeOf(value) === null) {
    return true;
  }
  let proto = value;
  while (Object.getPrototypeOf(proto) !== null) {
    proto = Object.getPrototypeOf(proto);
  }
  return Object.getPrototypeOf(value) === proto;
}

export default isPlainObject;
```

- getTag
  <br>
  里面的判断猜测是为了兼容，因为 Object.prototype.toString.call(undefined)和 Object.prototype.toString.call(null)在最新的 chrome 中依然能够返回预期的值
  <br>
- isObjectLike
  <br>
  使用 typeof 判断是否是引用类型，只需排除 null 即可。局限是无法排除数组、正则、Date 、Function 等，因为这些也属于引用类型
  <br>
- 结合 typeof 和 Object.prototype.toString 可判断是否是（狭义）对象
  <br>

  - typeof 缩小范围到引用类型
  - Object.prototype.toString 缩小到对象类型

  <br>

- Object.getPrototypeOf(value) === null
  <br>
  这是一种捷径，如果原型是 null，直接返回 true。例如判断 Object.create(null)
  <br>
- while 循环
  <br>
  使用 Object.create()创建的需要遍历才能判断，例如 Object.create([1,2,3])单靠上面的无法判断
