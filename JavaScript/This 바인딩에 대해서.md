### This binding!

  자바스크립트에서 기본적으로 `this` 객체는 window 전역 객체를 가리키고 있다. 하지만 클래스를 내부에서 사용할 경우 해당 클래스를 가르키게 된다. 클래스 내부에서 `this` 객체를 사용할 때 주의할 점이 있는데 바로 이벤트를 핸들링할 때이다. 특정 요소에 이벤트 리스너를 등록하면 `자신을 감싸고 있는 클래스 객체가 아닌 자신을 호출한 요소`를 가리킨다.

```jsx
class Test {
	constructor() {
		this.box = document.querySelector('.box');
		box.addEventListener('click', this.onClick);
	}
	
	onClick() {
		console.log(this); // output : <div class='box'></div>
	}
}
```

그렇다면 `자신을 호출한 요소`를 가리킨다는 것이 어떤 점이 잘못된 것일까? 만약 위의 코드 스니펫에서 같은 클래스 내부에 있는 다른 메서드를 호출하는 경우 에러가 발생할 수 있다! 아래의 코드 스니펫을 보자

```jsx
class Test {
	constructor() {
		this.box = document.querySelector('.box');
		box.addEventListener('click', this.onClick);
	}
	
	onClick() {
		console.log(this); // output : <div class='box'></div>
		this.print();
	}
	
	print() {
		console.log('class!!!');
	}
}
```

`box`요소를 클릭했을 때 onClick 메서드가 수행되고 onClick 메서드 안에 print 메서드도 수행되어야 한다. 하지만 이 때 `this` 객체가 가리키는 것이 class 객체가 아닌 자신을 호출한 요소를 가리키고 있다면 print 메서드를 찾을 수 없기 때문에 에러가 발생한다.

이러한 문제점 때문에 클래스 내부에서 `this`를 사용할 경우 주의가 필요하다는 것이다. 그러면 클래스 내부에서 `this`를 어떻게 사용해야할까?

바로 `this`가 가르키는 객체를 클래스 객체로 고정시켜주면 된다. `this`를 클래스 객체로 고정시키는 방법에는 여러가지가 있다. 아래의 코드 스니펫을 참고해보자.

```jsx
class Test {
	constructor() {
		this.box = document.querySelector('.box');
		this.box.addEventListener('click', this.onClick); // this가 box를 가리키고 있으므로 print()를 찾을 수 없는 에러가 발생!
		
		// this 객체를 클래스 객체로 고정시키는 방법
		// 1. bind()를 사용
		this.onClick = onClick.bind(this);
		this.box.addEventListener('click', this.onClick);
		
		this.box.addEventListener('click', this.onClick.bind(this)); // 똑같은 방법이니 편한 방법을 사용
		
		// 2. 화살표 함수를 사용
		this.box.addEventListener('click', () => this.onClick);

		// 3. onClick 함수를 변수로 선언
		this.box.addEvenetListener('click', this.onClick2);
	}
	
	onClick() {
		console.log(this); // output : <div class='box'></div>
		this.print();
	}

	onClick2 = (event) => {
		console.log(this); // output : <div class='box'></div>
		this.print();
	}
	
	print() {
		console.log('class!!!');
	}
}
```

[참고 사이트]

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)