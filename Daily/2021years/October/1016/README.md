# this value 는 어떻게 ??

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다. this의 값은 함수를 호출한 방식에 의해 동적으로 결정된다. 디스를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메소드를 참조 할 수 있습니다.

일반함수 호출시 this는 전역객체에 메서드를 호출시 호출한 객체에 바인딩되며 생성자 함수로 호출시 생성자 함수가 생성할 객체(인스턴스)에 바인딩 되며 call,apply,bind 메소드 사용시 메소드에 첫번째 인수로 전달하는 객체에 바인딩 된다.

실행중에는 할당할 수 없고 ES5에서 bind메서드를 통해 값을 설정할 수 있고 SE2015에서는 스스로의 바인딩을 제공하지 않는 화살표 함수를 추가하였다.(렉시컬 컨텍스트안의 this값을 유지한다)
