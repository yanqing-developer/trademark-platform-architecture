# trademark-platform-architecture
Architecture notes and case study

# 🏛 Trademark Information Management System — Architecture Notes

**Tech stack:** Python · Django · FastAPI · PostgreSQL · Celery · Alibaba Cloud

This repository documents the **architecture and key technical decisions** behind an
enterprise trademark information management system I worked on between **2018–2022**.

> ⚠️ No production code is included.  
> All examples are **anonymised** and simplified to focus on architecture and
> engineering decisions.

---

## 🎯 Project Context

- **Organisation:** National-level IP service provider (patent & trademark office)
- **Users:** Internal attorneys, paralegals, case managers
- **Scope:** Centralise and digitalise trademark cases accumulated since the 1960s
- **Data volume:**  
  - 2M+ historical trademark records  
  - Tens of millions of related events, documents and status changes

My role was **backend lead engineer**, responsible for data modelling, migration
pipeline, and backend API design.

---

