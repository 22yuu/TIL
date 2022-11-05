### Builder Pattern

Builder Pattern이란 Builder라는 이름처럼 객체를 생성하는 것에 관한 디자인 패턴의 종류이다.

객체를 만들어서 사용하다보면 간혹 객체의 생성자가 길어지거나 복잡해지는 경우가 있다. 이런 경우 빌더 패턴으로 객체의 생성 과정을 분리해 순차적이고 직관적인 코드로 만든다. 또한 구현 로직을 숨기고 싶거나 특정 객체를 보호할 수 있게끔 보안 측면에서도 유용하게 사용가능하다.

```jsx
// Builder Pattern
export default class GameBuilder {
/**
* GameBuilder 클래스를 따로 만드는 이유는?
* 1. Game 생성자의 매개변수가 3개 이상이면 생성자가 길어지거나 복잡해져 개발자 실수가 나올 수 있음
* 2. Game이 생성되는 과정을 숨길려고 (보안)
* 3. Builder Pattern은 체인닝을 이용해 간단 명료하게 코드 작성 가능(가독성)
*/

gameDuration(duration) {
    this.gameDuration = duration;
    return this;
    // array 배열에서 map이나 reduce를 쓰면 array를 그대로 리턴해 메소드를 체인닝처럼 사용할 수 있듯이 class 자체를 리턴해서 체인닝을 사용할 수 있다.
    // 메소드 체인닝을 위해서 class 자체를 리턴하는 것!
}

carrotCount(num) {
    this.carrotCount = num;
    return this;
}

bugCount(num) {
    this.bugCount = num;
    return this;
}

build() {
    return new Game(this.gameDuration, this.carrotCount, this.bugCount);
}
}

class Game {...}
```

위의 코드 스니펫처럼 구현된 Builder Pattern을 가지고 메인(main.js, index.js, app.js 등)에서 불러와 사용한다. 또한 Builder를 선언할 때 체인닝을 통해서 가독성을 높일 수 있다.

```jsx
import GameBuilder from "./game.js";

    const game = new GameBuilder()
      .gameDuration(5)
      .carrotCount(3)
      .bugCount(3)
      .build();
    
    /* 기존 코드
    import Game from "./game.js";
    
    const GAME_DURATION = 5;
    const CARROT_COUNT = 3;
    const BUG_COUNT = 3;
    
    const game = new Game(GAME_DURATION, CARROT_COUNT, BUG_COUNT);
    */
```
    
주석처리가 된 것이 기존 코드이다. 어떤 것이 더 가독성이 좋은가? 개인적으로 가독성보다는 Game의 로직을 숨기고 외부로부터 코드를 보호할 수 있는 보안적인 측면과 개발자가 생성자로 매개변수의 값을 넘겨줄 때 순서에 맞게 넘겨주지 않으면 예기치 못한 에러가 발생할 수 있는데 체인닝으로 메서드를 불러와 메서드 명으로 직관적으로 구분할 수 있도록 해 사소한 개발자의 실수를 줄일 수 있다는 점에서 유용하다고 생각한다.

[참고 사이트]

[https://ttum.tistory.com/35](https://ttum.tistory.com/35)