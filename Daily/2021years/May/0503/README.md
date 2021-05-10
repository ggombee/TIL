# 4. 파이썬 기본문법

## **자료형 (Data Type)**

스칼라 개념

숫자: int, float, complex

문자: str

벡터 개념

리스트

튜플

세트

딕셔너리

## **변수 (variable)**

변수는 자료형의 값을 저장하는 공간이다.

## **연산자 (Operator)**

```jsx
a = 14

b = 5

 

# 산술 연산자

sum = a + b

sub = a - b

multiply = a * b

divide = a / b

divide2 = int(a // b)

remainder = a % b

power = 2 ** 10

 

print('덧셈 : %d' % (sum))

print('뺄셈 : %d' % (sub))

print('곱셈 : %d' % (multiply))

print('나눗셈 : %f' % (divide))

print('나눗셈 : %f' % (divide2))

print('나머지 : %d' % (remainder))

print('제곱 : %d' % (power))

 

# 양의 정수는 우측 정렬

# 정수는 확보할 자리수

print('제곱2: [%3d]' % (power))

print('제곱3: [%6d]' % (power))

print('제곱4: [%-6d]' % (power))

 

su = 12.3456789

print('서식1 : [%f]' % (su))

print('서식2 : [%.2f]' % (su))

print('서식3 : [%6.2f]' % (su))

print('서식4 : [%-6.2f]' % (su))
```

## **입출력(I/O)**

```jsx
# 학생의 이름과 국어, 영어, 수학 점수를 입력 받으세요.

# 김철수, 50, 60, 80

# 총점은 소수점 2자리로, 평균은 소수점 3자리로 출력하세요.

 

# 출력 결과

# 이름 : 김철수

# 국어 : 50점

# 영어 : 60점

# 수학 : 80점

# 총점 : 190.00

# 평균 : 63.333

 

name = input('이름을 입력하세요')

kor = int(input('국어 점수를 입력하세요'))

eng = int(input('영어 점수를 입력하세요'))

math = int(input('수학 점수를 입력하세요'))

total = kor + eng + math

avg = total/3

 

print('이름 : %s' % (name))

print('국어 : %d점' % (kor))

print('영어 : %d점' % (eng))

print('수학 : %d점' % (math))

print('총점 : %.2f점' % (total))

print('평균 : %.3f점' % (avg))

su = 3

fruit = '사과'

 

# 인덱스 기반 매개변수 대입

print('positional argument')

str1 = '나는 {}를 {}개 먹었습니다.'

print(str1.format(fruit, su))

 

# 이 방법 추천

str2 = '나는 {0}를 {1}개 먹었습니다.'

print(str2.format(fruit, su))

 

str3 = '나는 {1}를 {0}개 먹었습니다'

print(str3.format(su, fruit))

 

print('keyword argument')

str4 = '나는 {abc}를 {defg}개 먹었습니다.'

print(str4.format(defg=su, abc=fruit))

 

# 2가지 혼합 방식

str5 = '나는 {abc}를 {}개 먹었습니다.'

print(str5.format(su, abc=fruit))

 

# # 이렇게 하면 안된다. positional argument가 앞에 오고 키워드 인자는 뒤에 와야 함

# str6 = '나는 {abc}를 {}개 먹었습니다.'

# print(str6.format(abc=fruit, su))

 

name = '김철수'

fruit = '사과'

su1 = 8

 

# 서식 지정자 %s(string), %d(decimal)

# %f(float): 기본 값으로 소수점 6자리까지 표시

# %c(문자 1개), %o(8진수), %x(16진수)

# %% : %문자를 표현할 때 사용

myformat = '%s가 %s를 %d개 먹었습니다.'

print(myformat % (name, fruit, su1))

 

su1 = 4

su2 = 9

# 4 곱하기 9는 36입니다.

 

myformat2 = '%d 곱하기 %d는 %d입니다.'

print(myformat2 % (su1, su2, su1*su2))

 

# pow(a, b) : a의 b 제곱

print(pow(5, 2))

 

# 2.0의 10.0승은 1024.0입니다.

su3 = 2.0

su4 = 10.0

myformat3 = '%f의 %f승은 %f입니다.'

print(myformat3 % (su3, su4, pow(su3,su4)))

 

rate = 0.4567

print('비율 : %.3f%%' % (100*rate))
```

## **파이썬 알고리즘 (Python Algorithm**

### **if 문**

조건문 뒤에는 반드시 콜론(:)이 붙는다

조건부 표현식

message = “success” if score >= 60 else “failure”

### **while 문**

### **for 문**

List Comprehension

a = [1,2,3,4]

result = [ i * 3 for i in a if i % 2 == 0 ]

print(result)

[6, 12]
