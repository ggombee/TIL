### **문제 설명**

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

### 제한 사항

- str은 길이 1 이상인 문자열입니다.

split으로 배열로 만들어 준뒤 다시 join으로 옵젝 형식으로 변환

charCodeAt ⇒  문자의 숫자코드를 알려주는 메서드

```jsx
function solution(s) {
  return s.split('').sort((prev, cur) => cur.charCodeAt() - prev.charCodeAt()).join('');
}
```

```jsx

function solution(s) {
  return s
    .split("")
    .sort()
    .reverse()
    .join("");
}
```
