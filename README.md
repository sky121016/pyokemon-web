# 🎫 PYOKEMON User Web

**Team O2** | LG CNS AM INSPIRE CAMP 2기 1조

> **더 공정하게, 더 투명하게**  
> **DID 기반 모바일 티켓 플랫폼**

<br/>

## 📖 프로젝트 소개

**PYOKEMON**(표켓몬)은 암표 차단을 위한 **DID(Decentralized Identifier) 기반** 공연 예매 및 입장 관리 플랫폼입니다.

현재 공연 예매 시장에서 발생하는 매크로/암표 문제를 해결하고, 공정하고 안전한 티켓 거래 환경을 만드는 것을 목표로 합니다. <br/>

### 🚨 기존 시장의 문제점

| 문제 | 설명 |
|------|------|
| ⚙️ **기술적 취약점** | 매크로의 티켓 선점으로 인한 예매 불균형 |
| ⚖️ **제도적 공백** | 암표 규제 및 판매자 책임 부재 → 제도적 보호 장치 미흡 |
| 🧩 **구조적 한계** | 위조 티켓 및 불법 양도 방지의 어려움 |

<br/>

### 🌟 핵심 목표

- **공정성 확보**: 암표 및 불법 거래 차단
- **편의성 향상**: 모바일 앱 기반의 간편한 검표
- **신뢰성 제고**: 위변조 불가능한 DID 기반 인증


<br/>

## 🎯 User Web의 주요 기능

이 레포지토리는 **PYOKEMON 사용자 웹 애플리케이션**으로, 다음 기능을 제공합니다:

- 🔍 **공연 조회**: 장르별, 날짜별 공연 검색 및 필터링
- 🎟️ **공연 예매**: 좌석 선택 및 결제 (토스페이먼츠 연동)
- 📱 **마이페이지**: 예매 내역 조회 및 티켓 관리
- 🔔 **알림**: 공연 시작 알림 및 예매 상태 변경 알림
- 🔐 **DID 인증**: 본인 인증 기반 안전한 예매

<br/>

## 🛠️ Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Framework** | React | UI 라이브러리 |
| **Language** | TypeScript | 타입 안정성 |
| **Build Tool** | Vite | 빠른 개발 서버 & 번들링 |
| **State Management** | Zustand, React Query | 클라이언트/서버 상태 분리 |
| **Routing** | React Router | 페이지 라우팅 |
| **Styling** | Tailwind CSS | 디자인 시스템 |
| **Form** | React Hook Form + Zod | 폼 관리 및 검증 |
| **Payment** | 토스페이먼츠 SDK | 결제 연동 |
| **Code Quality** | ESLint, Prettier | 린트 & 포맷팅 |


<br/>

## 📁 프로젝트 구조

```
pyokemon-web/
├── .github/              # GitHub Actions 워크플로우
├── src/
│   ├── api/              # API 레이어
│   │   ├── client/       # Axios 클라이언트
│   │   ├── event/        # 이벤트 API
│   │   │   ├── fetchers/ # 순수 API 호출 레이어
│   │   │   └── queries/  # React Query 데이터 캐싱 레이어
│   │   ├── booking/      # 예매 API
│   │   └── ...
│   ├── components/       # 재사용 가능한 컴포넌트들
│   │   ├── ui/           # 공통 컴포넌트
│   │   ├── event-preview-card/
│   │   └── ...
│   ├── hooks/            # 커스텀 훅
│   ├── pages/            # 페이지
│   │   ├── home/
│   │   │   ├── _component/    # 해당 페이지에서만 쓰이는 컴포넌트
│   │   │   └── home-page.tsx  # 페이지 컴포넌트
│   │   ├── event-detail/
│   │   └── ...
│   ├── store/            # 전역 상태 관리 (Zustand)
│   ├── types/            # 타입 정의
│   ├── utils/            # 유틸리티 함수
│   └── constants/        # 상수 정의
├── eslint.config.mjs     # ESLint 설정
├── vite.config.ts        # Vite 설정
├── vitest.setup.ts       # Vitest 설정
└── package.json
```

<br/>

## 👤 담당 역할

- **메인 페이지 컴포넌트**: 홈 화면 공연 리스트, 이벤트 카드 UI 구성 및 재사용 컴포넌트 설계

- **공연 상세 조회 페이지**: React Query와 fetcher/queries 구조 활용한 공연 상세 데이터 관리

- **알림창**: 무한 스크롤 훅 적용, 알림 목록 UI 구현

- **마이페이지**: 예매 내역 조회 및 티켓 관리 기능 구현

- **공통 컴포넌트**: 버튼, 로딩중/에러 페이지 등 공통 컴포넌트 설계, Props 기반 확장성 확보

- **리프레시 토큰**: Access Token 만료 시 자동 갱신 로직 구현, 401 중복 요청 방지 큐 관리

<br/>

## 📁 주요 파일/폴더

- **src/api/client/base-client.ts (12~95라인)** <br/>
Access Token 만료로 서비스 흐름이 끊기는 문제와 동시에 여러 401 요청 발생 시 중복 refresh 호출 문제를 해결하기 위해, 자동으로 Refresh Token을 발급받아 요청을 재시도하고 큐 관리로 중복을 방지한 인증 모듈입니다.

- **src/api/event/fetchers/ & queries/ 폴더** <br/>
API 호출과 데이터 캐싱/상태관리를 역할별로 폴더 단위로 분리해, 코드 재사용성과 테스트 용이성을 높이고, 반복 API 호출로 인한 로딩 지연과 관리 복잡성을 줄인 서버 상태 관리 구조입니다.

- **src/hooks/useInfiniteScrollQuery.ts** <br/>
스크롤 이벤트 리스너 사용 시 발생하는 성능 저하와 중복 코드 문제를 해결하기 위해 Intersection Observer를 활용해 재사용 가능한 무한 스크롤 훅을 구현했습니다. src/components/notification/notification-modal.tsx에서는 React Query의 useInfiniteQuery로 이 훅을 적용한 예시입니다.

- **src/components/event-preview-card/event-preview-card.tsx** <br/>
EventType을 활용해 홈, 검색, 관심 공연 등 여러 페이지에서 반복되는 공연 카드 UI를 Props 기반으로 재사용 가능하게 설계하여 코드 중복을 방지하고 UI 일관성을 유지한 컴포넌트입니다.

<br/>

## 🔗 관련 레포지토리

- **Admin App**: [pyokemon-mobile-admin](https://github.com/sky121016/pyokemon-mobile-admin) - 관리자 모바일 앱 (React Native)
- **Backend**: [pyokemon-backend](https://github.com/sky121016/pyokemon-service) - MSA 백엔드 서비스
