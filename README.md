# AWS EC2 Web Server Project

AWS EC2 기반으로 웹 서버 2대를 구성한 실습 프로젝트입니다.

## 프로젝트 개요

- 리전: Asia Pacific (Seoul), `ap-northeast-2`
- 사용 서비스: Amazon EC2
- 인스턴스:
  - `my-web01`
  - `my-web02`
- 인스턴스 유형: `t3.micro`
- 가용 영역: `ap-northeast-2a`
- 상태: 실행 중
- 상태 검사: 통과

> 참고: 공개 저장소에 올릴 수 있도록 AWS 계정 ID, 인스턴스 ID, 퍼블릭 IP, DNS 이름, 보안 그룹 ID는 문서에 포함하지 않았습니다.

## 구성도

```text
User
  |
  | HTTP/SSH access
  v
Security Group
  |
  +-- EC2: my-web01
  |
  +-- EC2: my-web02
```

## 수행한 작업

- 웹 서버 실습용 EC2 인스턴스 2대를 생성했습니다.
- 두 인스턴스를 서울 리전에 배치했습니다.
- 두 인스턴스가 실행 중인지 확인했습니다.
- 인스턴스 상태 검사가 정상 통과되는지 확인했습니다.
- EC2 콘솔에서 같은 보안 그룹 기준으로 인스턴스를 확인했습니다.

## 저장소 구성

- `README.md`: 프로젝트 개요
- `docs/aws-ec2-summary.md`: AWS 리소스 정리
- `docs/deployment-checklist.md`: 배포 및 점검 체크리스트
- `.gitignore`: Git에서 제외할 파일 목록

## 보안 주의사항

공개 GitHub 저장소에는 다음 정보를 올리지 않는 것이 좋습니다.

- AWS 계정 ID
- 액세스 키 또는 시크릿 키
- `.pem` 키 파일
- 인스턴스 ID
- 퍼블릭 IP 주소
- 퍼블릭 DNS 이름
- 보안 그룹 ID
- SSH 사용자명 또는 접속 세부 정보
