# CMSmosis

중등 수학·과학 개념을 **소리 내어 말하며** 외우는 학습 앱.
간격 반복(SRS) + 말하기 인출 연습 + 게임화를 한 화면에 담았습니다.

## 구성

- `index.html` — 앱 전체 (HTML + CSS + JS 단일 파일, 빌드 불필요)
- `manifest.json`, `icon-*.png` — 홈 화면 추가용 PWA 설정
- 백엔드: Supabase (Postgres + Auth)

## 기능

| 탭 | 내용 |
|---|---|
| 📚 학습 | 단원별 카드, 음성 인식 말하기 연습, SRS 자동 출제, 하단 미니 랭킹 |
| 🏆 랭킹 | 전체 학생 XP 순위 |
| 📅 내 기록 | 연속 학습일·정답률·마스터 카드, 월별 학습 달력 |

## 데이터베이스 테이블

| 테이블 | 역할 |
|---|---|
| `concept_cards` | 개념 카드 (과목·단원·질문·답) |
| `profiles` | 학생 프로필 + 누적 XP |
| `user_card_progress` | 학생별 카드 라이트너 단계 |
| `study_log` | 학습 로그 (달력·정답률 계산용) |

## 로컬 실행

`index.html`을 크롬으로 열면 끝입니다. 별도 서버가 필요 없습니다.
음성 인식은 크롬 계열 브라우저에서만 동작합니다.

## 배포

Vercel에 이 폴더를 연결하면 됩니다. 프레임워크 프리셋은 **Other**,
빌드 명령과 출력 디렉터리는 비워두세요 (정적 파일 그대로 서빙).

## 설정 바꾸기

`index.html` 안 "설정값" 블록에서 조절합니다.

```js
const XP_PER_CORRECT = 10;   // 정답 1개당 XP
const DAILY_GOAL     = 20;   // 하루 목표 카드 수
const XP_PER_LEVEL   = 100;  // 레벨당 필요 XP
const STAGE_INTERVAL_DAYS = { 1: 0, 2: 2, 3: 7, 4: 14, 5: 30 };  // 복습 간격(일)
```

## 참고

`SUPABASE_KEY`는 publishable key로, 브라우저에 노출되어도 되는 값입니다.
실제 데이터 보호는 Supabase의 RLS 정책이 담당합니다.
secret key는 절대 이 파일에 넣지 마세요.
