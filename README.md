# 🧭 PivotPilot — Evidence-Based AI Career Pivot Coach

> **Generative AI Hackathon Project**  
> Go from *"I want to switch careers"* to *"I got interviews"* with a personalized, evidence-based plan that adapts over time.

---

## 🌟 1. Core Principles (Why PivotPilot Outperforms Conventional Tools)

1. **Evidence-Based**: Every recommendation traces back to real, parsed Job Descriptions (JDs), never generic boilerplate advice.
2. **Adaptive Engine**: The curriculum automatically adjusts when you fall behind, when mock-interview rubric scores drop, or when job application feedback signals a missing skill.
3. **Transparent & Explainable**: Always explains *WHY* (e.g., *"SQL appears in 24 of 25 JDs analyzed (96%) with an importance weight of 5.0/5.0"*).
4. **Actionable**: Every single screen ends with a clear, high-ROI **"Next Best Action"** card with time estimates.
5. **Honest Confidence Levels**: Uses Bayesian Beta-Binomial shrinkage to report confidence badges (*"Early indicator: 3 applications"* vs *"High confidence: 15 applications"*). Never hallucinates statistics.

---

## 🛠️ 2. Tech Stack

- **Frontend & App Framework**: Next.js 14 (App Router) + TypeScript
- **Styling & UI Components**: Tailwind CSS + Custom CSS Variables + Lucide Icons + Sonner Toasts
- **Data Visualizations**: Recharts (Radar Benchmark, Priority Bar Chart, Habit Area Chart, Rubric Trajectory Line Chart)
- **Database & ORM**: SQLite (`prisma/dev.db`) + Prisma ORM (22 relational models with zero external credential requirements)
- **AI Service Layer**: Typed service layer with Zod schema validation, documented prompt templates in `prompts/`, fallback engines, and automated PII scrubbing
- **Resume & Document Ingestion**: `pdf-parse` + `mammoth` (supports PDF, DOCX, and pasted text)
- **Offline Demo Mode**: Pre-seeded with a realistic candidate persona (**Elena Vance: High School Teacher → Data Analyst**), 25 real JDs, 8-week curriculum, 3 domain-leveraged portfolio projects, scored mock interviews, and 15 diverse job applications.

---

## 📁 3. Project Structure

```
pivotpilot/
├── prisma/
│   ├── schema.prisma          # 22 relational models (Users, Profiles, Skills, JDs, Gaps, Plans, Tasks, Projects, Interviews, Rubrics, Applications, Insights)
│   └── dev.db                 # Local zero-configuration SQLite database
├── prompts/                   # Documented AI prompts with Zod validation schemas
│   ├── resume-parser.ts       # Resume profile & transferable strengths extractor
│   ├── jd-extractor.ts        # JD skills, tools, and seniority parser
│   ├── gap-analyzer.ts        # Evidence-based gap reasoning & priority scoring
│   ├── plan-generator.ts      # 8-week prerequisite-enforced curriculum generator
│   ├── project-recommender.ts # Domain-leveraged project architect
│   ├── interviewer.ts         # Adaptive mock interviewer & probing engine
│   ├── rubric-scorer.ts       # 6-dimension transparent rubric evaluator
│   ├── plan-adjuster.ts       # Adaptive engine (rules + LLM recalibration)
│   └── insight-narrator.ts    # Bayesian application statistics translator
├── scripts/
│   └── seed.mjs               # Seed script with realistic Elena Vance dataset
├── src/
│   ├── app/
│   │   ├── layout.tsx         # Root layout with sidebar, header, toaster, theme provider
│   │   ├── page.tsx           # Dashboard home (Flywheel overview, readiness ring, pivot story builder)
│   │   ├── globals.css        # Tailwind variables and styles
│   │   ├── onboarding/        # F1: 4-step resume intake wizard & review screen
│   │   ├── skill-gaps/        # F2: Skill gap map (Radar, Priority bar, evidence drawer)
│   │   ├── plan/              # F3: Week-by-week curriculum (Roadmap, Kanban, Checkpoint quiz)
│   │   ├── projects/          # F4: Portfolio project tracker (README generator, STAR bullets)
│   │   ├── interviews/        # F5: Mock interview room (6D rubric scoring, voice/text, timer)
│   │   ├── progress/          # F6: Progress & habit dashboard, Plan Changes audit log
│   │   ├── applications/      # F7: Application tracker & Bayesian learning insights
│   │   └── api/               # Typed Next.js route handlers
│   │       ├── ai/parse-resume/route.ts
│   │       ├── job-descriptions/route.ts
│   │       ├── skill-gaps/route.ts
│   │       ├── plan/route.ts
│   │       ├── plan/tasks/[id]/route.ts
│   │       ├── projects/route.ts
│   │       ├── projects/[id]/route.ts
│   │       ├── interviews/route.ts
│   │       ├── interviews/evaluate/route.ts
│   │       ├── progress/route.ts
│   │       ├── adjustments/[id]/route.ts
│   │       ├── applications/route.ts
│   │       ├── applications/[id]/route.ts
│   │       ├── export/applications/route.ts
│   │       └── seed/route.ts
│   ├── components/
│   │   ├── layout/
│   │   │   ├── sidebar.tsx    # Left navigation
│   │   │   ├── header.tsx     # Demo controls, reset seed, theme toggle
│   │   │   └── next-best-action.tsx # Actionable prompt on every screen
│   └── lib/
│       ├── db.ts              # Prisma singleton client
│       ├── ai-service.ts      # Structured AI service with fallback & PII scrubbing
│       ├── stats.ts           # Beta-Binomial Bayesian shrinkage calculations
│       └── resume-parser.ts   # Binary file text extractor (PDF & DOCX)
├── package.json
└── README.md
```

---

## 🚀 4. Quick Start & Setup

### Prerequisites
- Node.js 18+ (tested on Node 20 / Node 24)
- npm or pnpm

### 1. Install Dependencies
```bash
npm install
```

### 2. Configure Environment Variables
Copy or verify `.env`:
```env
DATABASE_URL="file:./dev.db"
LLM_PROVIDER="mock"            # Works 100% offline without API keys!
NEXT_PUBLIC_DEMO_MODE="true"
GEMINI_API_KEY=""              # Optional: add for live Gemini API calls
OPENAI_API_KEY=""              # Optional: add for live OpenAI API calls
```

### 3. Initialize & Seed Database
```bash
npx prisma generate
npx prisma db push
node scripts/seed.mjs
```

### 4. Run Development Server
```bash
npm run dev
```
Open **[http://localhost:3000](http://localhost:3000)** in your browser.

---

## ⏱️ 5. Three-Minute Hackathon Demo Script

### Narrative: "Elena Vance — High School Math Teacher pivoting to Junior Data Analyst"

| Timestamp | Screen / Feature | What to Show & Say |
|---|---|---|
| **0:00 - 0:35** | **Dashboard & Flywheel Overview (`/`)** | *"Career switchers struggle because generic advice doesn't tell them what specific skills hiring managers demand. Meet Elena Vance, an 8-year high school math teacher switching to Data Analytics. Here on PivotPilot's dashboard, her Role Readiness Score is at 72%. Notice the 60-Second Pivot Story Builder and our closed-loop flywheel."* |
| **0:35 - 1:10** | **F1: Resume Intake & Transferable Strengths (`/onboarding`)** | *"Click into Intake. When Elena uploads her teaching resume, PivotPilot doesn't just extract skills—it extracts Transferable Strengths. It bridges her past pedagogical diagnostic grading into executive data storytelling and churn gap analysis. An editable review screen allows instant corrections."* |
| **1:10 - 1:45** | **F2: Evidence-Based Skill Gap Map (`/skill-gaps`)** | *"Next, we benchmark her against 25 real Job Descriptions. PivotPilot calculates a mathematical Priority Score = Frequency × Importance × (1 − Proficiency). Clicking SQL reveals that it appears in 24 of 25 JDs (96%). We can inspect exact quotes from real postings in the Evidence Drawer."* |
| **1:45 - 2:15** | **F3: Adaptive Plan & F4: Domain Portfolio (`/plan` & `/projects`)** | *"PivotPilot converts those gaps into an 8-week curriculum with strict prerequisite ordering—SQL joins before BI dashboards. In Projects, instead of generic Iris flower datasets, Elena builds an EdTech Diagnostic Retention Predictor, leveraging her teaching credibility. The system outputs copyable STAR resume bullets and a generated GitHub README."* |
| **2:15 - 2:40** | **F5: Mock Interviews with 6D Rubric (`/interviews`)** | *"In the Mock Interview Room, Elena practices answering 'Why transition from teaching to data analytics?' The system scores her across our transparent 6-dimension rubric (Relevance, STAR, Technical Accuracy, Specificity, Communication, Pivot Narrative). It quotes her exact words, shows what a 5/5 needs, and generates an adaptive follow-up question."* |
| **2:40 - 3:00** | **F6 & F7: Adaptive Engine & Bayesian Insights (`/progress` & `/applications`)** | *"Finally, our closed loop: In the Application Tracker (15 tracked apps), our Bayesian engine reveals that Referral applications achieve 4.1x higher response rates, while Senior titles yielded 0/4 responses. The Adaptive Engine flags this, automatically reprioritizing Elena's syllabus. Every screen ends with a Next Best Action."* |

---

## 🔒 6. Data Privacy & Ethical AI Standards

- **Automatic PII Scrubbing**: Strips emails, phone numbers, and street addresses before any payload is sent to language models.
- **Explainable Statistics**: Statistical rates use Beta-Binomial Bayesian shrinkage to avoid small-sample distortions (e.g. 1/1 = 100%).
- **Deterministic Priority Calculations**: Priority scores and completion rates are computed directly in TypeScript code; LLMs are utilized solely for synthesis and explanation.
- **One-Click Reset**: Click "Reset Demo Data" in the header at any time to return the database to the clean seeded state.
