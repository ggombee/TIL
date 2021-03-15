# 1. 인텔리제이로 스프링 부트 시작하기

# 1.  Toolbox app 설치

- IntelliJ JVM 옵션 설정

# 2. 프로젝트 생성

## > 이클립스의 워크스페이스와 같은 개념이 없다.

프로젝트와 모듈의 개념만 존재,

모든 프로젝트를 한번에 불러올 수 없다. 한화면에서는 하나의 프로젝트만 열린다.

## > Gradle 프로젝트를 생성한다.

![Untitled (7)](https://user-images.githubusercontent.com/58289110/111097356-b2fc7980-8584-11eb-8934-4ea00f2e2f25.png)

## > GroupId 와 ArtifactId를 등록한다.

![Untitled (8)](https://user-images.githubusercontent.com/58289110/111097374-bbed4b00-8584-11eb-8c01-908f04760e89.png)

## > Gradle 프로젝트 스프링 부트 프로젝트 변경

### 1. build.gradle 파일에서 아래 코드 추가

![Untitled (9)](https://user-images.githubusercontent.com/58289110/111097399-c60f4980-8584-11eb-9744-a81210e5d93f.png)

프로젝트의 플러그인 의존성 관리를 위한 설정이다.

ext라는 키워드는 build.gradle에서 사용하는 전역변수를 설정한다는 의미,,

springBootVersion 전역변수를 생성하고 그 값을 '2.1.7.RELEASE'로 하겠다는 의미

### 2. 플러그인 의존성 적용

repositories는 각종 의존성 라이브러리를 어떤 원격 저장소에서 받을지를 정한다. 기본적으로 mavenCentral을 많이 사용하지만 최근에는 라이브러리 업로드 난이도 때문에 jcenter도 많이 사용한다.

전체코드는

```java
buildscript {
    ext {
        springBootVesion = '2.1.7.RELEASE'
    }
    repositories {
        mavenCentral()
        jcenter()
    }

    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'

group 'ggom.kun.dev'
version '1.0-SNAPSHOT'
sourceCompatibility = 1.8

repositories {
    mavenCentral()
}

dependencies {
    compile('org.springframework.boot:spring-boor-starter-web')
    testCompile('org.springframework.boot:spring=boot-starter-test')
}
```

이렇게 생겼다!

### > 프로젝트 깃에 올리기

![Untitled (10)](https://user-images.githubusercontent.com/58289110/111097402-c7407680-8584-11eb-9bbc-d2bb91e023ea.png)

### 깃 ignore 플러그인 설치

![Untitled (11)](https://user-images.githubusercontent.com/58289110/111097405-c7d90d00-8584-11eb-9f11-1ee57ceefeeb.png)

### gitignore 설정 → 깃 커밋푸시!

![Untitled (12)](https://user-images.githubusercontent.com/58289110/111097406-c90a3a00-8584-11eb-96db-40389dc734f2.png)
