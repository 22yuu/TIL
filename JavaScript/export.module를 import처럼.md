## export.module를 import처럼

평소 es6 문법을 주로 사용해 모듈을 사용할 때도 import 구문을 이용해 코드를 작성했었다.

그러다 commonJS를 이용해 코드를 작성하고 있는데, import로 class 객체를 불러왔을 땐 내부 메서드 접근이 가능했던 것이 commonJS로 불러왔을 땐 접근이 안됐었다.

```javascript
// -- Calculator.js --

class Calculator {

    add(a, b) {
        return a + b;
    }

    substract(a, b) {
        return a - b;
    }
}

export.modules = Calculator;
```

이렇게 `export.modules = Calculator;`를 사용해서 내보내면

```javascript
const Calculator = require('./Calculator');

class App {
    constructor() {
        this.calc = new Calculator();

        this.calc.add(1, 2);
    }
}
```

이처럼 생성자에 new 키워드를 이용해서 객체를 할당한 후 선언해야 한다. commonJS에서 import처럼 하면 체이닝을 통해서 바로 함수에 접근할 수 있게 구현하고 싶다면 export할 때 new 키워드를 사용하면 된다.

```javascript
// -- Calculator.js --

class Calculator {

    add(a, b) {
        return a + b;
    }

    substract(a, b) {
        return a - b;
    }
}

export.modules = new Calculator();

// -----------------
// -- App.js --

const Calculator = require('./Calculator');

class App {
    constructor() {
        Calculator.add(1, 2);
    }
}
```