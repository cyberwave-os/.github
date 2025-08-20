# Cyberwave

**AI‑Native Robotics Infrastructure**

> The embodiment layer between intelligent systems and the physical world.

---

## TL;DR
- **Operate heterogeneous robots at scale** with a cloud–edge control plane, real‑time policies, and observability.
- **Blend autonomy + teleoperation**: humans stay in the loop, safety stays on by default.
- **Plug into your stack**: open interfaces for models, sensors, ERPs/MES, and industrial networks.

---

## What you can build
- **Flexible manufacturing cells** that switch tasks (pick, place, inspect, assemble) with model‑driven recipes.
- **Shared‑autonomy teleop** for remote intervention and supervision.
- **Inspection & QA** driven by vision models and programmable acceptance policies.
- **Mobile workflows** (AMRs, AGVs, drones) orchestrated as first‑class resources.
- **Digital twins** that mirror live state for simulation, planning, and analytics.

---

## Architecture at a glance

```
               ┌──────────────────────────────────────────────────────┐
               │                      Cloud                           │
               │  Control Plane  •  Fleet Orchestrator  •  Registry   │
               │  Audit/Observability  •  Policy/Guardrails           │
               └──────────────▲───────────────────▲───────────────────┘
                              │                   │
                              │                   │ events, metrics
                    commands, goals           (time‑series, traces)
                              │                   │
┌─────────────────────────────┼───────────────────┼─────────────────────────────┐
│                          Edge Runtime (Site)                                  │
│  Scheduler • Real‑time Executor • Safety Layer • Local Cache • Gateway        │
│  ┌───────────────┐  ┌──────────────┐  ┌──────────────────────┐               │
│  │  Drivers      │  │  Skills/Apps │  │  Policy Engine       │               │
│  │ (ROS 2, PLCs, │  │ (planning,   │  │ (zones, limits, SOT) │               │
│  │ Modbus, OBCs) │  │ control, VLM)│  │                      │               │
│  └───────▲───────┘  └──────▲───────┘  └──────────▲───────────┘               │
│          │                 │                       │                          │
│          │ drivers & IO    │ skills/contracts      │ runtime checks           │
└──────────┼─────────────────┼───────────────────────┼──────────────────────────┘
           │                 │                       │
      ┌────▼─────┐      ┌────▼─────┐            ┌────▼─────┐
      │ Robots   │      │ Sensors  │            │ Humans   │
      │ (arms,   │      │ (cams,   │            │ (teleop, │
      │ AMRs,    │      │ force,   │            │ review)  │
      │ drones)  │      │ lidar)   │            │          │
      └──────────┘      └──────────┘            └──────────┘
```

**Key ideas**
- **Open interfaces, closed loops**: predictable timing where it matters.
- **Policy‑first safety**: constraints are compiled and enforced at runtime.
- **Cloud↔Edge symmetry**: run centrally, fall back locally.
- **Vendor‑neutral**: drivers and adapters instead of lock‑in.

---

## What we ship (high level)
- **Control Plane** (cloud): fleet orchestration, registry, RBAC, audit, observability.
- **Edge Runtime**: deterministic scheduler, real‑time executor, cache, safety layer.
- **Policy & Guardrails**: declarative safety, work‑zones, speed/force limits, SOT gating.
- **Digital Twin & Data**: unified state, time‑series, playback, sim bridges.
- **SDKs**: Python/TypeScript APIs for apps, skills, and integrations.

---

## Example (preview)
> Illustrative only.

**Define a workcell with policies**
```yaml
# cell.yaml
apiVersion: v1
kind: Workcell
metadata:
  name: cell-a
spec:
  resources:
    robots:
      - id: ur5e-01
        driver: ros2
    sensors:
      - id: cam-top
        type: camera
  policies:
    safety:
      zones:
        - name: human-zone
          geometry: poly(...)
          onEnter: slow
      limits:
        maxLinearSpeed: 0.5 m/s
        maxToolForce: 40 N
```

**Send a goal from Python**
```python
from cyberwave import CW

cw = CW()
session = cw.connect(cell="cell-a")

plan = session.plan.pick_and_place(
    pick_pose=(0.2, 0.1, 0.05),
    place_pose=(0.4, -0.1, 0.05),
)

session.execute(plan)  # policy checks enforced by runtime
```

---

## Principles
- **Safety by default**: human‑in‑the‑loop > human‑as‑afterthought.
- **Deterministic where it matters**: bounded latency on the edge.
- **Composability**: skills, drivers, and models are pluggable contracts.
- **Observability**: every command is traceable, replayable.

---

## Roadmap highlights
- Edge runtime public preview
- CLI (`cw`) for deployments and diagnostics
- SDKs & example workcells (manipulation, inspection)
- Digital‑twin APIs for planning/simulation bridges

> Follow the organization to be notified when previews land.

---

## Community & support
- **Issues**: bug reports and feature requests go in the relevant repo.
- **Discussions**: design proposals, Q&A, showcases.
- **Security**: please report vulnerabilities privately (see SECURITY.md in each repo).
- **Responsible use**: safety, compliance, and human oversight are non‑negotiable.

---

## Contributing
We welcome issues, design reviews, and contributions once the public preview opens. See `CONTRIBUTING.md` for guidelines (coding style, DCO/CLA, review process).

---

## Credits
Built by engineers and researchers across robotics, real‑time systems, and ML. Thank you to the open‑source communities behind ROS 2, WebRTC, gRPC, and the broader robotics ecosystem.

---

<p align="center">
  <sub>© Cyberwave. All rights reserved.</sub>
</p>

