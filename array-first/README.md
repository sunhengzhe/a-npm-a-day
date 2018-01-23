# array-first

## github

[https://github.com/jonschlinkert/array-first](https://github.com/jonschlinkert/array-first)

## Usage

```javascript
var first = require('array-first');

first(['a', 'b', 'c', 'd', 'e', 'f']);
//=> 'a'

first(['a', 'b', 'c', 'd', 'e', 'f'], 1);
//=> 'a'

first(['a', 'b', 'c', 'd', 'e', 'f'], 3);
//=> ['a', 'b', 'c']
```

## 看源码之前的实现版本

```javascript
exports = module.exports = function(arr, size = 1) {
    if (!Array.isArray(arr)) {
        throw new Error('the first argument must be an array');
    }

    if (arr.length === 0) {
        return null;
    }

    let formatedSize = parseInt(size, 10) || 1;

    if (formatedSize === 1) {
        return arr[0];
    }

    return arr.slice(0, formatedSize);
}
```

## 源码

```javascript
var isNumber = require('is-number');
var slice = require('array-slice');

module.exports = function arrayFirst(arr, num) {
  if (!Array.isArray(arr)) {
    throw new Error('array-first expects an array as the first argument.');
  }

  if (arr.length === 0) {
    return null;
  }

  var first = slice(arr, 0, isNumber(num) ? +num : 1);
  if (+num === 1 || num == null) {
    return first[0];
  }
  return first;
};
```

源码还引用到了其他的两个包，`is-number` 和 `array-slice`，不过大致思路是一样的，使用了 Array 的 slice 方法。

那为什么不用原生的 slice？为了兼容 IE9 以下。