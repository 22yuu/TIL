자바스크립트에서 sort()는 문자열 순서로 정렬한다.

문자 순서가 아닌 숫자로 정렬하려면 `compareFuntion`을 제공해야된다.

```javscript
const array = [4,5,3,2,1];

// 오름차순 정렬
array.sort((a,b) => {
    return a - b;
});

// 내림차순 정렬
array.sort((a,b) => {
    return b - a;
});
```

객체 정렬하는 방법

```javascript
var items = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic', value: 13 },
  { name: 'Zeros', value: 37 },
];

// value 기준으로 정렬
items.sort(function (a, b) {
  if (a.value > b.value) {
    return 1;
  }
  if (a.value < b.value) {
    return -1;
  }
  // a must be equal to b
  return 0;
});

// name 기준으로 정렬
items.sort(function (a, b) {
  var nameA = a.name.toUpperCase(); // ignore upper and lowercase
  var nameB = b.name.toUpperCase(); // ignore upper and lowercase
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }

  // 이름이 같을 경우
  return 0;
});
```

[MDN - sort()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
