# WebAuditor — Product Plan

## 1. User Expectations

### 1.1 Speed & Reliability
- Audit results delivered with live progress per module
- No silent failures — clear error messages with retry option
- Consistent results across repeated runs on the same URL
- Async job queue for heavy audit tasks (no synchronous blocking)

### 1.2 Clarity of Results
- Overall score (0–100) with per-category breakdown
- Issues prioritized as: Critical / Warning / Info
- Each issue includes: title, affected element, why it matters, how to fix
- AI-generated actionable recommendations (specific, not generic)

### 1.3 History & Trends
- Full audit history per project/URL
- Score trend graph over time
- Side-by-side comparison of two audit runs

### 1.4 Reporting & Export
- Export to PDF (branded), Excel, CSV
- Shareable public report link (no login required)
- Optional password protection and expiry on shared links

### 1.5 Notifications & Alerts
- Email on audit completion
- Alert when score drops below a user-defined threshold
- Weekly/monthly digest emails
- Slack webhook support

### 1.6 Team & Access Management
- Team accounts with member invitations
- Role-based access: Admin / Editor / Viewer
- Per-project organization (group audits by website or client)

### 1.7 Developer API
- REST API with API key auth (per project)
- Webhook support for CI/CD integration
- Well-documented API reference at /docs/api

### 1.8 Trust & Transparency
- Explain how each audit check works
- Link to relevant standards (WCAG, Core Web Vitals, etc.)
- Show full list of what was checked, not just failures

---

## 2. Pages & UI Flows

### 2.1 Landing / Home
- Hero with URL input to start a free audit
- Feature highlights (Accessibility, Performance, SEO, Security, Mobile, AI)
- Pricing section
- CTA to sign up

### 2.2 Auth Pages
- Sign up (email + password, Google OAuth, GitHub OAuth)
- Login
- Forgot password / Reset password
- Email verification

### 2.3 Dashboard
- Overview of all projects
- Recent audits across all projects
- Quick-start: run new audit
- Score summary cards per project

### 2.4 New Audit Flow
```
Enter URL → Select audit modules → Submit
     ↓
Progress screen (live updates per module)
  [✓] Accessibility ... done
  [⟳] Performance  ... running
  [ ] SEO          ... queued
     ↓
Auto-redirect to Results page on completion
     ↓
If failed → Error card with reason + Retry button
```

### 2.5 Results Page
```
Overall Score: 78/100
  ┌──────────┬────────────┬──────┬──────────┐
  │ Access.  │ Perf       │ SEO  │ Security │
  │  85/100  │  70/100    │ 80/  │  76/100  │
  └──────────┴────────────┴──────┴──────────┘

Issues (prioritized):
  🔴 Critical (3)   → Fix these first
  🟡 Warnings (8)   → Should fix
  🔵 Info (12)      → Nice to have

Each issue card:
  Title | Affected element | Why it matters | How to fix

AI Recommendations section:
  Specific, context-aware suggestions ranked by impact
```

### 2.6 Project Dashboard
```
Project: "mysite.com"
  Score trend chart (line graph over time)
  
  Audit History table:
  Date       Score   Change   Actions
  Apr 04     78/100  ↑+5      [View] [Compare] [Delete]
  Mar 20     73/100  ↓-2      [View] [Compare] [Delete]
```

### 2.7 Compare Audits
- Side-by-side diff of two audit runs
- Score changes per category
- Issues resolved vs new issues introduced

### 2.8 Export & Share
```
Results page → [Export ▾]
                 PDF (branded)
                 Excel
                 CSV

              → [Share Report]
                 Generates public link (no login needed)
                 Optional: password protect
                 Optional: expiry date
```

### 2.9 Notifications Settings
```
Project Settings → Notifications
  Email on audit completion        [toggle]
  Alert if score drops below [70]  [toggle + input]
  Weekly digest [Monday ▾]         [toggle + select]
  Slack webhook URL                [input + test button]
```

### 2.10 Team Management
```
Account → Team
  Member list with roles (Admin / Editor / Viewer)
  Invite by email
  Change role / Remove member
```

### 2.11 API Keys
```
Settings → API Keys
  List of keys with name, prefix, last used
  Generate new key (with name)
  Revoke key

Docs link → /docs/api
```

### 2.12 Audit Module Detail Pages
- Accessibility (WCAG 2.1 AA/AAA breakdown)
- Performance (Core Web Vitals: LCP, FID, CLS, TTFB)
- SEO (meta, headings, canonicals, sitemap, robots.txt)
- Security (HTTPS, CSP, headers, mixed content)
- Mobile Responsiveness (viewport, tap targets, font sizes)
- Cross-Browser (caniuse compatibility flags)

---

## 3. Integrations

### 3.1 Auth & Identity
- [ ] Google OAuth 2.0
- [ ] GitHub OAuth 2.0
- [ ] JWT-based session management
- [ ] Auth0 or Clerk (optional managed auth)

### 3.2 Google Integrations
- [ ] Google Analytics API
- [ ] Google Search Console API
- [ ] Google Tag Manager API
- [ ] Google Ads API

### 3.3 Email & Notifications
- [ ] Nodemailer (transactional email, self-hosted SMTP)
- [ ] SendGrid (production email delivery)
- [ ] Slack webhooks

### 3.4 Export & Reporting
- [ ] puppeteer / pdfkit (PDF generation)
- [ ] exceljs (Excel export)
- [ ] CSV export (built-in)

### 3.5 Audit Engine Libraries
- [ ] axe-core (accessibility)
- [ ] pa11y (accessibility CLI)
- [ ] Lighthouse API (performance)
- [ ] Cheerio (SEO / HTML parsing)
- [ ] Puppeteer / Playwright (headless browser)
- [ ] caniuse-lite (cross-browser compat data)

### 3.6 AI Layer
- [ ] Claude API (Anthropic) — primary AI insights
- [ ] OpenAI API — fallback / secondary

### 3.7 Infrastructure & DevOps
- [ ] Redis (job queue + caching)
- [ ] BullMQ (async audit job processing)
- [ ] AWS S3 / Cloudflare R2 (report/export storage)
- [ ] Cloudflare (CDN + WAF + DDoS protection)
- [ ] Sentry (error tracking — frontend + backend)
- [ ] Datadog or New Relic (APM)
- [ ] UptimeRobot or Pingdom (uptime monitoring)

### 3.8 Payments
- [ ] Stripe (subscription billing)

### 3.9 Security
- [ ] reCAPTCHA or hCaptcha (protect audit form)
- [ ] Doppler or AWS Secrets Manager (secrets management)
- [ ] Rate limiting (audit API abuse prevention)

### 3.10 Developer & CI/CD
- [ ] GitHub Actions integration (run audits on deploy)
- [ ] Jira / Linear (auto-create issues from findings)
- [ ] REST API with API key auth
- [ ] Webhook support (push results to external systems)

---

## 4. Backend Architecture

### API Routes (planned)
```
POST   /api/v1/auth/register
POST   /api/v1/auth/login
POST   /api/v1/auth/logout
POST   /api/v1/auth/refresh

GET    /api/v1/projects
POST   /api/v1/projects
GET    /api/v1/projects/:id
DELETE /api/v1/projects/:id

POST   /api/v1/audits              → trigger audit
GET    /api/v1/audits/:id          → get results
GET    /api/v1/audits/:id/status   → poll status
GET    /api/v1/projects/:id/audits → audit history

POST   /api/v1/audits/:id/export/pdf
POST   /api/v1/audits/:id/export/excel
POST   /api/v1/audits/:id/export/csv
POST   /api/v1/audits/:id/share    → generate public link

GET    /api/v1/team
POST   /api/v1/team/invite
PATCH  /api/v1/team/:memberId/role
DELETE /api/v1/team/:memberId

GET    /api/v1/settings/api-keys
POST   /api/v1/settings/api-keys
DELETE /api/v1/settings/api-keys/:id

POST   /api/v1/webhooks
GET    /api/v1/webhooks
DELETE /api/v1/webhooks/:id
```

### Data Models (MongoDB)
```
User        → _id, name, email, passwordHash, role, teamId, createdAt
Team        → _id, name, ownerId, members[], plan, createdAt
Project     → _id, teamId, name, url, settings, createdAt
Audit       → _id, projectId, url, status, scores, issues[], aiInsights, createdAt
AuditJob    → _id, auditId, status, progress, error, createdAt
SharedReport→ _id, auditId, token, password, expiresAt, createdAt
ApiKey      → _id, teamId, name, keyHash, prefix, lastUsed, createdAt
Webhook     → _id, teamId, url, events[], secret, createdAt
```

---

## 5. Frontend Structure (Vue.js)

```
src/
  views/
    Home.vue
    auth/
      Login.vue
      Register.vue
      ForgotPassword.vue
      ResetPassword.vue
    dashboard/
      Dashboard.vue
      Project.vue
      NewAudit.vue
      AuditProgress.vue
      AuditResults.vue
      CompareAudits.vue
    settings/
      Team.vue
      ApiKeys.vue
      Notifications.vue
      Billing.vue
  components/
    audit/
      ScoreCard.vue
      IssueCard.vue
      ScoreTrendChart.vue
      AuditProgressTracker.vue
      AIInsightsPanel.vue
      ModuleBreakdown.vue
    shared/
      Navbar.vue
      Sidebar.vue
      ExportMenu.vue
      ShareReportModal.vue
  store/         → Pinia stores
  composables/   → reusable logic
  services/      → API call wrappers
```
