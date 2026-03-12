# Animal Kingdom

> Roguelike survival multiplayer game — Vampire Survivors style co-op with PvE-focused gameplay.

![Unity](https://img.shields.io/badge/Unity-2021.3-blue?logo=unity)
![Photon](https://img.shields.io/badge/Multiplayer-Photon_PUN2-purple)
![Firebase](https://img.shields.io/badge/Backend-Firebase-orange?logo=firebase)
![Platform](https://img.shields.io/badge/Platform-Android-green?logo=android)

---

## Overview

Animal Kingdom is a **roguelike auto-battler** featuring cooperative PvE gameplay without competitive elements. Players team up (up to 4 players) to survive wave-based monster encounters with unique character builds and strategies.

### Core Features

- **Auto-Battle System** — Real-time combat with wave-based monster spawning
- **Multiplayer Co-op** — Up to 4 players via Photon PUN2 networking
- **FSM Unit AI** — Chase → Attack → Dead state machine for all units
- **Behavior Tree Boss AI** — Complex boss patterns with scripted behaviors
- **Status Effects** — Stun, slow, healing prevention, and more
- **Weapon System** — Melee, ranged, and area-of-effect weapon types
- **Skill System** — Cooldown-based abilities with selection mechanics

---

## Technical Architecture

### Game Systems

| System | Implementation |
|--------|---------------|
| **Unit AI** | Finite State Machine (Idle → Chase → Attack → Dead) |
| **Boss AI** | Behavior Tree with pattern sequences |
| **Networking** | Photon PUN2 with TimeSlice synchronization |
| **Backend** | Firebase Firestore + Authentication |
| **Monetization** | Google AdMob (interstitial, rewarded) |
| **Animation** | DOTween + Particle Systems |

### Network Synchronization

- **TimeSlice-based sync** for smooth multiplayer experience
- Host-authoritative game state
- Interpolation and prediction for low-latency feel
- Room management with Photon lobby system

### Combat System

```
Wave Spawner → Monster AI (FSM) → Collision Detection → Damage Calculation
                                                              ↓
Player Input → Skill System → Status Effects → HUD Update (HP, Damage Text)
```

- Wave-based difficulty scaling
- Combo system for consecutive kills
- Status effect stacking and priority
- Real-time damage text and health bar updates

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| **Engine** | Unity 2021.3.8f |
| **Language** | C# |
| **Multiplayer** | Photon PUN2 |
| **Database** | Firebase Firestore |
| **Auth** | Firebase Authentication |
| **Ads** | Google AdMob |
| **Animation** | DOTween Pro |
| **UI** | Unity UI (uGUI) + TextMesh Pro |
| **Platform** | Android (primary) |

---

## Game Features

### Implemented

- [x] Market analysis & game concept design
- [x] Battle flow system with wave management
- [x] Data sheet architecture
- [x] FSM-based unit AI (Chase, Attack, Dead states)
- [x] Weapon types (melee, ranged, AoE)
- [x] Status effect system (stun, slow, heal block)
- [x] HUD (health bars, round counter, timer, damage text)
- [x] Photon PUN2 multiplayer integration
- [x] Firebase backend setup

### In Progress

- [ ] Network synchronization optimization
- [ ] Boss Behavior Tree patterns
- [ ] UI prototyping and polish
- [ ] Firebase integration for player data

### Planned

- [ ] Skill selection & upgrade system
- [ ] Expanded boss pattern library
- [ ] Admin balancing tools
- [ ] Replay system
- [ ] Character progression & unlocks

---

## Architecture Patterns

- **Singleton** — GameManager, NetworkManager, AudioManager
- **Observer** — Event-based communication between systems
- **State Machine** — Unit behavior control (FSM)
- **Behavior Tree** — Boss AI decision making
- **Object Pool** — Projectile and effect recycling
- **Command** — Input handling and skill execution

---

## Getting Started

### Prerequisites

- Unity 2021.3.8f or later
- Photon PUN2 (import from Asset Store)
- Firebase Unity SDK
- Google AdMob SDK
- Android SDK (for mobile builds)

### Setup

1. Clone the repository
2. Open the project in Unity
3. Import Photon PUN2 and configure App ID
4. Set up Firebase project and download `google-services.json`
5. Configure AdMob with your ad unit IDs
6. Build for Android

---

## License

MIT License
