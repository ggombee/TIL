# prototype object

함수를 정의하면 함수만 생성되는 것이 아니라 `Prototype Object`도 같이 생성이 된다.

![https://media.vlpt.us/post-images/adam2/970d2010-32e9-11ea-8e4f-dda7a26d676e/image.png](https://media.vlpt.us/post-images/adam2/970d2010-32e9-11ea-8e4f-dda7a26d676e/image.png)

Prototype Object는 기본속성으로 `constructor`와 `__proto__`를 가지고 있다. (따라서 정확히 말하자면 Foo.prototype 객체가 프로토타입을 의미하는것은 아니다. constructor도 가지고 있으니! )

- **constructor**는 내가 선언한 생성자 함수(Foo)를 가리킨다. new 키워드와 함께 함수를 호출할 경우 constructor함수를 실행하고 부수효과로 객체가 생성된다._생성자 함수가 아니라 **함수를 생성하는 호출**이라고 생각하는것이 맞다_
- **prototype**은 생성자 함수에 정의한 모든 객체가 공유할 **원형**이다.
- **proto**는 [[Prototype]]링크이다. 생성자 함수에 정의해두었던 prototype을 참조한다.

프로토타입은 (constructor)생성자 함수에 사용사자 직접 넣는 거고, **proto**는 new를 호출할때 프로토타입을 참조하여 자동으로 만들어진다. 생성자 함수에는 프로토타입에 생성자로부터 만들어진 객체에는 **proto**에 생성자의 프로토타입이 들어간다.

프로토타입체계를 흔히 프로토타입 상속이라고 부른다. 하지만 상속은 기본적으로 복사를 수반하지만, 자바스크립에서의 상속은 객체-연결체계를 더 정확하게 나타내면 위임이라고 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10736acd-72ed-45a6-a1eb-9004a6f0dd3b/Untitled.png)
