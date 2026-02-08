# Okenaba – Technical Stack

> Status: Initial / Living Document  
> This stack defines the current foundation. Components may evolve, but the philosophy stays stable.

---

## 1. Overview

Okenaba is built as a **Python-first, server-rendered web application** focused on clarity, trust, and low operational complexity.

The system deliberately avoids a traditional frontend-backend split and instead uses **FastHTML + MonsterUI** as a unified application layer.

---

## 2. Core Principles

- Server-rendered by default
- Minimal JavaScript
- Python-only UI and business logic
- Validation-driven data flow
- Calm, predictable user experience
- Designed for non-technical users

---

## 3. Application Layer

### 3.1 FastHTML (Web Framework)

**Role**
- Primary web framework
- Routing, request handling, responses
- Server-side HTML rendering

**Why**
- Simple mental model
- Fewer moving parts
- Ideal for CRUD + confirmation flows
- No SPA complexity

FastHTML acts as both the backend and the UI delivery layer.

---

### 3.2 MonsterUI (UI System)

**Role**
- Core UI framework
- Component library
- Layout and design system
- Styling abstraction

MonsterUI is treated as a **first-class dependency**, not a cosmetic layer.

**Used for**
- Forms (receipt creation, confirmation)
- Layouts (dashboard, public pages)
- Navigation (navbars, tabs)
- Feedback states (alerts, loading, labels)
- Consistent typography and spacing

**Key Characteristics**
- Python-defined UI
- Server-rendered HTML
- Pre-styled semantic components
- Theme-based styling
- Minimal custom CSS

**Theme Initialization Example**
```python
app, rt = fast_app(
    hdrs=Theme.blue.headers()
)

4. Design Intent

The UI must consistently feel:

Calm

Reassuring

Predictable

Trust-oriented

MonsterUI enforces consistency and reduces UI-related decision fatigue by providing pre-styled, semantic components and predictable layout primitives.

5. UI Composition Strategy

Pages are composed using a small, consistent set of MonsterUI primitives:

Container, Grid, Card

Form, LabelInput, TextArea, Select

NavBar, TabContainer

Alert, Label, Divider

Guidelines:

Reusable UI patterns are preferred over custom layouts

UI logic must remain server-side

Custom CSS is avoided unless strictly necessary

6. Data Modeling & Validation
6.1 Pydantic

Role

Data validation

Schema definition

Internal data contracts

Used For

Receipt models

Form input validation

API and storage boundaries

Principle

Data that passes Pydantic validation is safe to store and display.

Validation always happens before persistence.

7. Persistence & Authentication
7.1 Supabase (PostgreSQL)

Role

Primary database

Authentication provider

Access control via Row Level Security (RLS)

Used For

Seller accounts

Receipt records

Confirmation state

Audit logs

Authentication Model

Sellers authenticate via email or OAuth

Buyers do not require accounts

Buyers access receipts through signed public links

Supabase is treated as infrastructure, not a frontend platform.

8. Caching & Ephemeral State
8.1 Upstash (Redis)

Role

Supporting cache and state layer

Used For

Signed receipt link tokens

One-time confirmation tokens

Basic rate limiting

Temporary state

Design Rule
Redis is non-critical.
The system must remain functional if Redis is temporarily unavailable.

9. Rendering & Interaction Model

100% server-rendered HTML

No client-side state management

No SPA framework

JavaScript only where unavoidable (e.g. modals)

This ensures:

Predictable behavior

Easier debugging

Lower maintenance burden

Long-term stability

10. Security & Trust Model

Signed public URLs

One-time confirmation tokens

Immutable finalized receipts

Server-side validation only

Clear separation of public and authenticated routes

Security is implemented quietly and consistently.

11. Explicitly Out of Scope

The following are intentionally excluded:

Frontend frameworks (React, Vue, etc.)

Custom CSS systems

Payment processing

Escrow services

Messaging or chat

Dispute resolution

Marketplace features

These exclusions reduce complexity and legal exposure.

12. Planned (Not Implemented)

These features may be introduced later if justified:

PDF generation for finalized receipts

Receipt versioning (pre-final)

Organization or team accounts

Public API access

White-label UI options

Nothing in this list is guaranteed.

13. Summary

Okenaba’s technical stack is:

Python-first

Server-rendered

Validation-driven

UI-consistent

Calm by design

The stack exists to support closure, clarity, and trust — not technical novelty.




---

### Why this version is strong
- No duplication
- Clear hierarchy
- Strong guardrails against stack creep
- Easy for future contributors to follow
- Perfectly aligned with FastHTML + MonsterUI reality

If you want next, I can:
- Extract **UI-only rules** into `ui_guidelines.md`
- Define **domain models** in `domain.md`
- Create a **repo structure** that enforces this stack
- Write a **non-negotiables.md** for contributors

Just tell me what’s next.
