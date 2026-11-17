# aws-dr-infra

> **Multi-Region(서울·싱가포르)을 활용한 무중단 서비스 아키텍처**
> 서울 리전 장애 시 Global Accelerator가 트래픽을 싱가포르 리전으로 자동 전환하는 AWS DR(재해복구) 구성 프로젝트입니다. (개인 프로젝트)

![architecture](docs/architecture.png)

## 1. 프로젝트 목적

- 각 리전에 VPC를 구성하고 **Transit Gateway**로 두 리전의 VPC와 IDC(온프레미스 가정) 네트워크를 연결
- IDC ↔ AWS 구간은 **Site-to-Site VPN**으로 암호화된 사설 통신 구성
- **Route 53 Resolver + 내부 DNS 서버**로 리전 간 도메인 이름 기반 통신 구현
- 서울 IDC의 **Master DB → 싱가포르 IDC의 Slave DB 복제**로 데이터 손실 방지
- **Global Accelerator** 헬스체크 기반으로 장애 시 다른 리전으로 자동 페일오버

### 시나리오
아시아 시장을 대상으로 하는 가상의 글로벌 패션·뷰티 이커머스 기업 "GlobalStyle"이 서울·싱가포르에 인프라를 구축하여, 한 리전에 장애가 나도 서비스가 중단되지 않도록 하는 상황을 가정했습니다.