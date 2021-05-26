### **문제 설명**

길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.

### 제한 조건

- n은 길이 10,000이하인 자연수입니다.

n만큼 반복 + n이 홀수일때 수, 짝수일때 ''

```jsx
const waterMelon = n => {
    return '수박'.repeat(n/2) + (n%2 === 1 ? '수' : '');
}
```

```jsx
function solution(n) {
    return '수박'.repeat(n).substr(0,n);
}

//repeat은 앞에배열을 괄호안만큼 반복
//substr은 인덱스괄호 첫번째부터 n까지 자르기
```

참고  : [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/repeat](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/repeat)
