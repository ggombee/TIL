# [코테_JS] 가운데 글자 가져오기(ceil, substr)

### **문제 설명**

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

### 제한사항

- s는 길이가 1 이상, 100이하인 스트링입니다.

### solution.js

```jsx
function solution(s) {
    return s.substr(Math.ceil(s.length / 2) - 1, s.length % 2 === 0 ? 2 : 1);
}

//substr 자르는거 (자를단어.substr(idx,갯수))
//Math.ceil
```

참고: [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil)
