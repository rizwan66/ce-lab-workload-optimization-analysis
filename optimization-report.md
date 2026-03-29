# Workload Optimization Report

## Executive Summary
Total identified monthly savings: $64.91 across scheduling and storage cleanup.

## 1. Instance Scheduling (Priority: HIGH)

| Instance | Type | Current Cost/mo | Scheduled Cost/mo | Savings/mo |
|----------|------|-----------------|-------------------|------------|
| dev-frontend | t3.medium | $30.37 | $10.07 | $20.30 |
| dev-backend | t3.large | $60.74 | $20.13 | $40.61 |
| **Subtotal** | | **$91.11** | **$30.20** | **$60.91** |

**Implementation:** EventBridge + Lambda scheduler (deployed in this lab)
- Stop rule: `cron(0 23 ? * MON-FRI *)` — 7 PM EST weekdays
- Start rule: `cron(0 12 ? * MON-FRI *)` — 8 AM EST weekdays

## 2. Orphaned EBS Volumes (Priority: MEDIUM)

| Volume ID | Size (GB) | Monthly Cost | Action |
|-----------|-----------|-------------|--------|
| vol-04171b8d024fb30f6 | 50 | $4.00 | Delete after backup verification |
| **Subtotal** | | **$4.00** | |

## 3. Old Snapshots (Priority: LOW)

| Count | Total Size (GB) | Monthly Cost | Action |
|-------|-----------------|-------------|--------|
| 0 snapshots > 90 days | 0 GB | $0.00 | Implement lifecycle policy going forward |

## Prioritized Recommendations
1. **Enable instance scheduling** — $60.91/mo savings, zero performance impact
2. **Delete orphaned volumes** — $4.00/mo, verify no dependencies first
3. **Purge old snapshots** — $0/mo currently, implement lifecycle policy going forward

## Annual Projected Savings: $779.00
