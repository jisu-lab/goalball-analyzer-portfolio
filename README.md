## Throw Analysis Design

최종적으로 하나의 투구에 대해 다음 정보를 생성하는 것을 목표로 합니다.

```text
Throw Event

Attacker
Release Position
Release Zone

Trajectory

Expected Target Position
Target Zone

Contact Position

Result
- Goal
- Block
- Out

Penalty
- High Ball
- Long Ball
```

특히 수비수에게 공이 막힌 경우에도  
실제 접촉 위치와 공이 원래 향하고 있던 **예상 Target Zone을 분리**하여 분석하도록 설계하고 있습니다.

---

## 7 × 7 Throw Course Analysis

골대를 7개의 Zone으로 나누고

```text
Release Zone × Target Zone
```

형태의 7 × 7 투구 경로 데이터를 생성할 예정입니다.

이를 통해 선수별로 다음과 같은 패턴을 분석할 수 있습니다.

- 자주 사용하는 투구 시작 위치
- 선호하는 공격 코스
- 득점 성공률
- 수비 성공률
- 특정 Zone 공격 비율
- 상대 선수별 공격 패턴

---

## Architecture

프로젝트는 기능별 책임을 분리하여 구성하고 있습니다.

```text
Core
 └─ Match / Throw data structures

Vision
 ├─ BallDetector
 ├─ PlayerDetector
 └─ Tracking

Analysis
 └─ ThrowAnalyzer

Database
 └─ Calibration / Match data

UI
 └─ Dear ImGui

Rendering
 └─ DirectX 11
```

Vision 모듈은 UI 코드에 의존하지 않고  
분석 로직과 화면 표시 로직도 분리하는 방향으로 설계하고 있습니다.

---

## Development Status

### Implemented

- [x] Windows C++ application
- [x] Video playback
- [x] Court calibration
- [x] Homography
- [x] Calibration persistence
- [x] Ball candidate detection
- [x] Ball tracking experiments
- [x] YOLOv8 player detection
- [x] Manual Throw Event annotation

### In Progress

- [ ] Player tracking
- [ ] Player role identification
- [ ] Ball / Player association
- [ ] Throw release detection
- [ ] Trajectory estimation
- [ ] Target Zone prediction
- [ ] Goal / Block / Out classification
- [ ] 7 × 7 throw statistics