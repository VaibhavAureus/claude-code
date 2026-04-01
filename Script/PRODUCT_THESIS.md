# ClaimPilot — Product Thesis

## AI-Powered Personal Document Advocate

**One-liner:** An AI agent platform that reads your bills, contracts, and paperwork — finds errors, knows your rights, and fights on your behalf.

---

## The Problem

Americans are drowning in complex paperwork that costs them real money:

| Domain | The Pain | Scale |
|--------|----------|-------|
| **Medical bills** | 80% contain errors; avg $1,300 overcharge on bills >$10K | 100M+ Americans carry medical debt |
| **Insurance claims** | 1 in 7 claims denied; only 0.1% are appealed | $262B in denied claims annually |
| **Tax filing** | Avg American spends 13hrs + $290; most miss deductions | $464B total compliance burden/year |
| **Contracts & leases** | Hidden clauses, illegal terms, missed renewal dates | 44M renter households in US |
| **Government forms** | 10,000+ federal forms; 11.6B hours/year spent filling them | Every single American |

**The core insight:** People don't fight back — not because they're lazy, but because they don't know:
1. That the error exists
2. What their rights are
3. How to draft a proper dispute
4. When to follow up

**This is a $500B+ problem** ($125B medical billing errors + $375B health insurance paperwork waste + $464B tax compliance) where the solution for individuals today is either:
- **Do nothing** (what 95% of people do) → lose money
- **Hire a professional** ($200-500/hr for billing advocates, lawyers, accountants) → too expensive
- **DIY research** (hours of Googling, phone calls, hold music) → too painful

---

## The Product

**ClaimPilot** is an AI-powered personal advocate that:

1. **READS** your documents (bills, EOBs, contracts, tax forms, letters)
2. **ANALYZES** them using specialized AI agents working in parallel
3. **FINDS** errors, overcharges, missing deductions, risky clauses, and missed rights
4. **EXPLAINS** everything in plain English — what's wrong and why it matters
5. **ACTS** by drafting dispute letters, appeal forms, optimized tax filings, and negotiation scripts
6. **TRACKS** deadlines, follow-ups, and resolutions to completion

### User Journey (Medical Bill Example)

```
User uploads medical bill + insurance EOB
        ↓
┌─────────────────────────────────────────────────┐
│  AGENT 1: Bill Itemizer                         │
│  Extracts every line item, CPT code, charge     │
├─────────────────────────────────────────────────┤
│  AGENT 2: Rate Researcher (parallel)            │
│  Looks up fair market rates for each procedure  │
│  in user's geographic area                      │
├─────────────────────────────────────────────────┤
│  AGENT 3: Insurance Matcher (parallel)          │
│  Cross-references charges against EOB coverage  │
│  and policy terms                               │
├─────────────────────────────────────────────────┤
│  AGENT 4: Error Detector (parallel)             │
│  Flags duplicate charges, unbundling errors,    │
│  upcoding, wrong patient info, services not     │
│  rendered                                       │
├─────────────────────────────────────────────────┤
│  AGENT 5: Rights Advisor                        │
│  Identifies applicable protections (No Surprise │
│  Act, state laws, appeal rights, financial      │
│  assistance programs)                           │
└─────────────────────────────────────────────────┘
        ↓
SYNTHESIS: Consolidated report with:
  - Total potential savings: $2,847
  - 3 billing errors found
  - 2 applicable legal protections
  - Recommended actions ranked by impact
        ↓
USER APPROVES (human-in-the-loop)
        ↓
AGENT 6: Letter Drafter
  - Generates dispute letter to provider
  - Generates appeal letter to insurer
  - Includes correct legal citations
  - Formatted for mailing or email
        ↓
SCHEDULED: Follow-up reminder in 30 days
  - "Your dispute with Memorial Hospital was
     filed 30 days ago. Want me to draft a
     follow-up letter?"
```

### Product Verticals (Phased Rollout)

**Phase 1 — Medical Bills (Wedge)** ← Start here
- Bill analysis & error detection
- Insurance EOB cross-referencing
- Dispute letter generation
- Appeal drafting for denied claims
- Financial assistance program matching

**Phase 2 — Insurance Claims**
- Auto/home/health claim filing assistance
- Denial appeal automation
- Policy coverage analysis
- Claim valuation benchmarking

**Phase 3 — Contracts & Leases**
- Lease review (flag illegal terms, unfair clauses)
- Employment contract analysis
- Service agreement red flags
- Renewal/termination deadline tracking

**Phase 4 — Tax Optimization**
- Deduction discovery from receipts/bank statements
- Tax form preparation assistance
- Audit response support
- Year-round tax planning

**Phase 5 — Government & Bureaucracy**
- Form-filling assistance (immigration, permits, benefits)
- Deadline tracking for applications
- Eligibility matching for programs
- Status tracking and follow-up

---

## Why THIS Codebase Makes It Possible

The Claude Code architecture isn't just "a chatbot" — it's a **full agent orchestration platform** with exactly the primitives needed for this product:

| Claude Code Capability | ClaimPilot Usage |
|---|---|
| **Multi-agent orchestration** | 5+ specialized agents analyze a single bill in parallel (itemizer, rate researcher, insurance matcher, error detector, rights advisor) |
| **Plugin system** | Each vertical (medical, insurance, legal, tax) is a plugin with its own agents, commands, and hooks |
| **MCP protocol** | Connect to healthcare price APIs, insurance databases, legal databases, tax code APIs, government form APIs |
| **File processing (Read/Write)** | Ingest PDFs of bills, EOBs, contracts, tax forms; generate dispute letters, appeals, optimized forms |
| **Web research (WebSearch/WebFetch)** | Look up fair market rates, regulations, legal precedents, program eligibility, form requirements |
| **Scheduling** | Recurring reminders: "30-day follow-up on your dispute", "Lease renewal in 60 days", "Quarterly tax estimated payment due" |
| **Hooks (safety guardrails)** | PreToolUse hooks ensure: no PHI leakage, legal disclaimers on advice, human approval before sending any letter |
| **Persistent state (.claude/ files)** | User profile, document history, active disputes, savings tracker, preferences |
| **Structured output** | Standardized analysis reports, savings calculations, action item checklists |
| **Human-in-the-loop (permissions)** | User approves every action before letters are sent, claims filed, or forms submitted |
| **AskUserQuestion** | Interactive clarification: "Is this bill from an in-network provider?" "What's your annual deductible?" |
| **Voice mode** | Users can describe their situation verbally instead of typing complex medical/legal details |

### Architecture (Built as Claude Code Plugins)

```
claimpilot/
├── plugins/
│   ├── medical-bills/
│   │   ├── .claude-plugin/plugin.json
│   │   ├── commands/
│   │   │   ├── scan-bill.md           # /scan-bill <upload>
│   │   │   ├── dispute.md             # /dispute <bill-id>
│   │   │   ├── appeal.md              # /appeal <claim-id>
│   │   │   └── savings-report.md      # /savings-report
│   │   ├── agents/
│   │   │   ├── bill-itemizer.md
│   │   │   ├── rate-researcher.md
│   │   │   ├── insurance-matcher.md
│   │   │   ├── error-detector.md
│   │   │   ├── rights-advisor.md
│   │   │   └── letter-drafter.md
│   │   ├── hooks/
│   │   │   └── hooks.json             # PHI protection, disclaimers
│   │   ├── skills/
│   │   │   └── medical-billing/
│   │   │       ├── SKILL.md           # CPT codes, billing rules
│   │   │       ├── references/
│   │   │       │   ├── no-surprises-act.md
│   │   │       │   ├── common-billing-errors.md
│   │   │       │   └── state-protections.md
│   │   │       └── examples/
│   │   │           ├── dispute-letter-template.md
│   │   │           └── appeal-letter-template.md
│   │   └── .mcp.json                  # Healthcare price API, CMS data
│   │
│   ├── insurance-claims/
│   │   └── ... (same structure)
│   │
│   ├── contracts-leases/
│   │   └── ... (same structure)
│   │
│   ├── tax-optimizer/
│   │   └── ... (same structure)
│   │
│   └── core/
│       ├── commands/
│       │   ├── dashboard.md           # /dashboard — overview of all active items
│       │   ├── upload.md              # /upload — smart document routing
│       │   └── track.md              # /track — status of all disputes/claims
│       ├── agents/
│       │   ├── document-classifier.md # Routes docs to correct vertical
│       │   └── savings-tracker.md     # Aggregates total savings across all verticals
│       ├── hooks/
│       │   └── hooks.json            # Global safety: disclaimers, PII protection
│       └── skills/
│           └── user-profile/
│               └── SKILL.md          # Insurance info, address, family, preferences
```

---

## Market Analysis

### Total Addressable Market (TAM)

| Segment | Population | Willingness to Pay | TAM |
|---|---|---|---|
| Medical bill disputes | 100M Americans with medical debt | $20/month or 15% of savings | $24B/year |
| Insurance claim appeals | 50M denied claims/year | $50/claim or 20% of recovery | $10B/year |
| Contract/lease review | 44M renter households | $10/review | $440M/year |
| Tax optimization | 150M individual filers | $30/year beyond basic filing | $4.5B/year |
| Government form assistance | 50M complex form filers/year | $15/form | $750M/year |
| **Total** | | | **~$40B/year** |

### Serviceable Addressable Market (SAM) — Year 1-3

Focus: Medical bills + insurance claims in the US
- 30M Americans actively struggling with medical bills × $15/month = **$5.4B/year**

### Serviceable Obtainable Market (SOM) — Year 1

- 100K users × $15/month = **$18M ARR** target

### Revenue Model

| Tier | Price | Features |
|---|---|---|
| **Free** | $0 | 1 bill scan/month, basic error detection, no letter drafting |
| **Personal** | $15/month | Unlimited scans, full analysis, dispute letters, follow-up tracking |
| **Family** | $29/month | Multi-member household, all verticals, priority processing |
| **Enterprise (B2B2C)** | Custom | White-label for employers, unions, health systems to offer members |

**Performance pricing option:** Free analysis + 15% of documented savings (aligns incentives perfectly)

---

## Competitive Landscape

| Competitor | What They Do | ClaimPilot Differentiator |
|---|---|---|
| **Faircare** (launched Mar 2026) | Consumer app for medical bill scanning | Single-purpose; ClaimPilot is multi-vertical with agent orchestration |
| **Advocara** | Connects users with human advocates | Expensive ($200+/hr); ClaimPilot automates 90% of the work |
| **Medical billing advocates** | Human professionals | $150-500/hr; 2-6 month timelines; ClaimPilot is instant + $15/mo |
| **TurboTax / H&R Block** | Tax filing only | Tax-only; no bills, claims, contracts, or bureaucracy |
| **DoNotPay** | "Robot lawyer" chatbot | Broad but shallow; generic chatbot, no multi-agent depth |
| **LegalZoom / Rocket Lawyer** | Legal document templates | Templates only; no analysis, no advocacy, no disputes |
| **ChatGPT / Claude chat** | General AI assistant | No persistent state, no scheduling, no integrations, no guided workflows |

**ClaimPilot's moat:**
1. **Multi-agent architecture** — Not a single chatbot, but a coordinated team of specialist agents
2. **Domain knowledge base** — Curated skills with CPT codes, billing rules, legal protections, tax codes
3. **MCP integrations** — Pre-wired connections to healthcare price APIs, insurance databases, legal databases
4. **Persistent state** — Remembers your insurance, past disputes, savings history, deadlines
5. **Scheduling** — Proactive follow-ups, deadline reminders, recurring audits
6. **Network effects** — Every disputed bill improves error detection patterns for all users

---

## Technical Implementation Plan

### Phase 1: MVP (Weeks 1-6) — Medical Bill Scanner

**Build:**
1. `medical-bills` plugin with core commands (`/scan-bill`, `/dispute`)
2. `bill-itemizer` agent — extracts line items from uploaded bills
3. `error-detector` agent — flags common billing errors (duplicates, upcoding, unbundling)
4. `letter-drafter` agent — generates dispute letters
5. Safety hooks — legal disclaimers, PHI protection
6. Basic user profile storage in `.claude/claimpilot-profile.local.md`

**MCP Integrations:**
- CMS Healthcare Price Transparency API (fair market rates)
- MedPAR/HCRIS public data (hospital cost reports)

**Skills:**
- Common billing error patterns database
- No Surprises Act provisions
- State-by-state billing protection laws
- Dispute letter templates

### Phase 2: Insurance Claims (Weeks 7-12)

**Add:**
- EOB cross-referencing agent
- Insurance coverage analysis agent
- Claim appeal letter generator
- Denial reason code database (CARC/RARC codes)
- Scheduling for appeal deadline tracking

### Phase 3: Contracts & Leases (Weeks 13-18)

**Add:**
- Lease review agent (flag illegal clauses by state)
- Contract risk scorer
- Renewal/termination deadline scheduler
- Negotiation talking points generator

### Phase 4: Full Platform (Weeks 19-24)

**Add:**
- Tax optimization agent
- Government form assistant
- Unified dashboard (`/dashboard`)
- Savings tracker across all verticals
- Family account support

---

## Key Risks & Mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| **Unauthorized practice of law/medicine** | High | Clear disclaimers on every output; frame as "information tool, not legal/medical advice"; human-in-the-loop approval for all actions |
| **PHI/PII data handling** | High | All processing local (no cloud upload of medical data); PreToolUse hooks strip/mask sensitive data before web calls; encryption at rest |
| **Accuracy of error detection** | High | Conservative flagging (over-flag, let user decide); cite sources for every claim; continuous feedback loop |
| **Regulatory changes** | Medium | Scheduled agents that monitor for regulatory updates; modular skills that can be updated independently |
| **User trust** | Medium | Transparent reasoning (show work, not just conclusions); free tier for trial; performance pricing aligns incentives |
| **Provider/insurer pushback** | Medium | Users own their data and rights; ClaimPilot exercises existing consumer rights, doesn't create new ones |

---

## Why Now?

1. **Medical debt crisis is peaking** — 100M+ Americans affected, [political momentum for reform](https://www.pymnts.com/healthcare/2026/healthcares-billing-wars-are-becoming-an-ai-vs-ai-contest/)
2. **AI capabilities are finally sufficient** — Claude's document understanding + reasoning quality makes this viable for the first time
3. **Healthcare price transparency rules** — CMS mandates hospitals publish prices, creating the data layer we need
4. **No Surprises Act (2022)** — Created new consumer rights that most people don't know how to exercise
5. **Agent frameworks are mature** — Claude Code's plugin/agent/MCP/hooks architecture provides the exact infrastructure needed
6. **Competitors are just starting** — Faircare launched March 2026; the market is nascent with no dominant player
7. **AI vs AI dynamic** — Insurers and providers are using AI to optimize billing; consumers need AI to fight back on equal footing

---

## The Vision

> **Today:** You get a $4,700 medical bill. You feel sick. You pay it.
>
> **With ClaimPilot:** You photograph the bill. In 60 seconds, five AI agents tell you there are $1,847 in errors, you're protected by the No Surprises Act, and here's a dispute letter ready to send. You tap "Send." Thirty days later, ClaimPilot reminds you to follow up, and drafts that letter too. Your bill drops to $2,853. You saved $1,847 without making a single phone call.
>
> **The future:** ClaimPilot proactively monitors your insurance claims, flags every error before you even see a bill, automatically files appeals for denied claims, optimizes your tax deductions year-round, reviews every contract before you sign, and ensures you never miss a deadline or leave money on the table.

**ClaimPilot turns Claude Code's agent infrastructure into something every American household needs — a personal advocate that never sleeps, never forgets, and never gives up.**

---

## Sources

- [Aptarro - 40+ Medical Billing Stats 2026](https://www.aptarro.com/insights/medical-billing-stats)
- [Gitnux - Medical Billing Errors Statistics 2026](https://gitnux.org/medical-billing-errors-statistics/)
- [PYMNTS - Healthcare Billing Wars: AI vs AI](https://www.pymnts.com/healthcare/2026/healthcares-billing-wars-are-becoming-an-ai-vs-ai-contest/)
- [Faircare - Consumer App Launch](https://news.marketersmedia.com/faircare-launches-consumer-app-to-detect-medical-billing-errors-and-reduce-medical-debt/89184733)
- [Fortune - Americans Spend $146B on Tax Compliance](https://fortune.com/2026/03/24/tax-compliance-cost-americans-2026/)
- [NTU Foundation - Tax Compliance Burden](https://www.ntu.org/foundation/detail/taxpayers-will-spend-71-billion-hours-464-billion-on-tax-compliance-in-2025)
- [CPA Practice Advisor - 11.6 Billion Hours on Federal Forms](https://www.cpapracticeadvisor.com/2026/03/16/americans-to-spend-11-6-billion-hours-completing-federal-compliance-forms/179866/)
- [CNBC - Health Insurance Paperwork Wastes $375B](https://www.cnbc.com/2015/01/13/health-insurance-paperwork-wastes-375-billion.html)
- [AJMC - Billing Errors in US Health Insurance](https://www.ajmc.com/view/survey-exposes-pervasive-billing-errors-aggressive-tactics-in-us-health-insurance)
- [SNS Insider - IDP Market Size](https://www.snsinsider.com/reports/intelligent-document-processing-market-2937)
- [Grand View Research - Legal AI Market](https://www.grandviewresearch.com/industry-analysis/legal-ai-market-report)
- [IBM - AI Tech Trends 2026](https://www.ibm.com/think/news/ai-tech-trends-predictions-2026)
- [Microsoft - 7 AI Trends to Watch 2026](https://news.microsoft.com/source/features/ai/whats-next-in-ai-7-trends-to-watch-in-2026)
- [Google Cloud - AI Agent Trends 2026](https://cloud.google.com/resources/content/ai-agent-trends-2026)
