# D-SHIELD Threat Detection FSM State Diagram

```text
                 +----------------+
                 |                |
                 |      SAFE      |
                 |                |
                 +----------------+
                         |
          fusion_score = 1
                         |
                         v

                 +----------------+
                 |                |
                 |      LOW       |
                 |                |
                 +----------------+
                         |
          fusion_score = 2
                         |
                         v

                 +----------------+
                 |                |
                 |    MEDIUM      |
                 |                |
                 +----------------+
                         |
          fusion_score = 3
                         |
                         v

                 +----------------+
                 |                |
                 |      HIGH      |
                 |                |
                 +----------------+
                         |
             HIGH persists
              for 4 cycles
                         |
                         v

                 +----------------+
                 |                |
                 |    CRITICAL    |
                 |                |
                 +----------------+

```

## Defense Modes

| Mode | Description |
|------|-------------|
| 00 | Surveillance Mode |
| 01 | Defensive Mode |
| 10 | Emergency Mode |
| 11 | Lockdown Mode |

## Reconfigurable Behavior

### Surveillance Mode
- Conservative detection
- Normal escalation

### Defensive Mode
- Faster escalation
- Increased sensitivity

### Emergency Mode
- Aggressive threat escalation
- Medium threats become HIGH

### Lockdown Mode
- Immediate CRITICAL activation
- Maximum defense readiness

# D-SHIELD FSM State Table

| Fusion Score | Mode | Next State |
|--------------|------|-------------|
| 00 | Any | SAFE |
| 01 | Surveillance | LOW |
| 01 | Defensive | LOW |
| 01 | Emergency | MEDIUM |
| 01 | Lockdown | HIGH |
| 10 | Surveillance | MEDIUM |
| 10 | Defensive | HIGH |
| 10 | Emergency | HIGH |
| 10 | Lockdown | CRITICAL |
| 11 | Surveillance | HIGH |
| 11 | Defensive | HIGH |
| 11 | Emergency | CRITICAL |
| 11 | Lockdown | CRITICAL |

---

# State Encoding

| State | Binary Encoding |
|-------|-----------------|
| SAFE | 000 |
| LOW | 001 |
| MEDIUM | 010 |
| HIGH | 011 |
| CRITICAL | 100 |

---

# Mode Encoding

| Mode | Binary |
|------|--------|
| Surveillance | 00 |
| Defensive | 01 |
| Emergency | 10 |
| Lockdown | 11 |
