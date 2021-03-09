![Untitled](https://user-images.githubusercontent.com/58289110/110439144-70f1b480-80fa-11eb-875e-e62b76da4ec0.png)

## 1. VPC 생성

### VPC 마법사 통해 생성

![Untitled (1)](https://user-images.githubusercontent.com/58289110/110439179-7c44e000-80fa-11eb-9e0e-9a9bdc859fcd.png)

- default vpc가 존재함
- 별다른 설정안하면 default vpc로 진행
- subnet도 default존재
- workload 하는경우 default 가능

### vpc 구성 선택

- 퍼블릭 서브넷 - 인터넷으로부터 연결 가능
- 프라이빗 서브넷 - 인터넷으로부터 연결 불가

### CIDR 블록(이해 필요)

### 서브넷 추가

- 중첩 서브넷 생성시 ip주소가 겹쳐서 알림뜸

### 라우팅 테이블

- 네비게이션 같은 역할
- 기본 라우팅 테이블 생성
- 인터넷 연결 필요시 라우팅 편집필요

### 보안그룹 생성하기

- 인바운드 규칙 - 설정 안하면  모든 트래픽 허용 안함
- 위치무관 - 모든 트래픽 허용
- SSH는 아이피 특정하는게 좋음SSH는 아이피 특정하는게 좋음

## 2. EC2

- 온프레미스 형식 VM

### t2.micro

- 성능 대비 가격 저렴

### 네트워크

- 미리 만들어 놓은(VPC-Lab) VPC 선택 후 서브넷(public subnet A) 선택
- 퍼블릭 IP 자동할당 활성화로 변경

 

### 고급세부정보

- 사용자 데이터

- 웹서버를 띄울때 인스턴스를 일일이 설치하는게 아니라 알아서 해주는 기능 (아래스크립트 넣어줄것)

```jsx
#include [https://s3.amazonaws.com/immersionday-labs/bootstrap.sh](https://s3.amazonaws.com/immersionday-labs/bootstrap.sh)
```

### 스토리지 추가

- 다양한 사이즈, 볼륨의 스토리지 생성가능

### 태그 추가

- 리소스 관리할때 중요

### public IPv4 주소

There was a problem connecting to your instance An error occurred and we were unable to connect to your instance. Wait a few minutes and try again. ì??¬ì????ë????

EC2 >  대시보드 > 인스턴스 상태 > 상태 검사 가 검사 통과 상태 일때 정상적으로 실행됨

![Untitled (2)](https://user-images.githubusercontent.com/58289110/110439210-8830a200-80fa-11eb-977a-5fe7778480d8.png)

퍼블릭 주소 url창에 치면

![Untitled (3)](https://user-images.githubusercontent.com/58289110/110439248-9383cd80-80fa-11eb-8e38-25fb19f85980.png)

이 페이지 뜸!!!

## 3. AMI 생성하기

### 우클릭, 작업 > 이미지 생성

- 설명은 자세하게 써야지 관리가 용이관리가 용이
- 상태는 이미지 > AMI에서 확인가능

![Untitled (4)](https://user-images.githubusercontent.com/58289110/110439280-9ed6f900-80fa-11eb-9168-059177bc3fa1.png)

## 4. AMI 기반 인스턴스 만들기

- 붕어빵틀 AMI만들어서 EC2 리눅스 서버를 찍어내는 느낌

![Untitled (5)](https://user-images.githubusercontent.com/58289110/110439313-a6969d80-80fa-11eb-8bbf-e5763abed4da.png)

## 5. 로드밸런서 구성하기

- 두개의 인스턴스를 생성했을때 트래픽의 부하를 분산해주는 역할

### ELB(Elastic Load Balancing) 이해하기

- load balancer 생성 (web alb로 생성 application loadbalancer)
- 새로고침을 할때마다 서버가 바뀐다.

![Untitled (6)](https://user-images.githubusercontent.com/58289110/110439367-b57d5000-80fa-11eb-955b-66be5597fc90.png)

- 현재 ip주소 2개와 dns주소로 접속이 가능하여, 보안상 취약점이 존재한다.
- 로드밸런서에서 오는 요청만 받게 구성하는게 바람직

## 6. 도메인 주소로만 접속

- 보안그룹 > webserver-sg > 인바운드 규칙 편집에서 0.0.0.0/0 삭제해준다

![Untitled (7)](https://user-images.githubusercontent.com/58289110/110439369-b7471380-80fa-11eb-972e-61f978f444a9.png)

## 자원삭제

EC2(로드밸런서,인스턴스,AMI)→ SNS주제 삭제 →오토스케일링 삭제(탬플릿, 그룹, 버킷, )→VPC
