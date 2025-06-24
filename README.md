# GAME

Animal Kingdom

게임 장르 : 로그라이크, 뱀파이어서바이벌, 멀티 게임(크로스 플랫폼은 추후 진행 예정)

🎮 게임 시스템 소개
1. 게임 모드 구성
싱글 PVE
개인이 몬스터 웨이브를 상대로 생존하며, 무기 및 스킬 선택을 통해 최대 라운드까지 도달하는 것을 목표로 합니다.

멀티 PVE (Co-op)
Photon 기반 매칭 시스템을 통해 최대 4인이 하나의 전장을 공유하여 생존하는 구조입니다.
유저 간 실시간 동기화는 TimeSlice 시스템으로 구현되어, 위치 및 상태 변화에 대한 불필요한 과부하 없이 부드러운 동기화가 가능합니다.

2. 전투 흐름 및 구조
항목	내용
전투 방식	실시간 자동 전투, 라운드별 몬스터 스폰 기반
전투 FSM 상태 전이	CHASE → ATTACK → DEAD
보스 몬스터 AI	고급 전투 패턴 및 연출은 Behavior Tree(BT) 기반으로 구성
타겟팅 로직	가장 가까운 적, 최근 공격한 적 우선
스킬 발동 조건	- 일정 공격 횟수
- 체력 조건
- 쿨타임
상태 이상 처리	스턴, 슬로우, 회복불가 등 시간 기반 처리
승리/패배 판정	제한 시간 생존 여부 또는 전체 전멸 여부로 판단

✅ 유닛은 직접 조작되지 않으며, FSM 상태 기반으로 자동 전투를 수행합니다.

⚙ 기술 시스템 구성
1. AI 구조
FSM 유닛 AI

CHASE: 적 추적

ATTACK: 공격 가능 시 자동 타격

DEAD: 체력 0 시 사망 상태 진입

보스 AI (BT)

타겟 스위칭, 범위 공격, 패턴 강화 등은 Behavior Tree 기반으로 유연하게 구성

2. 동기화 시스템
TimeSlice 기반 구조 설계

플레이어 상태 및 위치를 일정 주기 단위로 묶어 전송

불필요한 프레임 동기화 제거 → 퍼포먼스 최적화

유닛 FSM 상태/좌표만 전송, 이동/공격은 각 클라이언트에서 예측 및 보간

🧠 데이터 설계 (테이블 기반)
1. CharacterData
필드	설명
ID / Name / Type	고유 캐릭터 정보
HP / ATK / DEF / Range / Speed	기본 전투 스탯
SkillType / AttackSound / SkillSound / DeadSound	전투 사운드 설정
IconSprite	UI 리소스 연결

2. MonsterData
필드	설명
ID / MapID / MonsterType	맵 별 등장 몬스터 정보
HP / ATK / DEF / Speed / SkillType	AI 제어용 전투 데이터
Sound 설정	출현, 공격, 사망 음원 지정

3. MapData
필드	설명
MapID / MapName / Description	맵 정보
BGMSound / EnvType / BackgroundImage	배경 리소스 설정
SpawnMonsterIDs[]	라운드별 등장 몬스터 구성
TimeLimit / RecommendedLevel	라운드 제한 시간 및 권장 레벨

4. RoundData
필드	설명
MapID / Round	라운드 구분
MonsterRatios / SpawnCount	몬스터 비율 및 소환 수량

🧩 기능별 구현 요소
기능	설명
무기 시스템	근거리, 원거리, 범위형 등 무기 타입별 FSM 연동 자동 공격
스킬 시스템	단일 타겟 / 광역 / 버프 등 유형별 쿨타임 & 조건 기반 발동
보스 패턴	Behavior Tree로 다단계 패턴 구성 (ex. 체력 조건, 스턴 연계 등)
라운드 시스템	라운드 기반 웨이브 구조 / 시간제한 전투
전투 HUD	상단 체력/라운드/타이머 / 중앙 데미지 텍스트 및 이펙트
상점 시스템 (예정)	보상 기반 선택형 스킬/아이템/무기 제공 방식
결과창	생존 시간, 몬스터 처치 수, DPS, 플레이어 순위 출력
Firebase 연동	로그인, 유저 프로필, 매치 결과 저장 및 리플레이 준비

🎨 리소스 및 UI 스타일
디자인 스타일: 플랫 2D 기반 (LoL TFT, Survivor.io 참고)

툴 사용:

Midjourney: UI 요소 및 아이콘 레퍼런스 생성

Figma / Adobe XD: UI 설계 및 프로토타이핑

Spine or Unity Animator: 유닛 애니메이션 구성

UI 구조:

HUD: 체력, 라운드, 타이머, 스킬 쿨다운 표시

인게임: 데미지 텍스트, 상태이상 아이콘, 결과창

정보창: 캐릭터 상태, 능력치, 무기 및 스킬 목록

🧰 사용 기술 스택
분류	기술
엔진	Unity 2021.3.8f
멀티플레이	Photon PUN2
데이터 저장	Firebase Firestore
로그인 인증	Firebase Auth, Google OAuth
광고	Google AdMob (보상형 광고, 전면 광고 등)
UI 개발	Unity UI Toolkit + Prefab 기반 구성
FSM/BT	FSM (유닛 AI) + Behavior Tree (보스)
동기화 시스템	TimeSlice 기반 커스텀 네트워크 구조
이펙트	DOTween, 파티클 시스템
리소스 관리	Addressables, ScriptableObject

🧪 개발 플로우 및 일정
단계	내용	상태
Step 1	시장 분석, 장르 방향성 정의	✅ 완료
Step 2	전투 흐름 기획 및 FSM 설계	✅ 완료
Step 3	캐릭터/몬스터/맵/라운드 데이터 시트 작성	✅ 완료
Step 4	FSM 기반 유닛 AI 구현	🛠 진행 중
Step 5	TimeSlice 네트워크 구조 구현	🛠 진행 중
Step 6	UI 프로토타이핑 및 HUD 기능화	예정
Step 7	보스 BT 구조 적용 및 연출 구성	예정
Step 8	광고 및 로그인 연동 / Firebase 테스트	예정
Step 9	테스트, 튜토리얼, 밸런싱 → CBT 버전 출시	예정

🔚 마무리
Survival Showdown은 PvP 요소를 제거하고 오직 싱글/멀티 PVE 구조로 설계된 뱀서류 핵심 생존 게임입니다.
자동 전투, 전략적 무기 선택, 점점 강해지는 웨이브, 그리고 친구들과의 협동이 게임의 핵심 재미 포인트입니다.

앞으로도 아래 기능이 추가될 예정입니다:

📦 스킬 선택 시스템 (레벨업 구조)

🧟‍♀️ 보스 패턴 확장 및 고급 상태 이상

🛠 관리자용 밸런싱 툴 (Google Sheets 연동)

🎥 리플레이 시스템 및 서버 기록






