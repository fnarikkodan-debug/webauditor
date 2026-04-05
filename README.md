# WebAuditor

A comprehensive web auditing tool that helps analyze web pages for accessibility, performance, SEO, security, and more — with AI-powered insights and automated reporting.

## Architecture

```mermaid
graph TB
    subgraph Client["Frontend (Vue.js)"]
        UI[Dashboard / UI]
        AuditForm[Audit Form]
        Reports[Reports & History]
        Export[Export Module]
    end

    subgraph Gateway["API Gateway (Node.js / Express)"]
        REST[REST API]
        Auth[Auth Middleware\nJWT + bcrypt]
        RateLimit[Rate Limiter]
    end

    subgraph AuditEngine["Audit Engine (Node.js)"]
        Accessibility[Accessibility Auditor\naxe-core / pa11y]
        Performance[Performance Auditor\nLighthouse API]
        SEO[SEO Auditor\nCheerio]
        Security[Security Auditor\nHeaders / CSP / HTTPS]
        Mobile[Mobile Responsiveness\nPuppeteer / Playwright]
        CrossBrowser[Cross-Browser Checker\ncaniuse data]
    end

    subgraph AI["AI Layer"]
        AIInsights[AI Insights Engine\nClaude / OpenAI API]
        Recommendations[Recommendations Generator]
    end

    subgraph Integrations["Google Integrations"]
        GA[Google Analytics API]
        GSC[Google Search Console API]
        GTM[Google Tag Manager API]
        GAds[Google Ads API]
    end

    subgraph Notifications["Notification Service"]
        Email[Email Service\nNodemailer / SendGrid]
    end

    subgraph Reporting["Reporting Service"]
        PDF[PDF Generator\npuppeteer / pdfkit]
        Excel[Excel Generator\nexceljs]
        CSV[CSV Exporter]
    end

    subgraph DB["Database (MongoDB)"]
        Users[(Users)]
        Audits[(Audit Results)]
        History[(Audit History)]
        Config[(Configurations)]
    end

    subgraph HeadlessBrowser["Headless Browser"]
        Puppeteer[Puppeteer / Playwright]
    end

    UI --> REST
    AuditForm --> REST
    Reports --> REST
    Export --> REST

    REST --> Auth
    Auth --> RateLimit
    RateLimit --> AuditEngine
    RateLimit --> Reporting
    RateLimit --> Integrations

    AuditEngine --> Accessibility
    AuditEngine --> Performance
    AuditEngine --> SEO
    AuditEngine --> Security
    AuditEngine --> Mobile
    AuditEngine --> CrossBrowser

    Mobile --> Puppeteer
    Performance --> Puppeteer

    AuditEngine --> AIInsights
    AIInsights --> Recommendations

    AuditEngine --> DB
    Auth --> Users
    AuditEngine --> Audits
    Audits --> History

    Reporting --> PDF
    Reporting --> Excel
    Reporting --> CSV

    AuditEngine --> Notifications
    Notifications --> Email

    Integrations --> GA
    Integrations --> GSC
    Integrations --> GTM
    Integrations --> GAds
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vue.js |
| Backend | Node.js + Express |
| Database | MongoDB |
| Headless Browser | Puppeteer / Playwright |
| Accessibility | axe-core / pa11y |
| Performance | Lighthouse API |
| HTML Parsing | Cheerio |
| AI Insights | Claude / OpenAI API |
| Email | Nodemailer / SendGrid |
| PDF Export | puppeteer / pdfkit |
| Excel Export | exceljs |

## Features

1. Accessibility audit
2. Performance audit
3. SEO audit
4. Security audit
5. Mobile responsiveness audit
6. Cross-browser compatibility audit
7. AI-powered insights and recommendations
8. Automated reporting
9. User management
10. Audit history
11. Export to PDF, Excel, CSV
12. Email notifications
13. API for integration with other tools
14. Google Analytics integration
15. Google Search Console integration
16. Google Tag Manager integration
17. Google Ads integration
