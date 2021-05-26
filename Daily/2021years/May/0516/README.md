### **문제 설명**

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.

### 제한 사항

- `s`는 길이 1 이상, 길이 8 이하인 문자열입니다.

(s.length === 4 || s.length === 6)  ⇒ [4,6].includes(s.length)

```jsx
function solution(s) {
  return /^[0-9]+$/.test(s) && [4,6].includes(s.length);
}
```

```jsx
function alpha_string46(s){
  var regex = /^\d{6}$|^\d{4}$/;
  return regex.test(s);
}
```

```jsx
function alpha_string46(s){
  var result = false;
  if((s.length == 4 || s.length == 6) && /^[0-9]+$/.test(s)) {
    result = true;
  }

  return result;
}
```

참고 : [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
