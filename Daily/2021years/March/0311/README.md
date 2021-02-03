# 0. 스토리지 타입

## 1. 블록스토리지

- 데이터를 일정 크기의 블록으로 나누어 저장
- 호스트에서 파일 시스템을 생성
- Storage Area Network

## 2. 파일 스토리지

- 디렉토리 구조로 파일을 저장
- 스토리지 단에서 파일 시스템을 생성
- Network Attached Storage

## 3. 오브젝트 스토리지

- REST 기반의 API 호출을 통해 데이터에 접슨
- HTTP 프로토콜

---

# 1. Amazon EBS (Elastic Block Storage)

## 특징

- EC2 인스턴스내에 결합되어 사용할 수 있는 저장공간 볼륨
- 고성능 트랜잭션 워크로드에 사용
- 고가용성, 안정성, 확장성, 성능, 백업(스냅샷)

## 볼륨타입

→ 언제든지 변경 가능

### General-purpose SSD(gp2/gp3)

- NoSQL DB
- 트랜잭션 워크로드, 낮은 지연시간 필요한 애플리케이션

### Provisioned IOPS SSD(io1/io2)

- 관계형 데이터베이스
- I/O가 많은 데이터베이스 애플리케이션

### Throughput-optimized HDD(st1)

- 빅데이터, 분석
- 대랑의 데이터셋

### Cold HDD(sc1)

- 파일, 미디어
- 자주 엑세스 하지 않는 큰 사이즈의 데이터셋

## Amazon EBS Multi-Attach

### 고성능이 필요한 High Performance Computing 시스템

# 2. Amazon EFS

### 리눅스 NAS, 안정적이고 비용 효과적인 클라우드 네이티브 NFS 파일 스토리지 서비스

---

![Untitled](https://user-images.githubusercontent.com/58289110/110724426-158a0880-8259-11eb-864b-78bdf9a8772a.png)

- delete on termination 필수 체크

### EC2 서버 실행

![Untitled (1)](https://user-images.githubusercontent.com/58289110/110724431-16bb3580-8259-11eb-93fb-613ffb7cecb8.png)
