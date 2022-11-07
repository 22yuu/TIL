## Number.isNaN() vs isNaN()

JavaScript에서는 `NaN`을 판별하기 위해 `Number.isNaN(value)`과 `isNaN(value)` 함수가 있다. 두 함수 중 어떤 함수를 사용해야 좋을지 고민이 되어 정리해보았다.
위의 두 함수는 주어진 값 `value`가 `NaN`이면 `true`아니면 `false`를 반환하는 함수이다. `isNaN()` 함수는 왜 필요한 것일까? JavaScript에서는 다른 모든 값과 달리, `NaN`은 같음 연산(`==`, `===`)을 판별할 수 없다고 한다. 즉, `NaN == NaN`, `NaN === NaN`은 `false`가 반환되기 때문이다. 그래서 `NaN`을 판별하는 함수가 필요하다.

하지만 `isNaN()`의 경우 주어진 인자가 `Number`형이 아닌 경우 그 값을 먼저 숫자로 변환 후 함수가 수행된다. 따라서 숫자 형으로 변형된 결과가 NaN이 아닌 값(undefined, {}, "123")으로 변형이 되어 `false`가 반환될 수 있기 때문이다. 따라서 `isNaN()`함수의 경우 몇몇 혼란스러운 상황들이 있으므로 ES6(ECMAScript 2015)에서 추가된 Number.isNaN()으로 바꾸는 편이 좋다.

```javascript
console.log(Number.isNaN(undefined)); // false 
console.log(isNaN(undefined)); // true

console.log(Number.isNaN("NaN")); // false 
console.log(isNaN("NaN")); // true

console.log(Number.isNaN({})); // false 
console.log(isNaN({})); // true

console.log(Number.isNaN("123ABC")); // false 
console.log(isNaN("123ABC")); // true -> 숫자로 변형이 되어 뒤에 문자 ABC가 사라지고 123만 남음
```




