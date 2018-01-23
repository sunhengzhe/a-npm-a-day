# utils-merge

## github

[https://github.com/jaredhanson/utils-merge](https://github.com/jaredhanson/utils-merge)

## Usage

```javascript
var a = { foo: 'bar' }
  , b = { bar: 'baz' };

merge(a, b);
// => { foo: 'bar', bar: 'baz' }
```

## 看源码之前的实现

```javascript
exports = module.exports = (a, b) => ({ ...a, ...b });
```

## 源码

```javascript
exports = module.exports = function(a, b){
  if (a && b) {
    for (var key in b) {
      a[key] = b[key];
    }
  }
  return a;
};
```

实际上原模块是把合并后的对象整合在了第一个参数上，和我的实现是不一样的。因为 Javascript 是按值传递，a 只是实参的引用值，改变引用就用实参没有关系了。