# AWS EC2 Web Server Project

AWS Cloud Basic 실습 자료를 바탕으로 VPC 네트워크와 EC2 웹 서버를 구성한 프로젝트입니다.

## 프로젝트 개요

- 리전: Asia Pacific (Seoul), `ap-northeast-2`
- 사용 서비스: Amazon VPC, Amazon EC2, Security Group, AMI
- 선택 실습 범위: Application Load Balancer, IAM Role, Amazon S3
- VPC: `my-vpc`
- 서브넷:
  - `my-sub01`
  - `my-sub02`
- 보안 그룹:
  - `my-web-sg`
- 인스턴스:
  - `my-web01`
  - `my-web02`
- 인스턴스 유형: `t3.micro`
- 스크린샷 확인 가용 영역: `ap-northeast-2a`
- PDF 기준 권장 가용 영역: `ap-northeast-2a`, `ap-northeast-2c`
- 상태: 실행 중
- 상태 검사: 통과

> 참고: 공개 저장소에 올릴 수 있도록 AWS 계정 ID, 인스턴스 ID, 퍼블릭 IP, DNS 이름, 보안 그룹 ID는 문서에 포함하지 않았습니다.

## 구성도

```text
Internet User
  |
  | HTTP access
  v
Internet Gateway
  |
  v
Route Table
  |
  +-- Public Subnet: my-sub01
  |     |
  |     +-- EC2: my-web01
  |
  +-- Public Subnet: my-sub02
        |
        +-- EC2: my-web02
```

## 수행한 작업

- `my-vpc`를 생성하고 IPv4 CIDR을 `10.0.0.0/16`으로 설정했습니다.
- `my-sub01`, `my-sub02` 서브넷을 생성했습니다.
- 인터넷 게이트웨이를 연결하고 라우팅 테이블을 구성했습니다.
- VPC 리소스 맵에서 서브넷, 라우팅 테이블, 인터넷 게이트웨이 연결 상태를 확인했습니다.
- 퍼블릭 IP 자동 할당을 활성화해 퍼블릭 서브넷으로 구성했습니다.
- `my-web-sg` 보안 그룹을 생성하고 HTTP/SSH 접근 규칙을 설정했습니다.
- Amazon Linux 기반 `my-web01` EC2 인스턴스를 생성했습니다.
- `my-web01`에 `git`, `stress`, `nginx`를 설치하고 Nginx 웹 서버를 실행했습니다.
- 웹 콘텐츠를 배치하고 브라우저에서 접속을 확인했습니다.
- `my-web01`을 기반으로 AMI를 생성했습니다.
- 생성한 AMI를 사용해 `my-web02` 인스턴스를 추가 생성했습니다.
- `my-web02`의 웹 페이지를 별도 index 파일로 변경해 서버 구분이 가능하도록 했습니다.
- 두 인스턴스가 실행 중이고 상태 검사를 통과하는지 확인했습니다.

## 저장소 구성

- `README.md`: 프로젝트 개요
- `docs/aws-ec2-summary.md`: AWS 리소스 정리
- `docs/deployment-checklist.md`: 배포 및 점검 체크리스트
- `docs/lab-notes.md`: PDF 실습 기준 작업 노트
- `.gitignore`: Git에서 제외할 파일 목록

