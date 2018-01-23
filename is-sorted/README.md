# is-sorted

## github

[https://github.com/dcousens/is-sorted](https://github.com/dcousens/is-sorted)

## Usage

```javascript
var sorted = require('is-sorted')

console.log(sorted([1, 2, 3]))
// => true

console.log(sorted([3, 1, 2]))
// => false

// supports custom comparators
console.log(sorted([3, 2, 1], function (a, b) { return b - a })
// => true
```

## 看源码之前的实现

```javascript
module.exports = function (arr, func = (a, b) => a - b) {
    for (let i = 1; i < arr.length; i++) {
        if (func(arr[i - 1], arr[i]) > 0) {
            return false;
        }
    }
    return true;
}
```

## 源码

```javascript
function defaultComparator (a, b) {
  return a - b
}

module.exports = function checksort (array, comparator) {
  comparator = comparator || defaultComparator

  for (var i = 1, length = array.length; i < length; ++i) {
    if (comparator(array[i - 1], array[i]) > 0) return false
  }

  return true
}
```

基本差不多，数组的排序其实要注意的就是 `sort` 默认是按字符串排序的

```javascript
const arr = [1, 3, 14, 2];
arr.sort();
// => [1, 14, 2, 3]
```
