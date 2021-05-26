### **문제 설명**

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

### 제한사항

- 문자열 s의 길이 : 50 이하의 자연수
- 문자열 s는 알파벳으로만 이루어져 있습니다.

split 함수는 문자기준으로 나누어 배열에 저장 한다.

ex) pooxyy→ [poox ,y, y]

```jsx
function numPY(s){
  //함수를 완성하세요
    return s.toUpperCase().split("P").length === s.toUpperCase().split("Y").length;
}
```

```jsx
function solution(s) {
  const p = s.split('').filter(v => ['p', 'P'].includes(v));
  const y = s.split('').filter(v => ['y', 'Y'].includes(v));
  return p.length === y.length;
}
```

**해당 문자열.match('찾을 단어')**

**// match()함수는 인자에 포함된 문자를 찾으면 이를 반환함**

```jsx
function numPY(s) {
  return s.match(/p/ig||[]).length == s.match(/y/ig||[]).length;
}
```

replace() 메서드는 어떤 패턴에 일치하는 일부 또는 모든 부분이 교체된 새로운 문자열을 반환

ex) 

const p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';

console.log(p.replace('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"

```jsx
function solution(s){
  return s.replace(/p/gi, '').length == s.replace(/y/gi, '').length;
}
```

참고: [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/replace](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
