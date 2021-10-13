# 클래스 함수

```
    function Foo(){

    }
```

함수를 정의하면 함수만 생성되는 것이 아니라 `Prototype Object`도 같이 생성이 된다.

![https://media.vlpt.us/post-images/adam2/970d2010-32e9-11ea-8e4f-dda7a26d676e/image.png](https://media.vlpt.us/post-images/adam2/970d2010-32e9-11ea-8e4f-dda7a26d676e/image.png)

Prototype Object는 기본속성으로 `constructor`와 `__proto__`를 가지고 있다. (따라서 정확히 말하자면 Foo.prototype 객체가 프로토타입을 의미하는것은 아니다. constructor도 가지고 있으니! )

- **constructor**는 내가 선언한 생성자 함수(Foo)를 가리킨다. new 키워드와 함께 함수를 호출할 경우 constructor함수를 실행하고 부수효과로 객체가 생성된다._생성자 함수가 아니라 **함수를 생성하는 호출**이라고 생각하는것이 맞다_
- **prototype**은 생성자 함수에 정의한 모든 객체가 공유할 **원형**이다.
- **proto**는 [[Prototype]]링크이다. 생성자 함수에 정의해두었던 prototype을 참조한다.

```
const f = new Foo();
Object.getPrototypeOf(f) === Foo.prototype; // true
```

![https://media.vlpt.us/post-images/adam2/11724c50-32ee-11ea-9de7-5b60278cfbd1/image.png](https://media.vlpt.us/post-images/adam2/11724c50-32ee-11ea-9de7-5b60278cfbd1/image.png)

![https://media.vlpt.us/post-images/adam2/fb66d520-fd8c-11e9-9881-1f0bd327923e/Untitled-f837623b-c1d2-4ff0-ab2b-1fba6dd88352.png](https://media.vlpt.us/post-images/adam2/fb66d520-fd8c-11e9-9881-1f0bd327923e/Untitled-f837623b-c1d2-4ff0-ab2b-1fba6dd88352.png)

![https://media.vlpt.us/post-images/adam2/59f64b20-32ee-11ea-9de7-5b60278cfbd1/image.png](https://media.vlpt.us/post-images/adam2/59f64b20-32ee-11ea-9de7-5b60278cfbd1/image.png)

`prototype`은 생성자 함수에 사용자가 직접 넣는 거고, `__proto__` 는 new를 호출할 때 prototype을 참조하여 자동으로 만들어진다.생성자 함수에는 `prototype`에, 생성자로부터 만들어진 객체에는 `__proto__`에 생성자의 prototype이 들어간다.

`new` Foo()로써 만들어진 모든 객체(`f`)는 결국 **Foo.prototype 객체**와 내부적으로 **[[Prototype]]링크**로 연결된다.**결국 `f` 와 `Foo` 는 상호 연결된 두개의 객체가 된다.**

![https://media.vlpt.us/post-images/adam2/00bec870-fd8d-11e9-9881-1f0bd327923e/Untitled-2a35c021-b5ac-44aa-8880-43a0eb1f5480.png](https://media.vlpt.us/post-images/adam2/00bec870-fd8d-11e9-9881-1f0bd327923e/Untitled-2a35c021-b5ac-44aa-8880-43a0eb1f5480.png)

### new 연산자

객체지향언어에서 클래스를 인스턴스화 하기 위해 `new 연산자`를 사용한다. 그리고 자바스크립트에서도 두개의 객체를 연결하기 위해 new연산자를 사용한다.

하지만 전자의 경우 클래스로부터 작동을 **복사**하여 새로운 객체를 만드는 것이고, 후자의 경우 복사 과정 없이 **그저 두 객체를 연결**한 것이 전부이다.따라서 자바스크립트의 new 키워드는 우리가 흔히 아는 new키워드와 다르게 동작한다는걸 알 수 있다.

js에서 new연산자는 결국 **새 객체를 다른 객체와 연결하기 위한 간접적인 우회 방법**이고, `Object.create()`를 이용해 직접적으로 객체를 연결해주는 방법도 있다.

> [[Prototype]] 체계를 흔히들 프로퍼타입 상속이라고 부른다. 하지만 상속은 기본적으로 복사를 수반하지만, 자바스크립트는 객체 프로퍼티를 복사하지 않는다. 따라서 프로퍼타입 상속은 의미를 더 햇갈리게 만드는 단어의 조합이고, `위임이야말로` 자바스크립트 객체-연결 체계를 훨씬 더 정확하게 나타내는 용어라고 할 수 있다.

### 생성자

앞 예제에서 new를 붙여 Foo함수를 호출하여 객체가 "생성"되는 현장을 목격했으니 Foo를 생성자라고 믿고 싶은 욕망을 버리기란 쉽지 않다.

하지만 Foo는 생성자가 아니다. 그저 **함수**일 뿐이다.

함수는 결코 생성자가 아니지만 new를 붙여 호출하는 순간 이 함수는 `생성자 호출`을 한다. `new키워드`는 일반 함수 호출 도중에 원래 수행할 작업 외에 `객체 생성`이라는 잔업을 더 부과하는 지시자인 것이다.

```
    function nothing(){
    	console.log(`그저 함수입니다`)
    }

    const a = new nothing();
    // "그저 함수입니다"
    a;  // {}
```

![https://media.vlpt.us/post-images/adam2/c6b44690-32ee-11ea-9de7-5b60278cfbd1/image.png](https://media.vlpt.us/post-images/adam2/c6b44690-32ee-11ea-9de7-5b60278cfbd1/image.png)

평범한 함수인 nothing을 new로 호출함으로써 **_객체가 생성_** 되고 부수효과로 생성된 그 객체를 a에 할당하는 것이다. 이것을 보통 생성자(constructor) 호출 이라고 부르지만 nothing함수 자체는 생성자가 아니다.

즉, 자바스크립트는 앞에 new를 붙여 호출한 함수를 모두 **생성자**라고 할 수 있다. 함수는 결코 생성자가 아니지만 new를 사용하여 호출할 때에만 **생성자 호출**이다.

### 그렇다면 객체를 객체와 연결해야 하는 이유는 뭘까? 그렇게 함으로써 어떤 장점이 있는걸까?

```
// this를 사용
function Toy(name){
	this.name = name;
  this.battery = 100;
  this.charge = function(){
  	battery += 10;
    console.log(`charging is finished. battery is ${this.battery}`)
  }
}

const woody = new Toy('woody');
const buzz = new Toy('buzz');
```

![https://media.vlpt.us/post-images/adam2/d67d0690-32ec-11ea-8e4f-dda7a26d676e/image.png](https://media.vlpt.us/post-images/adam2/d67d0690-32ec-11ea-8e4f-dda7a26d676e/image.png)

```
// prototype 사용
function Toy(name){
  this.name = name;
  this.battery = 100;
}
Toy.prototype.charge = function(){
  	this.battery += 10;
    console.log(`charging is finished. battery is ${this.battery}`)
  }

const woody = new Toy('woody');
const buzz = new Toy('buzz');
```

![https://media.vlpt.us/post-images/adam2/5e72ef10-32ed-11ea-b8fa-133bed040259/image.png](https://media.vlpt.us/post-images/adam2/5e72ef10-32ed-11ea-b8fa-133bed040259/image.png)

prototype은 모든 객체가 `공유`하고 있어서 `한 번`만 만들어지지만, this에 넣은 것은 객체 하나를 만들 때마다 메소드도 하나씩 만들어지기 때문에 **불필요한 메모리 낭비**가 발생한다.

# 정리

---

객체에 존재하지 않는 프로퍼티를 접근하려 시도하면 해당 객체의 내부 [[Prototype]] 링크를 따라 다음 수색 장소를 결정한다. 모든 일반 객체의 최상위 프로토타입 연쇄는 내장 `Object.prototype`이고 이 지점에서도 찾지 못하면 탐색이 종료된다.

두 객체를 서로 연결짓는 가장 일반적인 방법은 함수 호출 시 `new`키워드를 앞에 붙이는 것이다.new키워드는 `일반 함수 호출 + "객체" 생성`이라는 잔업을 더 부과하는 지시자이다.`const f = new Foo()`를 실행하면 Foo 함수가 실행되고, 객체가 생성되어 변수 f에 할당된다.

```
typeof f // object
typeof Foo //function
```

- **constructor**는 내가 선언한 생성자 함수(Foo)를 가리킨다. new 키워드와 함께 함수를 호출할 경우 constructor함수를 실행하고 부수효과로 객체가 생성된다._생성자 함수가 아니라 **함수를 생성하는 호출**이라고 생각하는것이 맞다_
- **prototype**은 생성자 함수에 정의한 모든 객체가 공유할 **원형**이다.
- **proto**는 [[Prototype]]링크이다. 생성자 함수에 정의해두었던 prototype을 참조한다.

[https://velog.io/@adam2/자바스크립트-Prototype-완벽-정리](https://velog.io/@adam2/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Prototype-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)
