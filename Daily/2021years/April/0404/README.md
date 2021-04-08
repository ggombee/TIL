# React.ReactElement | null

## 에러
보통 컴포넌트를 만들때 React.ReactElement를 써서 만들었는데,

```java
function Components(): React.ReactElement {
	return(<></>)  
}
```

Switch case 문을 작성할때 default type으로 null을 리턴할때

아래의 에러가 났다..

> TS2322: Type 'null' is not assignable to type 'ReactElement<any, string | ((props: any) => ReactElement<any, string | ... | (new (props: any) => Component<any, any, any>)> | null) | (new (props: any) => Component<any, any, any>)>'.

![Untitled (6)](https://user-images.githubusercontent.com/58289110/113976586-4d966280-987c-11eb-940b-bf1628ef4a37.png)

검색을 해보니 Typescript 환경에서의 function 함수와 class 함수의 리턴타입과 관련이 있었다.

아래 링크를 참고하면 이해가 쉽다.

[https://stackoverflow.com/questions/58123398/when-to-use-jsx-element-vs-reactnode-vs-reactelement](https://stackoverflow.com/questions/58123398/when-to-use-jsx-element-vs-reactnode-vs-reactelement)

결론적으로 React.ReactElement 뒤에 | null 타입을 같이 지정해주면 해결된다.

```java
function Components(): React.ReactElement | null  {
  switch () {
    case '01':
      return (
        <div >
	         hh
        </div>
      );
    case '02':
      return (
        <div >
			     sss
        </div>
      );
    default:
      return null;
  }
}
```

```java
function Components(): React.ReactElement  {
  switch () {
    case '01':
      return (
        <div >
	         hh
        </div>
      );
    case '02':
      return (
        <div >
			     sss
        </div>
      );
    default:
      return <>{null}</>;
  }
}
```

이렇게 사용해도 무방하나.. fragment 가 불필요한 작업을 한번 더 하게 될 수있다.
