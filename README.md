# 👶 CareBaby — AI 기반 육아 기록 앱

> 수유·수면·기저귀 기록부터 AI 패턴 분석까지, 육아의 모든 순간을 스마트하게 기록하세요.

<br/>

## 📱 스크린샷

<!-- 스크린샷 추가 예정 -->

<br/>

## ✨ 주요 기능

| 기능 | 설명 |
|---|---|
| 📊 AI 인사이트 | 수면 부족 감지, 수유 간격 변화, 다음 수유 예측 등 로컬 통계 기반 AI 분석 |
| ⚡ 빠른 기록 | 홈 화면에서 수유·수면·기저귀·이유식 원터치 기록 |
| 🔄 실시간 동기화 | 공동 양육자와 Supabase Realtime 기반 실시간 데이터 공유 |
| 📈 통계 대시보드 | 7일/14일 기간별 바 차트 + 평균/최대값 시각화 |
| 👨‍👩‍👧 다중 아기 지원 | 여러 아기 프로필 전환 및 초대 코드 기반 공동 양육자 연결 |
| 🌙 타임라인 | 시간순 기록 타임라인, 스와이프 삭제, 상대 시간 표시 |

<br/>

## 🛠 기술 스택

```
Frontend   React Native 0.81 · Expo SDK 54 · TypeScript
상태관리    Zustand · MMKV (캐싱)
Backend    Supabase (PostgreSQL · Realtime · RLS · Edge Functions)
UI         lucide-react-native · react-native-svg · lottie-react-native
```

<br/>

## 🏗 아키텍처

```
app/                   Expo Router 기반 파일 라우팅
├── (auth)/            로그인·회원가입
├── (tabs)/            홈·통계·설정 탭
│   ├── index.tsx      홈 대시보드
│   ├── stats.tsx      통계 화면
│   └── settings.tsx   설정·아기 관리
├── baby-setup.tsx     아기 등록·수정
components/
├── home/              홈 화면 컴포넌트 (InsightCard, TimerCardList, TimelineList...)
├── stats/             통계 컴포넌트 (BarChart, StatSummaryCard...)
├── records/           기록 입력 폼
└── ui/                공통 UI (BottomSheet, RichText, SliderInput...)
stores/                Zustand 스토어 (auth, baby, record, insight, ui)
lib/
├── insightEngine.ts   AI 인사이트 로직 (AAP 기준 수면 권장량 등)
└── supabase.ts        Supabase 클라이언트
```

<br/>

## 🤖 AI 인사이트 상세

AAP(미국소아과학회) 2017 가이드라인 기반 로컬 통계 엔진:

- **수면 부족 감지** — 월령별 권장 수면 시간과 최근 7일 평균 비교
- **수유 간격 변화** — 14일 전반/후반 수유 간격 변화율 감지 (15% 이상 시 알림)
- **다음 수유 예측** — 최근 3일 패턴 기반 다음 수유 시각 예측
- **기저귀 패턴 알림** — 최근 3일 횟수가 7일 평균 대비 30% 이상 감소 시 경고
- **주간 요약** — 수유·수면·기저귀·이유식 일평균 자동 요약

<br/>

## 📦 개발 환경 설정

```bash
git clone https://github.com/chry8822/CareBaby.git
cd CareBaby
npm install

# .env 파일 생성
cp .env.example .env
# EXPO_PUBLIC_SUPABASE_URL, EXPO_PUBLIC_SUPABASE_ANON_KEY 입력

npx expo start
```

<br/>

## 📄 라이선스

Copyright © 2026 CareBaby. All rights reserved.  
본 프로젝트의 소스코드는 사전 허가 없이 상업적으로 사용할 수 없습니다.
