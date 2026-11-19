# 오늘의 타로 디자인 가이드

모바일에서 로그인 없이 카드 한 장을 뽑고, 1분 안에 자신에게 맞춘 짧은 해석을 읽는 경험을 설계한다. 레퍼런스의 넓은 여백, 낮은 대비의 표면 구분, 이미지 중심 구성을 가져오고, 따뜻한 종이색과 잉크 자주색으로 타로 카드가 중심이 되는 화면을 만든다.

## 색과 표면

| 역할 | 토큰 | 값 | 사용 |
|---|---|---|---|
| 페이지 | `background` | `#FAF8F4` | 전체 배경 |
| 본문 | `foreground` | `#241D29` | 제목과 본문 |
| 카드 | `card` / `card-foreground` | `#FFFFFF` / `#241D29` | 결과와 안내 패널 |
| 주요 행동 | `primary` / `primary-foreground` | `#512A68` / `#FFFFFF` | 시작·뽑기·결과 공유 |
| 주요 행동 호버 | `primary-hover` | `#402052` | 호버 및 눌림 배경 |
| 보조 표면 | `muted` / `muted-foreground` | `#F1EDE8` / `#625766` | 안내, 보조 설명 및 비활성 상태 |
| 선택 | `accent` / `accent-foreground` | `#EFE5F5` / `#512A68` | 선택된 주제 |
| 구분선 | `border` | `#DDD5DE` | 카드 테두리와 구분선 |
| 입력 경계 | `input` | `#897D8C` | 입력과 미선택 주제 경계 |
| 키보드 포커스 | `ring` | `#713E8C` | 2px 외곽선, 2px 오프셋 |
| 오류 | `destructive` | `#A12542` | 오류 문구 및 입력 경계 |

페이지와 카드, 카드와 안내 표면은 배경과 1px 경계로 구분한다. 그림자는 사용하지 않는다. 금색은 카드 아트의 세부 장식에만 쓴다. 개인정보 안내와 오락용 안내는 `muted-foreground`를 사용하고 사용자에게 보이는 텍스트로 제공한다.

## 글씨, 간격, 모서리

| 역할 | 크기 / 줄높이 | 굵기 | 적용 |
|---|---|---|---|
| 시작 제목 | 40 / 48px, 넓은 화면 52 / 60px | 700 | S-01 제목 |
| 화면 제목 | 28 / 36px | 700 | 정보 입력 및 결과 제목 |
| 카드 이름 | 22 / 30px | 700 | 카드 번호와 이름 |
| 본문 및 입력 | 16 / 24px | 400 | 설명, 해석, 입력값 |
| 버튼 및 라벨 | 14 / 20px | 600 | 버튼, 필드, 주제 |
| 보조 및 안내 | 14 / 20px | 400 | 개인정보, 오류, 오락용 안내 |

본문은 Pretendard, Noto Sans KR, 시스템 산세리프 순으로 적용한다. 시작 제목과 카드 이름에는 사용 가능한 경우 Noto Serif KR을 적용한다. 한글 제목 자간은 최대 `-0.025em`로 좁히고 본문은 기본 자간을 사용한다.

4px 단위로 간격을 구성한다. 아이콘 옆 8px, 라벨과 필드 사이 8px, 주제 칩 사이 8px, 필드 간 16px, 카드 내부 20px(넓은 화면 28px), 화면 내 주요 그룹 간 24–32px를 사용한다. 화면은 너비 480px 안에서 가운데 정렬하고, 좌우 20px 여백을 기본으로 둔다. 320px 폭에서는 좌우 16px, 넓은 화면에서는 24px를 적용한다. 각 페이지는 화면 높이에 맞춰 잘라내지 않고 세로 스크롤을 허용한다.

버튼은 완전한 알약형, 입력과 주제 칩은 12px, 카드 아트 프레임은 16px, 결과 카드와 미리보기 패널은 28px로 맞춘다. 모든 탭 대상은 최소 44×44px로 두고 주요 버튼은 높이 48px 이상으로 둔다.

## 컴포넌트 규칙

| 요소 | shadcn 구성 | 표현과 동작 |
|---|---|---|
| 주요 버튼 | `Button` 기본 | 시작·뽑기는 전체 너비. 결과에서는 공유를 주요 행동으로 두고 저장은 테두리형으로 둔다. |
| 보조 버튼 | `Button` `outline`, `ghost` | 이미지 저장은 흰 바탕과 입력 경계. 다시 뽑기·처음으로·뒤로는 고스트. 아이콘만 있을 경우 접근 가능한 이름을 제공한다. |
| 입력 | `FieldGroup` → `Field` · `FieldLabel` · `Input` · `FieldDescription` / `FieldError` | 모든 라벨을 입력 위에 노출한다. 오류는 해당 필드 아래에 표시하고 `data-invalid`, `aria-invalid`, `aria-describedby`를 연결한다. |
| 주제 | 단일 선택 `ToggleGroup` · `ToggleGroupItem` | 커리어·재물·연애·건강·학업·종합 순서로 배치한다. 기본 3열 2행, 확대 시 2열 또는 1열로 줄인다. 선택 상태는 배경·테두리·체크 표시와 컴포넌트의 접근성 상태로 드러낸다. 마지막 선택을 다시 누르면 선택을 유지한다. |
| 결과 카드 | `Card`, `CardHeader`, `CardTitle`, `CardDescription`, `CardContent`, `CardFooter` | 제목과 주제 → 그림 → 카드 이름과 별자리 → 해석 → 오락용 안내와 서비스 이름. 저장·공유 버튼은 카드 바깥에 둔다. |
| 개인정보 안내 | `Alert` / `AlertDescription` | 잠금 아이콘은 장식으로 처리하고 안내 전문을 펼쳐 둔다. 입력 폼 아래와 결과 행동 아래에 배치한다. |
| 대체 미리보기 | `Dialog` + `DialogTitle` | 이미지나 선택 가능한 공유 글을 표시한다. 닫으면 원래 버튼으로 포커스를 돌린다. |
| 진행과 피드백 | `Spinner`, `Skeleton`, 접근 가능한 토스트 | 처리 중에는 버튼 라벨을 유지하고 스피너와 함께 비활성화한다. 성공 알림은 `role="status"`로 한 번 알린다. 수동 저장·복사 안내는 화면에 유지한다. |

호버 변경은 포인터가 있는 환경에서 적용한다. 포커스 표시는 호버 및 선택 상태 위에서도 보이게 한다. 비활성 버튼은 연한 중립 배경과 보조 텍스트를 사용하며, S-02에서는 활성화에 필요한 조건도 버튼 가까이에 표시한다. 버튼의 상태별 스타일은 공통 variant에서 정의하고 화면에서는 배치와 너비를 지정한다.

## 화면별 구성

### S-01 시작 · F-1

- `오늘의 타로` → 카드 뒷면 → 한 장 뽑기 설명 → `타로 시작` → 오락용·정보 미보관 안내 순서로 구성한다.
- 카드 뒷면은 세로 2:3, 너비 160–208px로 중앙에 배치한다. 직접 제작했거나 사용 범위가 확인된 카드 아트를 사용한다.
- 시작 버튼으로 이동하면 S-02의 제목에 포커스를 두고 정보를 입력할 수 있게 한다. 공유 링크도 이 화면으로 연결한다.

### S-02 내 정보와 주제 · F-2~F-3

- 이름은 필수, 닉네임 가능, 최대 10자다. 생년월일은 필수이며 실제 날짜를 받는다. 전공은 선택이라고 라벨에 쓴다.
- 주제 선택 뒤 개인정보 안내를 표시한다. “입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요.”
- 이름·유효한 생년월일·주제가 갖춰졌을 때 `카드 한 장 뽑기`를 활성화한다. 잘못된 날짜에는 “날짜를 다시 확인해 주세요”를 표시한다.
- 메이저 아르카나 22장 중 정방향 한 장을 뽑는다. 연속 탭을 막고, 기본 뒤집기는 450ms에 끝내며 최대 1초를 넘기지 않는다. `prefers-reduced-motion`에서는 즉시 앞면으로 전환한다. 결과가 나오면 결과 제목으로 포커스를 옮긴다.

### S-03 맞춤 해석 결과 · F-4~F-7

- `{이름}님의 타로 · {주제}` 아래에 카드 그림을 보여 준다. 카드 번호·이름, 별자리, 해석을 순서대로 읽을 수 있게 한다.
- 해석은 카드×주제 기본 문장, 별자리 문장, 전공 계열 문장 순으로 최대 3문장·90자다. 전공이 없거나 분류할 수 없으면 마지막 문장을 생략한다. 좁은 화면과 글자 확대에서도 전체 문장을 읽을 수 있도록 자연 줄바꿈을 허용한다. 건강·재물 문구는 돌아볼 관점으로 쓴다.
- 카드 하단에 “※ 오락용 타로 해석입니다”를 표시한다. 행동 영역에는 “저장 이미지와 공유 결과에 이름이 들어가요”를 표시한다. `이미지 저장`과 `결과 공유`를 같은 줄에 두고, 폭이 부족하면 세로로 쌓는다.
- `다시 뽑기`는 입력값을 유지하고 S-02의 주제 선택으로 돌려보낸다. `처음으로`는 입력값과 결과를 지우고 S-01로 이동한다. 결과 화면에도 S-02의 개인정보 안내 전문을 표시한다.

## 이미지 저장과 공유

- PNG는 1080×1350으로 내보낸다. 결과 카드와 같은 순서와 색상을 적용하고 72px 안쪽 여백을 둔다. 제목·주제, 카드 그림·이름, 별자리, 해석, 오락용 안내 및 서비스 이름만 담는다. 10자 이름과 90자 해석을 넣어 잘림이 없는지 확인한다.
- 공유 화면은 기기 공유 메뉴에서 이미지와 글을 전달한다. 글에는 이름·주제·카드 이름·별자리·해석·오락용 안내·시작 링크가 포함된다. PNG 및 공유 글에 생년월일이나 전공 원문을 보내지 않고 시작 링크에는 개인 정보나 결과 값을 붙이지 않는다.
- 저장 성공은 “이미지를 저장했어요”로 알린다. 다운로드를 지원하지 않으면 이미지를 열고 “이미지를 길게 눌러 저장해 주세요”를 표시한다. 공유 메뉴가 없으면 글을 자동으로 복사하고, 성공 시 “결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요”를 표시한다. 복사가 실패하면 글을 보여 주고 “아래 글을 길게 눌러 복사해 주세요”라고 안내한다. 공유를 끝내거나 취소하면 결과 화면으로 돌아온다.
- 입력값 및 결과의 원본 데이터는 화면 메모리에서만 다룬다. 탭 닫기, 새로 고침, 처음으로에서 초기화한다. 서버·분석 도구로 전송하거나 브라우저 저장소에 기록하지 않는다. 사용자가 직접 선택한 저장·공유 동작에는 위의 공개용 데이터만 전달한다.

## Tailwind CSS v4 및 shadcn 적용 예시

`:root`의 의미 토큰을 단일 기준으로 유지하고 `@theme inline`으로 유틸리티와 연결한다. 이 서비스의 기본 테마는 밝은 색상이다. 초기 구현 시 실제 프로젝트의 shadcn 설정에 맞춰 아이콘과 프리미티브를 선택한다.

```css
@import "tailwindcss";

:root {
  --background: #faf8f4;
  --foreground: #241d29;
  --card: #ffffff;
  --card-foreground: var(--foreground);
  --popover: var(--card);
  --popover-foreground: var(--card-foreground);
  --primary: #512a68;
  --primary-foreground: #ffffff;
  --primary-hover: #402052;
  --muted: #f1ede8;
  --muted-foreground: #625766;
  --secondary: var(--muted);
  --secondary-foreground: var(--foreground);
  --accent: #efe5f5;
  --accent-foreground: var(--primary);
  --border: #ddd5de;
  --input: #897d8c;
  --ring: #713e8c;
  --destructive: #a12542;
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-primary-hover: var(--primary-hover);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-destructive: var(--destructive);
  --font-sans: Pretendard, "Noto Sans KR", system-ui, sans-serif;
  --font-serif: "Noto Serif KR", Georgia, serif;
  --spacing: 0.25rem;
  --radius-field: 0.75rem;
  --radius-art: 1rem;
  --radius-card: 1.75rem;
  --text-taro-title: 1.75rem;
  --text-taro-title--line-height: 2.25rem;
  --text-taro-display: 2.5rem;
  --text-taro-display--line-height: 3rem;
  --text-taro-display-wide: 3.25rem;
  --text-taro-display-wide--line-height: 3.75rem;
}
```

버튼 variant는 `bg-primary text-primary-foreground hover:bg-primary-hover`, 필드는 `rounded-field border-input`, 카드에는 `rounded-card bg-card text-card-foreground`를 사용한다. 공통 포커스는 `focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-ring`으로 맞춘다. 화면 레이아웃은 `gap-*`으로 간격을 잡고, 처리 중인 버튼에는 `Spinner`를 넣는다.

## 구현 검수 기준

- 320px와 480px 화면 및 200% 글자 확대에서 입력, 결과 전문, 모든 버튼에 가로 스크롤 없이 접근할 수 있다.
- 키보드로 주제 선택, 뽑기, 저장, 공유 및 미리보기 닫기가 가능하다. 장식용 카드 뒷면은 빈 대체 텍스트를 사용한다. 결과 카드 그림은 인접한 카드 이름과 중복되는 낭독을 피한다.
- 일반 텍스트는 배경과 4.5:1 이상, 입력 경계와 포커스 표시는 인접 표면과 3:1 이상을 유지한다.
- 빈 입력, 날짜 오류, 미선택 주제, 전공 생략, 동작 축소, 공유 취소, 다운로드·복사 실패, 상태 초기화를 확인한다.
- 결과 이미지는 고정 크기 PNG에서 해석과 안내가 잘리지 않으며, 이미지와 공유 글에는 지정된 필드만 포함된다.

## 기획 근거

- [TARO_01 PRD](TARO_01_PRD.md) · 제품 목표, 범위, 개인정보 및 오락용 원칙
- [TARO_02 기능명세서](TARO_02_기능명세서.md) · 입력 검증, 해석 조합, 저장·공유 분기
- [TARO_03 유저플로우](TARO_03_유저플로우.md) · S-01부터 S-03까지의 전환과 복귀
- [TARO_04 와이어프레임](TARO_04_와이어프레임.md) · 정보의 순서, 안내 문구, 이미지와 공유 글
