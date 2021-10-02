#Prototype

원시타입

6개.. 원래는 5개엿음 symbol이 생기게 된 이유?

boolean string number undefined null symbol

symbol

래퍼런스 타입 배열 key가 INDEX인 순회가능 SYMBOL

자바스크립트 객체는 `Prototype`이라는 내부 프로퍼티가 존재한다. 거의 모든 객체가 생성 시점에 이 프로퍼티에 null이 아닌 값이 할당된다.

우선 너무나도 자연스러운 이 코드를 살펴보자.

```
    const woody = {
    	riding:true
    }

    woody.riding // true
```

`woody.riding` 처럼 객체 프로퍼티를 참조할 경우 [[Get]]이 호출되어 객체 내부에 해당 프로퍼티가 존재하는지 탐색한다. 그렇다면 객체 내부에 없는 프로퍼티를 호출하게 되면 어떻게 될까??

[[Get]]은 객체 내부에서 해당 프로퍼티를 찾지 못하면 바로 [[Prototype]]링크를 따라가 프로퍼티를 탐색한다. 모든 일반 객체의 최상위 프로토타입 연쇄는 내장 `Object.prototype`이고 이 지점에서도 찾지 못하면 탐색이 종료된다. (undefined 반환)

```
    const buzz = {
    flying:true
    }

    const woody = Object.create(buzz);
    // 우디가 날 수 있게 되었다!
    woody.flying; // true
```

woody는 buzz와 [[Prototype]]이 링크되었다. woody내부에는 flying이라는 프로퍼티가 없지만 연결된 buzz에서 해당 프로퍼티를 찾아 그 값을 반환한 것이다.

![https://media.vlpt.us/post-images/adam2/f3cfee50-fd8c-11e9-9881-1f0bd327923e/Untitled-d97e46ed-9a42-48ed-8157-084269d64d5c.png](https://media.vlpt.us/post-images/adam2/f3cfee50-fd8c-11e9-9881-1f0bd327923e/Untitled-d97e46ed-9a42-48ed-8157-084269d64d5c.png)

`for...in`루프에서도 객체를 순회할 때 prototype 연결을 통해 탐색 가능한 프로퍼티라면 모두 열거한다.

```
    for(let i in woody){
    	console.log(`${i}를 발견`)
    }
    // flying를 발견
```
