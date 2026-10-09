# Security+ Exam Lab — Simple Interview Guide

## 30-second version

> I built a private Security+ practice exam website using JavaScript and Cloudflare. I secured it with Cloudflare Access, verified user identities at the API, and used Cloudflare D1 to synchronize answers and scores across devices. I added automated GitHub tests and kept purchased PDFs local for privacy. The project helped me practice cloud security, identity and access management, and secure application development.

## 60–90-second version

> I wanted a realistic Security+ study website that worked on my computer, tablet, and phone while saving my progress. So I developed a web app with Timed and Study modes, interactive practice activities, answer explanations, review flags, and results history.
>
> I deployed the app through Cloudflare Pages and protected it with Cloudflare Access. More importantly, the backend verifies signed identity tokens before accessing exam progress, so one account can't simply request another account's results.
>
> I used Cloudflare D1 to synchronize progress and wrote conflict-handling logic to stop an old device from overwriting newer answers. I also kept purchased PDF materials on each browser rather than uploading them into my application database or public code repository.
>
> I tested the application with GitHub Actions, reviewed its practice exercises, then verified the Production deployment and confirmed my earlier results and cloud synchronization still worked.
>
> This project gave me practical experience in Zero Trust access, IAM, API security, cloud data storage, testing, and troubleshooting.

## Five questions you may get

### 1. What problem did you solve?
I wanted reliable exam practice across multiple devices, with a secure place to save progress and results.

### 2. What was your security approach?
I protected the website with Cloudflare Access, but I also validated the signed identity token on every progress API request and limited database operations to the authenticated account.

### 3. What was the hardest issue?
Preventing older browser sessions from overwriting newer exam progress. I used version-aware updates and conflict-reconciliation logic.

### 4. How did you test it?
I ran automated UI, parsing, API authorization, and synchronization tests. I also checked the live Production deployment, cloud status, and previously saved history.

### 5. What would you improve next?
More end-to-end browser automation, accessibility testing, and stronger browser dependency/security policies.

## How to connect this to a cybersecurity analyst role

I would emphasize three lessons:

- **Verify identity at the backend**, not just the login screen.
- **Minimize data exposure** by keeping licensed documents separate from cloud progress.
- **Protect data integrity** with conflict handling, regression tests, and non-destructive release checks.

## Résumé-ready bullet

Designed and deployed a protected Cloudflare-based Security+ exam simulator using Zero Trust access controls, JWT-verified APIs, D1 cross-device progress synchronization, browser-local document storage, and GitHub Actions regression testing.

## Interview boundaries

This is a personal, independently developed engineering project—not a CompTIA-endorsed exam service. The public portfolio contains no exam questions from purchased PDFs, no private credentials, and no unrestricted live application link.
