# redux

상태관리 라이브러리, 스토어라는 데이터 공간이 존재한다.

액션은 스토어에 운반할 데이터를 말한다.

리듀서는 액션이 운반될 곳이다 액션은 리듀서를 거쳐 리듀서가 주문을 보고 스토어의 상태를 업데이트한다. 액션을 리듀서에 전달하기 위해서는 디스패치 메소드를 사용해야한다.