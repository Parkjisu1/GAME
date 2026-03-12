# Animal Kingdom | 애니멀 킹덤

> 로그라이크 서바이벌 멀티플레이어 게임 — 뱀파이어 서바이버 스타일의 PvE 협동 게임
>
> Roguelike survival multiplayer game — Vampire Survivors style co-op with PvE-focused gameplay.

![Unity](https://img.shields.io/badge/Unity-2021.3-blue?logo=unity)
![Photon](https://img.shields.io/badge/Multiplayer-Photon_PUN2-purple)
![Firebase](https://img.shields.io/badge/Backend-Firebase-orange?logo=firebase)
![Platform](https://img.shields.io/badge/Platform-Android-green?logo=android)

---

## 개요 | Overview

Animal Kingdom은 경쟁 요소 없이 **PvE 중심 협동 플레이**를 제공하는 로그라이크 오토배틀 게임입니다. 최대 4인까지 팀을 이뤄 웨이브 기반 몬스터 전투에서 생존합니다.

Animal Kingdom is a **roguelike auto-battler** featuring cooperative PvE gameplay without competitive elements. Players team up (up to 4 players) to survive wave-based monster encounters with unique character builds and strategies.

### 핵심 기능 | Core Features

| 기능 | 설명 |
|------|------|
| **오토 배틀** | 웨이브 기반 실시간 자동 전투 시스템 |
| **멀티플레이 협동** | Photon PUN2 기반 최대 4인 멀티플레이 |
| **FSM 유닛 AI** | Chase → Attack → Dead 상태 머신 |
| **행동 트리 보스 AI** | 스크립트 기반 복합 보스 패턴 |
| **상태이상 시스템** | 스턴, 슬로우, 회복 차단 등 |
| **무기 시스템** | 근거리, 원거리, 범위 공격 무기 |
| **스킬 시스템** | 쿨다운 기반 스킬 + 선택 메커니즘 |

---

## 기술 아키텍처 | Technical Architecture

### 게임 시스템 | Game Systems

| 시스템 | 구현 방식 |
|--------|-----------|
| **유닛 AI** | Finite State Machine (Idle → Chase → Attack → Dead) |
| **보스 AI** | Behavior Tree — 패턴 시퀀스 기반 |
| **네트워킹** | Photon PUN2 + TimeSlice 동기화 |
| **백엔드** | Firebase Firestore + Authentication |
| **수익화** | Google AdMob (전면, 보상형) |
| **애니메이션** | DOTween + Particle Systems |

### 전투 흐름 | Combat Flow

```
웨이브 스포너 → 몬스터 AI (FSM) → 충돌 감지 → 데미지 계산
                                                    ↓
플레이어 입력 → 스킬 시스템 → 상태이상 → HUD 업데이트 (HP, 데미지 텍스트)
```

- 웨이브별 난이도 스케일링
- 연속 처치 콤보 시스템
- 상태이상 중첩 및 우선순위 처리
- 실시간 데미지 텍스트 및 체력바

### 네트워크 동기화 | Network Sync

- **TimeSlice 기반** 동기화로 부드러운 멀티플레이 경험
- 호스트 권위적 게임 상태 관리
- 보간(Interpolation)과 예측(Prediction)으로 저지연 구현
- Photon 로비 기반 룸 관리

---

## 기술 스택 | Tech Stack

| 구성요소 | 기술 |
|----------|------|
| **엔진** | Unity 2021.3.8f |
| **언어** | C# |
| **멀티플레이** | Photon PUN2 |
| **데이터베이스** | Firebase Firestore |
| **인증** | Firebase Authentication |
| **광고** | Google AdMob |
| **애니메이션** | DOTween Pro |
| **UI** | Unity UI (uGUI) + TextMesh Pro |
| **플랫폼** | Android |

---

## 개발 현황 | Development Status

### 완료 | Completed

- [x] 시장 분석 및 게임 컨셉 설계
- [x] 전투 흐름 시스템 (웨이브 관리)
- [x] 데이터 시트 아키텍처
- [x] FSM 기반 유닛 AI (Chase, Attack, Dead)
- [x] 무기 타입 (근거리, 원거리, 범위)
- [x] 상태이상 시스템 (스턴, 슬로우, 회복 차단)
- [x] HUD (체력바, 라운드 카운터, 타이머, 데미지 텍스트)
- [x] Photon PUN2 멀티플레이어 연동
- [x] Firebase 백엔드 설정

### 진행중 | In Progress

- [ ] 네트워크 동기화 최적화
- [ ] 보스 행동 트리 패턴
- [ ] UI 프로토타이핑 및 폴리싱

### 계획 | Planned

- [ ] 스킬 선택 & 업그레이드 시스템
- [ ] 보스 패턴 확장
- [ ] 밸런싱 도구
- [ ] 리플레이 시스템
- [ ] 캐릭터 성장 & 해금

---

## 아키텍처 패턴 | Architecture Patterns

| 패턴 | 적용 |
|------|------|
| **Singleton** | GameManager, NetworkManager, AudioManager |
| **Observer** | 시스템 간 이벤트 기반 통신 |
| **State Machine** | 유닛 행동 제어 (FSM) |
| **Behavior Tree** | 보스 AI 의사결정 |
| **Object Pool** | 투사체, 이펙트 재활용 |
| **Command** | 입력 처리 및 스킬 실행 |

---

## 시작하기 | Getting Started

### 필수 요구사항

- Unity 2021.3.8f 이상
- Photon PUN2 (Asset Store에서 임포트)
- Firebase Unity SDK
- Google AdMob SDK
- Android SDK

### 설치

1. 저장소 클론
2. Unity에서 프로젝트 열기
3. Photon PUN2 임포트 후 App ID 설정
4. Firebase 프로젝트 설정 후 `google-services.json` 다운로드
5. AdMob 광고 단위 ID 설정
6. Android 빌드

---

## 라이선스 | License

MIT License
