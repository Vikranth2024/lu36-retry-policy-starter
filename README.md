# LU36 — Retry Policy Starter Template

This repository contains the template for the LU36 retry-policy design assignment.

## How to use

1. Open `retry-policy-template.md`
2. Fill in every section using the observed production data from the assignment question
3. Export your completed document as a **PDF** (max 5 MB, max 4 pages)
4. Upload the PDF to the assignment submission portal

## Template sections

| Section | What to fill in |
|---|---|
| 1. Outcome Classification | Retry decision + reasoning for each failure type |
| 2. Timeout and Deadline | Exact values + worst-case arithmetic |
| 3. Backoff and Jitter | Formula, values, per-retry cap table, Retry-After rule |
| 4. Retry Amplification | Budget window, budget %, behaviour at exhaustion |
| 5. Safety and Fallback | Idempotency, user message, independent fallback, metrics |

## Submission

**PDF upload only. Do not submit a PR or repository URL.**

## Assignment scenario

ParcelPulse creates shipping labels via a third-party `CarrierAPI`. During a 20–40 second `503` window, 600 original calls each produced five synchronised retries, crashing the carrier a second time. Design a better policy.
