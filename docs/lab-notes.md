# PDF 실습 기준 작업 노트

이 프로젝트는 `AWS_Lab (1).pdf`의 Cloud Basic 실습 흐름을 바탕으로 정리했습니다.

## Lab 1: Network

- 서울 리전(`ap-northeast-2`)을 선택했습니다.
- `my-vpc` VPC를 생성했습니다.
- VPC CIDR은 `10.0.0.0/16`으로 구성했습니다.
- `my-sub01`, `my-sub02` 서브넷을 생성했습니다.
- `my-web-sg` 보안 그룹을 생성했습니다.
- 인터넷 게이트웨이를 VPC에 연결했습니다.
- 라우팅 테이블을 생성하고 인터넷 게이트웨이 경로를 추가했습니다.
- 서브넷을 라우팅 테이블에 연결하고 퍼블릭 서브넷으로 구성했습니다.

## Lab 2: EC2 Web Server

- `my-web01` 인스턴스를 생성했습니다.
- Amazon Linux에서 `git`, `stress`, `nginx`를 설치했습니다.
- Nginx를 시작하고 자동 실행되도록 설정했습니다.
- 웹 서버 파일을 `/usr/share/nginx/html/`에 배치했습니다.
- `index1.html`을 `index.html`로 복사해 `my-web01` 웹 페이지를 구성했습니다.
- `my-web01`에서 AMI를 생성했습니다.
- 생성한 AMI를 사용해 `my-web02` 인스턴스를 만들었습니다.
- `index2.html`을 `index.html`로 복사해 `my-web02` 웹 페이지를 구성했습니다.
- 두 웹 서버가 브라우저에서 접속 가능한지 확인했습니다.

## Lab 3: High Availability

- Application Load Balancer `my-alb`를 생성하는 흐름을 정리했습니다.
- 대상 그룹 `webserver-tg`를 생성하고 EC2 인스턴스를 등록하는 흐름을 정리했습니다.
- ALB 보안 그룹 `my-alb-sg`를 만들고 웹 서버 보안 그룹에서 ALB를 HTTP 소스로 지정하는 흐름을 정리했습니다.
- ALB DNS 이름으로 로드밸런싱 접속을 테스트하는 절차를 정리했습니다.

## S3 IAM Role Practice

- EC2가 S3에 접근할 수 있도록 IAM 역할 `myS3AccessRole`을 생성하는 흐름을 정리했습니다.
- `my-web01`, `my-web02`에 IAM 역할을 연결하는 절차를 정리했습니다.
- EC2에서 AWS CLI로 S3 파일 업로드와 다운로드를 테스트하는 절차를 정리했습니다.

## 공개 저장소 업로드 기준

다음 정보는 저장소에 올리지 않았습니다.

- AWS 계정 ID
- 액세스 키와 시크릿 키
- `.pem` 키 파일
- 인스턴스 ID
- 보안 그룹 ID
- 퍼블릭 IP 주소
- 퍼블릭 DNS 이름
- 버킷 이름
