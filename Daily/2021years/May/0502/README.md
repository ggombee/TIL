# 0. 아나콘다 설치

appwiz.cpl -- 애플리케이션 확인

![Untitled (2)](https://user-images.githubusercontent.com/58289110/117740285-13353200-b23b-11eb-86e8-9100180c5030.png)

![Untitled (3)](https://user-images.githubusercontent.com/58289110/117740284-129c9b80-b23b-11eb-9f92-4d11fe8f4538.png)

# 1. 아나콘다 시스템 변수 및 환경변수 설정

```jsx
ANACONDA_HOME1 C:\ProgramData\Anaconda3

ANACONDA_HOME2 C:\ProgramData\Anaconda3\Scripts

ANACONDA_HOME3 C:\ProgramData\Anaconda3\Library\bin

ANACONDA_HOME4 C:\ProgramData\Anaconda3\Library\mingw-w64\bin
```

위에 있는 아나콘다 설치 경로 및 이름을 변수 설정해준다

![Untitled (4)](https://user-images.githubusercontent.com/58289110/117740281-116b6e80-b23b-11eb-91ca-67f7cd054764.png)

시스템 변수와 환경변수를 설정해준다!

![Untitled (5)](https://user-images.githubusercontent.com/58289110/117740291-14665f00-b23b-11eb-8627-6e458befe666.png)

cmd에서 버전이 뜨면 설치 완료다!

![Untitled (6)](https://user-images.githubusercontent.com/58289110/117740290-14665f00-b23b-11eb-9de8-3de78cd92471.png)

# 2. 파이참 설치

![Untitled (7)](https://user-images.githubusercontent.com/58289110/117740289-13cdc880-b23b-11eb-8cf4-73941fa0fa7b.png)

![Untitled (8)](https://user-images.githubusercontent.com/58289110/117740288-13cdc880-b23b-11eb-9cc5-93a5de69f89e.png)

# 3. git 레포지토리에 추가

git init
git add .
git commit -m "2021-05-1 15:30"
git remote add origin [https://github.com/ggombee/python_ncs.git](https://github.com/ggombee/python_ncs.git)
git push -u origin master

git config --global [user.name](http://user.name/) "ggombee“
git config --global user.email ["minniemice98@gmail.com](mailto:%22minniemice98@gmail.com)"

# 4. 파이썬 예제

### calculator.py

![Untitled (9)](https://user-images.githubusercontent.com/58289110/117740287-13353200-b23b-11eb-8740-c46a2105377a.png)

주피터노트북과 파이참에서 작업시 차이점은 파이참은 파일 단위 혹은 프로젝트 단위로 실행한다. 

-> 어플리케이션 제작

주피터는 한줄한줄 특정 코드만 실행한다. -> 데이터 분석__name__ 변수는 private 으로 사용하는 ...

외부적: public  -> 아이디
내부적: private -> 비밀번호자연어(한글, 영어, ...) word <-> 기계어(C, Java, Python...) term기계어는 크게 2가지

숫자 타입 변수
문자 타입 변수main.py 는 모듈이다(함수, 클래스)

main 이란 이름은 엔트리 포인트(모듈의 진입점)이다.파일이나 폴더 이름 변경은 SHIFT + F6 입니다.

__init__.py oop패키지 내부적으로 사용하는 파일이다.

객체지향

```jsx
class ...
    def __init__(self):
         pass
    def ... 메소드함수형 구조
def ...def __init__ 초기화: 가장 먼저 실행되는 파일또는 코드. private 한 값의 저장공간
return 이 없습니다.
def sum(self):
return 이 있습니다. 계산결과를 공개해라.의미맨 앞에 있는 라인 - 루트라인
```

### Naming Convention

파이썬의 문법요소들을 명시할 때 이름을 주는 방법에 대한 합의이다.
클래스는 대문자로 시작하고, 뜻이 바뀌는 단어의 연결지점은 다시 대문자로 하는 방식(파스칼 표기법)이고, 함수나 메소드는 소문자로 시작하고, 뜻이 바뀌는 단어의 연결지점은 다시 대문자로 하는 방식(카멜 표기법)이다. 

모듈(=파이썬 파일)과 패키지는 다 소문자이고, 뜻이 바뀌는 지점에서 _ 를 처리하는 방식(스네이크-바 방식)을 주는 것이다. 

반드시 하라는 것은 아니고, 권고사항이다.

# calculation.py

```python
class Calculator:

    def __init__(self, first, second):
        self.first = first
        self.second = second

    def sum(self):
        return self.first + self.second

    def sub(self):
        return self.first - self.second

    def mul(self):
        return self.first * self.second

    def div(self):
        return self.first / self.second

    def mod(self):
        return self.first % self.second

    @staticmethod
    def execute():
        calc = Calculator(int(input("첫번째 수")), int(input("두번째 수")))
        print(f'첫번째수: {calc.first}')
        print(f'두번째수: {calc.second}')
        print(f'{calc.first} + {calc.second} = {calc.sum()}')
        print(f'{calc.first} - {calc.second} = {calc.sub()}')
        print(f'{calc.first} * {calc.second} = {calc.mul()}')
        print(f'{calc.first} / {calc.second} = {calc.div()}')
        print(f'{calc.first} % {calc.second} = {calc.mod()}')

if __name__ == '__main__':
    Calculator.execute()
```

# person.py

```python
class Person:
    def __init__(self, name, age, address):
        self.name = name
        self.age = age
        self.address = address

    def greeting(self):
        print(f'안녕하세요. 제 이름은 {self.name}이고,' 
              f' 나이는 {self.age}살이고,' 
              f' {self.name} 에서 거주합니다.')

    @staticmethod
    def main():
        eunbee = Person('은비',24,'서울')
        eunbee.greeting()
        minjae = Person('민재',27,'경기')
        minjae.greeting()

if __name__ == '__main__':
    Person.main()
```

## git bash

```python
//이후 커밋
git add .
git commit -m "2021-05-01 Grade 추가"

//초기설정
git init
git add .
git commit -m "2021-05-1 15:30"
git remote add origin https://github.com/ggombee/python_ncs.git
git push -u origin master

git config --global user.name "ggombee“
git config --global user.email "minniemice98@gmail.com"
```

# grade.py

```python
'''
클래스에 학생의 이름을 입력하면
해당 학생이 얻은 3과목의 평균점수에 따라 A - F 까지 출력
해당 문제를 해결하기 위해서는 72페이지의 리스트를 참조
'''

class Grade:
    def __init__(self,  name):
        self.name = name
        self.marks = [] # list로 타입선언

    def addMarks(self, mark):
        self.marks.append(mark)

    def avg(self):
        return sum(self.marks) / len(self.marks)

    @staticmethod
    def main():
        student = Grade(input("학생이름 입력"))
        for subject in ['국어', '영어', '수학']:
            student.addMarks(int(input(subject + "점수 입력")))
        avg = student.avg()
        print(f'{student.name}의 과목 평균은 {int(avg)} 점 이다.')
        if avg >= 90:
            grade = 'A'
        elif avg >= 80:
            grade = 'B'
        elif avg >= 70:
            grade = 'C'
        elif avg >= 60:
            grade = 'D'
        elif avg >= 50:
            grade = 'E'
        else:
            grade = 'F'

        print(f'{student.name}의 과목 평균은 {int(avg)}점, 학점은 {grade} 이다.')

if __name__ == '__main__':
    Grade.main()
```

# contacts.py

```python
'''
이름, 전화번호, 이메일, 주소를 받아서
연락처 입력, 출력, 삭제하는 프로그램을 완성하시오.
'''
class Contacts:

    def __init__(self, name, phone, email, address):
        self.name = name
        self.phone = phone
        self.email = email
        self.address = address

    def print_info(self):
        print(f'이름: {self.name}')
        print(f'전화번호: {self.phone}')
        print(f'이메일: {self.email}')
        print(f'주소: {self.address}')

    @staticmethod
    def set_contact():
        name = input("아름: ")
        phone = input("전화번호: ")
        email = input("이메일: ")
        address = input("주소: ")
        return Contacts(name, phone, email, address)

    @staticmethod
    def get_contacts(ls):
        for i in ls:
            i.print_info()

    @staticmethod
    def del_contact(ls,name):
        for i, j in enumerate(ls): # i = index, j = element 리스트내부의 ㅜ소
            if j.name == name:
                del ls[i]

    @staticmethod
    def print_menu():
        print("1. 연락처 입력")
        print("2. 연락처 출력")
        print("3. 연락처 삭제")
        print("4. 종료")
        menu = input("메뉴 선택 : ")
        return int(menu)

    @staticmethod
    def main():
        ls = []
        while 1:
            menu = Contacts.print_menu()
            if menu == 1:
                t = Contacts.set_contact()
                ls.append(t)
            elif menu == 2:
                Contacts.get_contacts(ls)
            elif menu == 3:
                name = input("삭제할 이름:")
                Contacts.del_contact(ls, name)
            elif menu == 4:
                break

if __name__ == '__main__':
    Contacts.main()
```
