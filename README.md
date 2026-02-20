# Workforce Planning Across Different Time Zones (Support Coverage + Project Time) — Simulated Mockup

This is a **portfolio project** that demonstrates a practical approach to **workforce planning and scheduling** for a global customer support team across different **time zones**, under a **4‑day work week**, while still meeting hourly customer coverage needs.

It also includes the 2026 idea of **dedicated project time** (half-day/full-day blocks) and shows how to allocate that time **only when support coverage allows**.

> ✅ **Disclaimer:** This project uses **simulated data** inspired by public posts.  
> It does **not** use any internal/company support data.

---

## What problem this solves (simple explanation)

Customer support teams need to be “always on”, but:
- volume changes by **hour and day**
- people work in different **time zones**
- schedules must be **fair** and **stable**
- and teams still need time for **projects and improvements**

This mockup shows how to use data + optimization to:
- estimate **hour‑by‑hour coverage needed**
- create schedules that match that coverage
- protect project time without breaking customer support

---

## What’s inside

### Notebook
- `notebook/` (recommended)
  - Your Jupyter notebook (`.ipynb`) with the full workflow.

---

## Process (what the notebook does)

### 1) Simulated hourly requirement (calibrated to 386 agent-hours/week)
- Creates a weekly 7×24 view (168 hours).
- Simulates realistic demand patterns (weekdays busier than weekends, peaks at certain hours).
- Scales the final requirement so the total equals **386 agent-hours/week**.

📊 Chart produced:
- **Heatmap: Required agents per hour (UTC)**

---

### 2) Team + schedule templates (4-day workweek & time zones)
- Simulates a team (Advocates & Leads) across multiple time zones.
- Generates possible schedule templates that follow rules like:
  - 4 working days/week
  - 3 days off/week
  - at least 2 consecutive off-days
  - shift start times (example: 09:00 / 12:00 / 15:00 local)
- Adds a simple “cost score” to represent preferences and fairness proxy.

---

### 3) Heuristic schedule (greedy baseline)
- Builds a schedule using a simple greedy approach.
- Purpose: quick baseline that is easy to understand and compare.

📊 Chart produced:
- **Heatmap: Capacity − Required (Heuristic)**  
  - Positive = extra coverage  
  - Negative = coverage gaps

---

### 4) Optimized schedule (MILP via SciPy/HiGHS)
- Uses a solver to choose the best schedule template per person.
- Optimization goal:
  - heavily reduce **undercoverage**
  - lightly penalize **overcoverage**
  - include a small “stability” proxy (avoid unnecessary changes)

📊 Chart produced:
- **Heatmap: Capacity − Required (Optimized / MILP)**

---

### 5) Project time blocks (only where coverage allows)
- After the optimized schedule is created, the notebook allocates “project blocks”:
  - half-day blocks in this mockup (3 hours)
  - only in time windows where there is surplus capacity
- This reflects the idea: people can step away from inbox **without harming customers**.

---

### 6) What-if analysis (demand deflection → more project capacity)
- Simulates what happens if demand drops due to:
  - self‑serve improvements
  - AI deflection
  - systemic fixes
- Shows how reduced demand creates **more surplus hours**, which can be used for project blocks.

📈 Chart produced:
- **Deflection rate vs surplus agent-hours**

---

## How to run locally

### Install dependencies
```bash
pip install numpy pandas matplotlib scipy openpyxl reportlab
