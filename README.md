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

## 🧱 High-Level Architecture

```mermaid
flowchart LR
    subgraph Legacy[Legacy Systems]
        L1[Legacy DB dumps (CSV / XLS / Custom)]
        L2[Scanned documents (File shares)]
    end

    subgraph ETL[Migration & ETL Layer]
        C[Cleaning scripts (Python)]
        V[Validation rules]
        B[Batch loader\n(Celery workers)]
    end

    subgraph Core[Core Application Layer]
        D[PostgreSQL Primary DB]
        SVC[Django app Back-office UI]
        API[FastAPI Public/Internal APIs]
    end

    subgraph Infra[Infrastructure]
        OSS[Object Storage (Alibaba OSS)]
        MQ[Message Queue]
        MON[Monitoring & Alerts]
    end

    L1 --> C --> V --> B --> D
    L2 --> OSS

    SVC --> D
    API --> D

    SVC --> MQ --> MON
    API --> MQ

