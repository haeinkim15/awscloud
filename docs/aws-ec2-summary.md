# AWS EC2 리소스 정리

이 문서는 AWS Cloud Basic 실습 자료를 바탕으로 구성한 리소스를 정리합니다.

## VPC 및 네트워크

| 리소스 | 이름 | 설정 |
| --- | --- | --- |
| VPC | `my-vpc` | IPv4 CIDR `10.0.0.0/16` |
| Subnet | `my-sub01` | `ap-northeast-2a`, `10.0.1.0/24` |
| Subnet | `my-sub02` | `ap-northeast-2c`, `10.0.2.0/24` |
| Internet Gateway | `my-igw` | `my-vpc`에 연결 |
| Route Table | `my-route` | 인터넷 게이트웨이로 기본 라우팅 |

## AWS 콘솔 확인 내용

제공된 VPC 리소스 맵 스크린샷에서 다음 구성이 확인되었습니다.

- VPC `my-vpc`가 `Available` 상태입니다.
- VPC IPv4 CIDR은 `10.0.0.0/16`입니다.
- VPC 내부에 서브넷 2개가 있습니다.
  - `my-sub01`: `ap-northeast-2a`
  - `my-sub02`: `ap-northeast-2c`
- 라우팅 테이블 2개가 생성되어 있습니다.
- `my-route` 라우팅 테이블이 인터넷 게이트웨이 `my-igw`와 연결되어 있습니다.

스크린샷 원본에는 AWS 계정 ID와 VPC ID 같은 식별자가 포함되어 있어 저장소에는 업로드하지 않았습니다.

## 보안 그룹

| 이름 | VPC | 용도 |
| --- | --- | --- |
| `my-web-sg` | `my-vpc` | EC2 웹 서버 접근 제어 |

권장 공개 규칙은 HTTP만 전체 공개하고, SSH는 실습 환경이 아니라면 내 IP로 제한하는 것입니다.

## EC2 인스턴스

| 이름 | 리전 | 가용 영역 | 인스턴스 유형 | 상태 | 상태 검사 |
| --- | --- | --- | --- | --- | --- |
| `my-web01` | `ap-northeast-2` | `ap-northeast-2a` | `t3.micro` | 실행 중 | 3/3 검사 통과 |
| `my-web02` | `ap-northeast-2` | `ap-northeast-2a` | `t3.micro` | 실행 중 | 3/3 검사 통과 |

> PDF 실습 기준으로는 `my-web02`를 `my-sub02` 또는 `ap-northeast-2c`에 배치하는 흐름도 포함되어 있습니다. 현재 표는 제공된 AWS 콘솔 스크린샷에서 확인된 상태를 기준으로 정리했습니다.

## 웹 서버 구성

- OS: Amazon Linux
- Web server: Nginx
- 설치 패키지: `git`, `stress`, `nginx`
- `my-web01`에서 웹 서버를 구성한 뒤 AMI를 생성했습니다.
- 생성한 AMI를 사용해 `my-web02`를 만들었습니다.
- 각 서버의 `index.html`을 다르게 배치해 접속 대상 서버를 구분했습니다.

## 선택 실습 항목

| 항목 | 리소스명 | 목적 |
| --- | --- | --- |
| Application Load Balancer | `my-alb` | 두 웹 서버로 HTTP 트래픽 분산 |
| Target Group | `webserver-tg` | EC2 인스턴스 대상 그룹 |
| ALB Security Group | `my-alb-sg` | ALB HTTP 접근 제어 |
| IAM Role | `myS3AccessRole` | EC2에서 S3 접근 |

## 네트워크 및 보안

- 인스턴스들은 보안 그룹에 연결되어 있습니다.
- 민감한 식별자는 저장소에 포함하지 않았습니다.
- 스크린샷을 공개할 때는 다음 정보를 가려야 합니다.
  - AWS 계정 ID
  - 인스턴스 ID
  - 보안 그룹 ID
  - 퍼블릭 IPv4 주소
  - 퍼블릭 DNS 이름

## 권장 보안 그룹 규칙

| 유형 | 포트 | 소스 | 목적 |
| --- | --- | --- | --- |
| SSH | 22 | 내 IP만 허용 | 서버 관리 |
| HTTP | 80 | `0.0.0.0/0` | 웹 접속 |
| HTTPS | 443 | `0.0.0.0/0` | 보안 웹 접속 |

공개 환경에서는 SSH 포트 22를 `0.0.0.0/0`으로 열지 않는 것이 좋습니다.

## 운영 메모

- 불필요한 비용을 막기 위해 사용하지 않을 때는 EC2 인스턴스를 중지합니다.
- `Name`, `Project`, `Owner` 같은 태그를 사용해 리소스를 관리합니다.
- 개인 키 파일은 저장소 밖에 보관합니다.
