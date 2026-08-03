# Retry Policy Design — [Your Name]

## Scenario Reference
Service: ParcelPulse → CarrierAPI (`POST /labels`)

---

## Section 1 — Outcome Classification

| Outcome | Retry? | Reason / required action |
|---|---|---|
| Connection reset | | |
| Client timeout after request sent | | |
| `429` + `Retry-After: 6` | | |
| `503` | | |
| `400` invalid address | | |
| `401` expired token | | |
| `403` blocked account | | |
| `422` unsupported parcel | | |

> Note on timeout: state whether outcome of first attempt is known and how idempotency key is handled.

---

## Section 2 — Timeout and Deadline

```
connection timeout:        ___ ms
per-attempt timeout:       ___ ms
overall deadline:          ___ ms
maximum total attempts:    ___ (1 initial + ___ retries)
```

**Worst-case elapsed time calculation:**

```
attempt 1:  attempt-timeout + backoff sleep = ___ms + ___ms
attempt 2:  attempt-timeout + backoff sleep = ___ms + ___ms
attempt 3:  attempt-timeout                 = ___ms
total:                                        ___ms
```

> Total must fit inside overall deadline. Justify your choices from the observed data.

---

## Section 3 — Backoff and Jitter

Formula:
```
delayCap(n) = min(maxDelay, baseDelay × 2^n)
sleep(n)    = random(0, delayCap(n))
```

Chosen values:
```
baseDelay: ___ ms
maxDelay:  ___ ms
```

| Retry | delayCap | Actual sleep range |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |

**Retry-After formula:**
```
sleep = max(Retry-After value, delayCap) + random(0, jitter)
```

---

## Section 4 — Retry Amplification and Budget

Current worst case:
```
600 original × (1 + 5 retries) = 3,600 total calls
```

Proposed budget:
```
budget window:        ___ seconds
retry calls allowed:  ___% of original calls
at 600/min:           maximum ___ retry calls/min
```

What happens when budget is exhausted:
> (write here — "keep retrying" is not allowed)

---

## Section 5 — Safety, Fallback, Observability

**1. Idempotency-Key generation and reuse:**
> 

**2. User-visible message when retries/deadline/budget end:**
> 

**3. Independent fallback if CarrierAPI stays down:**
> 

**4. Four metrics and one alert:**

| Metric | Alert condition |
|---|---|
| | |
| | |
| | |
| | |

**5. Where in call chain retries should happen:**
> 

---

*Submit as a single PDF. Maximum 4 pages. Show all arithmetic.*
