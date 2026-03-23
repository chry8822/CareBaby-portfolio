# 👶 CareBaby — AI 기반 육아 기록 앱

> 수유·수면·기저귀 기록부터 AI 패턴 분석, 성장곡선 추적, 프리미엄 주간 리포트까지  
> 육아의 모든 순간을 스마트하게 기록하세요.

<br/>

## 📱 스크린샷

<br/>

## ✨ 주요 기능 (결제 / 프리미엄 관련 내용은 임시입니다.)

| 기능 | 설명 |
|------|------|
| ⚡ 빠른 기록 | 홈 화면 FAB에서 수유·수면·기저귀·이유식·체온·약·병원·성장기록 원터치 입력 |
| 🕐 타이머 | 수유·수면 타이머 (백그라운드 복귀 시 자동 재계산), 경과시간 초단위 롤링 애니메이션 |
| 🤖 AI 인사이트 | AAP 기준 수면 부족 감지, 수유 간격 변화율, 다음 수유 예측, 기저귀 패턴 알림 |
| 📊 통계 대시보드 | 7일/14일 바 차트, 수유·수면·기저귀 카테고리별 요약, 24시간 활동 흐름 시각화 |
| 📈 성장곡선 | WHO 0~60개월 P3·P50·P97 기준선 + 드래그 스크러버 + 선 그리기 애니메이션 |
| 🔄 실시간 동기화 | Supabase Realtime 기반 공동 양육자 실시간 데이터 공유 (목표 2초 이내) |
| 👪 다중 아기 | 여러 아기 프로필 전환 + 초대 코드 기반 공동 양육자 연결 |
| 🌙 타임라인 | 시간순 기록 타임라인, 완료시간 범위 표시 (14:00 ~ 15:00), 스와이프 삭제·복사 |
| 💎 프리미엄 | RevenueCat 구독 + 주간 리포트 + AdMob 배너 (프리미엄 사용자 자동 숨김) |

<br/>

## 🛠 기술 스택

```
Frontend     React Native 0.81 · Expo SDK 54 · TypeScript Strict
라우팅        Expo Router v6 (파일 기반 라우팅)
상태관리      Zustand · MMKV (네이티브 캐싱) · AsyncStorage (폴백)
Backend      Supabase (PostgreSQL · Realtime · RLS · Edge Functions)
결제          RevenueCat (구독 관리)
광고          react-native-google-mobile-ads (AdMob)
UI            lucide-react-native · react-native-svg · lottie-react-native
공유          react-native-view-shot · expo-sharing
```

<br/>

## 🏗 아키텍처

```
app/
├── (auth)/              로그인·회원가입
├── (tabs)/              홈·통계·건강·기록·설정
│   ├── index.tsx        홈 대시보드 (타이머 카드·AI 인사이트·타임라인)
│   ├── stats.tsx        통계 화면 (바 차트·활동 흐름·AI 섹션·프리미엄 리포트)
│   ├── health.tsx       건강·성장 기록 탭
│   ├── record.tsx       기록 입력 탭 (수유·수면·기저귀·이유식)
│   └── settings.tsx     설정·아기 관리·공동 양육자·구독
├── baby-setup.tsx       아기 등록·수정
└── growth-detail.tsx    성장 상세 (차트·기록 리스트)

components/
├── home/                홈 (TimerCardList · TimelineList · InsightCard · QuickCardManager)
├── stats/               통계 (BarChart · StatSummaryCard · ActivityFlowBar · WeeklyReport)
├── health/              건강 (GrowthChart · GrowthRecordForm · TemperatureForm ...)
├── records/             기록 폼 (FeedingForm · SleepForm · DiaperForm · MealForm)
└── ui/                  공통 UI (BottomSheet · WheelTimePicker · RulerInput · SwipeableRow · Toast)

features/premium/        RevenueCat 구독 · AdMob · 주간 리포트 (독립 피처 모듈)
stores/                  Zustand 스토어 (auth · baby · record · health · growth · insight · purchase · ui)
lib/
├── insightEngine.ts     AI 인사이트 로직
└── supabase.ts          Supabase 클라이언트
```

<br/>

## 🤖 AI 인사이트 상세

AAP(미국소아과학회) 2017 가이드라인 기반 로컬 통계 엔진:

| 인사이트 | 로직 |
|---------|------|
| 수면 부족 감지 | 월령별 권장 수면과 최근 7일 평균 비교 |
| 수유 간격 변화 | 14일 전반/후반 수유 간격 변화율 (15% 이상 시 알림) |
| 다음 수유 예측 | 최근 3일 패턴 기반 다음 수유 시각 예측 |
| 기저귀 패턴 알림 | 최근 3일 횟수가 7일 평균 대비 30% 이상 감소 시 경고 |
| 주간 요약 | 수유·수면·기저귀·이유식 일평균 자동 요약 |

<br/>

## 📈 성장 기록 & 차트

- **WHO 0~60개월** 체중·키·머리둘레 P3·P50·P97 기준선 데이터 내장
- **드래그 스크러버**: 좌우 드래그로 개월별 수치 탐색, 데이터 포인트 툴팁
- **선 그리기 애니메이션**: requestAnimationFrame + SVG ClipPath 마스킹
- **세그먼트 네비게이션**: 0-12 · 12-24 · 24-36 · 36-48 · 48-60개월 탭 전환
- **최신 포인트 pulse** 루프 애니메이션 + 또래 백분위 뱃지

<br/>

## 💎 프리미엄 기능

| 기능 | 구현 |
|------|------|
| RevenueCat 구독 | `purchaseStore` + `usePremium` 훅, `DEV_FORCE_PREMIUM` 플래그로 개발 환경 전체 활성화 |
| 구독 시트 | 플랜 카드·구매·복원 버튼, 설정 화면 "구독 & 결제" 섹션 연동 |
| 주간 리포트 | 기간 변화 추이·수유 시간대 분포·수면 분석·베스트 섹션 + 이미지 공유 |
| AdMob 배너 | 홈 하단 배너, 프리미엄 사용자 자동 숨김, Expo Go 동적 로드 호환 |

<br/>

## 🎬 인터랙션 & 애니메이션

| 항목 | 설명 |
|------|------|
| 타이머 숫자 롤링 | 매초 위→아래 fade-slide (10분 미만 초단위, useNativeDriver) |
| FAB 펄스 | 우하단 FAB 주기적 ripple 링 (scale·opacity loop) |
| 타임라인 슬라이드인 | 저장 후 항목 우→좌 슬라이드 등장 |
| 탭바 아이콘 바운스 | 탭 전환 시 위로 살짝 bounce |
| 빈 화면 플로팅 | 이미지 페이드인 + 위아래 floating loop |
| 성장곡선 선 그리기 | rAF + SVG ClipPath 마스킹 |
| 바 차트 spring | 데이터 확정 후 scaleY spring 애니메이션 |
| 빠른기록 탭 scale | 카테고리 탭 선택 시 scale 애니메이션 + 햅틱 |
| 카드 순서 변경 | 길게 눌러 탭 위치 교환 + breathing 애니메이션 |

<br/>

## 🔒 오프라인 & 동기화

- 네트워크 없을 때 `pendingSync` 큐에 저장 (AsyncStorage/MMKV 영속화)
- 앱 시작 시 미동기화 기록 자동 일괄 업로드
- Supabase Realtime 채널 구독으로 다중 기기 2초 이내 동기화
- `TOKEN_REFRESH_FAILED` 후 자동 로그아웃 방지 플래그 처리

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
