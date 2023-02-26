[참고 링크](https://springisover.tistory.com/14)

### WPF x:Name vs Name

WPF Control Property를 보면 x:Name, Name으로 해당 컨트롤의 이름을 명시해줄 수 있다.

결론을 먼저 말하자면 두 Property 모두 똑같은 기능으로 동작하며 아무거나 사용해도 상관없다.

Xaml 코드 상에서 뿐만 아니라 Runtime에도 계속 보존되어야 할 Property가 필요했던 것.

단순히 요소의 이름을 붙여주는 것과 동시에 핵심 기능은 behind code에서 해당 요소를 참조할 수 있는 Field를 만들어주는 것이다.

Name 속성과 x:Name 속성 모두 behind code에서 Binding이 잘된다. WPF 프레임워크 자체가 Name과 x:Name을 하나로 매핑 시켜주어서 어떤 것을 사용해도 본래의 기능을 수행할 수 있도록 해준다고 한다.

`Name`값은 `Unique`한 값으로
