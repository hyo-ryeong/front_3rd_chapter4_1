# 프론트엔드 배포 파이프라인

## 개요

아래는 GitHub Actions를 활용해 구축한 프론트엔드 배포 파이프라인입니다. 이 파이프라인은 Next.js 프로젝트를 자동으로 빌드하고, S3와 CloudFront를 통해 배포합니다.


<img width="824" alt="diagram 4" src="https://github.com/user-attachments/assets/a2fdf6ae-ee04-4187-99a5-4696bb550688">



---

## 다이어그램 설명

- **GitHub Actions**: 워크플로우 트리거 및 실행.
- **AWS S3**: 빌드 결과물 저장.
- **AWS CloudFront**: 전 세계 사용자에게 콘텐츠를 빠르게 전달.
- **캐시 무효화**: 최신 빌드 결과가 사용자에게 제공되도록 캐시 초기화.

--- 

### 배포 프로세스
1. GitHub Actions에서 워크플로우를 트리거합니다. (`push` 이벤트 기반)
2. 저장소를 체크아웃합니다.
3. Node.js 18.x 버전을 설정합니다.
4. 프로젝트 의존성을 설치합니다.
5. Next.js 프로젝트를 빌드합니다.
6. AWS 자격 증명을 구성합니다.
7. 빌드된 파일을 S3 버킷에 동기화합니다.
8. CloudFront 캐시를 무효화하여 최신 콘텐츠가 제공되도록 보장합니다.

---

## 주요 링크

- **S3 버킷 웹사이트 엔드포인트**: [http://hyo-hanghae.s3-website-us-east-1.amazonaws.com](http://hyo-hanghae.s3-website-us-east-1.amazonaws.com)
- **CloudFront 배포 도메인 이름**: [https://d3jkj0hl7piyz3.cloudfront.net](https://d3jkj0hl7piyz3.cloudfront.net)

---

## 주요 개념

### GitHub Actions과 CI/CD 도구
- **GitHub Actions**: 코드 푸시 시 자동으로 빌드와 배포를 실행.
- **CI/CD**: 지속적 통합과 지속적 배포로 효율적 개발 파이프라인 구성.

### S3와 스토리지
- **S3**: 정적 웹사이트 호스팅을 위한 AWS의 스토리지 서비스.
- **버킷 동기화**: `aws s3 sync`를 통해 빌드 파일을 S3에 업로드.

### CloudFront와 CDN
- **CloudFront**: S3에서 제공하는 정적 콘텐츠를 글로벌 캐시로 배포.
- **CDN**: 콘텐츠 전송 속도와 사용자 경험을 최적화.

### 캐시 무효화(Cache Invalidation)
- 변경된 파일이 즉시 반영되도록 CloudFront 캐시를 무효화.
- `aws cloudfront create-invalidation --paths "/*"` 명령어로 모든 캐시를 제거.

### Repository Secret과 환경변수
- AWS 액세스 키와 같은 민감한 정보를 GitHub Secrets에 저장.
- `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`를 사용해 Actions에서 안전하게 인증.

---

## 사용한 기술 스택
- Next.js: 최신 프론트엔드 프레임워크
- AWS S3: 정적 파일 저장 및 배포
- AWS CloudFront: CDN 기반 콘텐츠 전송
- GitHub Actions: CI/CD 자동화
- YAML: GitHub Actions 워크플로우 정의

---

