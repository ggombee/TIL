# 1. Jira 협업 툴 설치하기
---
## 1. Jira 서버버전 설치하기

### Jira 설치

[https://www.atlassian.com/ko/software/jira/download](https://www.atlassian.com/ko/software/jira/download) 에 들어가서 클라우드 버전이 아닌 서버 버전을 설치한다

# 1. AWS EC2 인스턴스 생성

## EC2 대시보드에 가서 인스턴스 생성을 누른다.

인스턴스 생성시에는 각각의 설정을 해줘야한다.

![image](https://user-images.githubusercontent.com/58289110/113541638-9c928c80-961d-11eb-872a-8ec19ea96613.png)

## Step 1. 먼저  Amazon Linux AMI 서버를 선택한다.

<img width="1140" alt="Screen_Shot_2021-03-27_at_2 04 23_AM" src="https://user-images.githubusercontent.com/58289110/113541744-d06db200-961d-11eb-8851-4facfac87d4b.png">


## Step 2.  인스턴스의 타입은 t2.large

지라의 메모리용량이 클 수 있어 micro버전이 아닌 t2.large 버전으로 진행한다.


<img width="627" alt="Screen_Shot_2021-03-27_at_2 07 53_AM" src="https://user-images.githubusercontent.com/58289110/113541768-da8fb080-961d-11eb-8588-5264469aff74.png">

## Step3~ Step 5.

스텝3 부터 5까지는 기본값을 유지하고 넘어간다.

## Step 6 . 보안그룹 구성

보안그룹은 혹시 모를 과금을 방지하기 위하여 내 IP만 허용한다.

22번 포트와 지라 서비스를 올리기 위한 8080포트를 올려준다.

![Untitled](https://user-images.githubusercontent.com/58289110/113541932-280c1d80-961e-11eb-8a48-71c6c0f66b75.png)


## Step7. 인스턴스 시작

검토후 시작을 누른 뒤 키페어를 지정하면 인스턴스 시작을 할 수 있다.

처음 시작했을때는  initializing 상태이다. 이때는 접속을 해도 오류가 발생하니 기다렸다가 인스턴스의 상태가  

checks passed 상채로 바뀌면 접속이 가능해진다.

![Untitled (1)](https://user-images.githubusercontent.com/58289110/113541784-e11e2800-961d-11eb-9931-6fd8cd906c82.png)

![Untitled (2)](https://user-images.githubusercontent.com/58289110/113541787-e24f5500-961d-11eb-9382-30d24bc5238d.png)

# 2. 터미널로 도커 설치하기

## 1. 터미널 열기

인스턴스를 런치 할때 만들거나 사용한 키가 있는 곳으로 이동한다

![Untitled (3)](https://user-images.githubusercontent.com/58289110/113541805-ea0ef980-961d-11eb-8727-f0d87e309df7.png)


그리고 해당 키를 아래 명령어를 입력하고  서버를 실행시키면 된다.

```jsx
ssh -i keyname username@portnumber
```

간혹가다 공개키의 권한 문제로 인해 서버 접속이 거부되는 경우가 있는데 그때는 

chmod 400 keyname

명령어로 권한을 설정해주면 된다.

완료 후 서버에 정상적으로 접속이 되면,

![Untitled (4)](https://user-images.githubusercontent.com/58289110/113541821-f09d7100-961d-11eb-9664-edb84433dd31.png)

이런 화면이 나온다..(~~드디어!!~~)

다음은 도커를 설치해보자.

## 2. 도커 설치

터미널에 docker라는 명령어를 치면 설치가 안되어 있기 때문에 command not found가 나온다

아래 명령어를 실행해서 docker를 설치해보자!

```jsx
sudo yum install docker-io
```

![Untitled (5)](https://user-images.githubusercontent.com/58289110/113541830-f5622500-961d-11eb-8fb4-b02a36e7f955.png)


중간에 is this ok가 나오면 y를 입력해주면 설치가 정상적으로 실행된다.

설치가 완료된 후 docker라는 명령어를 통해 설치가 되었다는 것을 확인가능하다.

<img width="339" alt="Screen_Shot_2021-04-05_at_12 10 49_AM" src="https://user-images.githubusercontent.com/58289110/113541839-fabf6f80-961d-11eb-80e3-7f9f04e0b053.png">


다음은 데몬이 실행 되어 있는지 docker ps -a로 확인한다.

도커가 실행되어 있지 않다면

아래 명령어를 통해 도커를 실행한다.

```jsx
sudo systemctl start docker
```
