# 신통사주카페 — Firebase 연동 준비 버전

## 포함 내용
- `index.html`: 제공된 Firebase 웹 설정값 반영, Firebase 익명 인증 시도
- `firestore.rules`: 운영 전 개인정보 노출을 방지하기 위한 전면 차단 규칙

## 현재 상태
사이트 HTML과 Firebase 프로젝트 설정값이 연결됩니다. 다만 Firestore는 의도적으로 읽기/쓰기를 차단합니다. **이 파일은 실제 예약 서비스로 사용하면 안 됩니다.**

## 왜 아직 예약이 작동하지 않나요?
- 고객과 어머님이 모두 익명 Firebase 계정이라면 Firestore Rules만으로 '전화번호+관리자 PIN'의 소유자를 안전하게 확인할 수 없습니다.
- `index.html`에 비밀번호 또는 해시를 넣어 확인하는 방식은 누구나 코드를 볼 수 있기 때문에 관리자 권한 보호가 안 됩니다.
- 예약 중복 방지는 서버에서 검증하는 트랜잭션 및 엄격한 보안 규칙이 필요합니다.
- 다른 고객의 전화번호·예약 메모는 공개 데이터와 분리해야 합니다.

## 다음 단계
Cloud Functions 등의 서버에서 관리자 PIN 검증과 권한 부여를 구현하고, 공개 예약 가능 시간 및 비공개 고객 데이터를 분리한 뒤, 인증·예약·동시성에 맞춘 보안 규칙을 배포합니다. Cloud Functions 배포는 일반적으로 Firebase Blaze 요금제가 필요할 수 있습니다.

## 확인 방법
1. Firebase Authentication → Sign-in method → Anonymous 활성화
2. Firebase Firestore Database 생성 (Production mode)
3. `index.html` GitHub Pages 업로드
4. 실제 고객 데이터를 입력하지 않고 Firebase 프로젝트 연결 오류만 점검

보안상 운영 준비 전까지 Firestore 규칙은 전면 차단 상태로 유지하세요.
