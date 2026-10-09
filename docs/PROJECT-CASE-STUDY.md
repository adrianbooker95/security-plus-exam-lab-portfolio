# Project Case Study — Security+ Exam Lab

**Project:** Security+ Exam Lab — Zero-Trust Protected Exam Simulator  
**Role:** Personal project: application development, cloud security configuration, testing, documentation, and release verification  
**Deployment:** Protected Cloudflare Pages site, Version 1.0 deployed October 2026  
**Portfolio focus:** Cloud Security · Identity and Access Management · API Authorization · Secure Data Storage · Testing

## 1. The problem I wanted to solve

I was preparing for the Security+ certification and wanted an exam simulator that would:
- Offer realistic timed and study experiences.
- Let me flag difficult questions, study the explanations, and review missed questions.
- Preserve active progress and results history.
- Let me study on my computer, tablet, or phone without accidentally overwriting answers.
- Keep purchased training materials private and separate from cloud-synchronized records.

I also wanted hands-on practice designing and operating a **protected cloud application**, not just another practice-test page.

## 2. Requirements and planning

I separated the design into five areas:

| Requirement | Implementation |
|---|---|
| Exam experience | JavaScript browser app with Timed/Study modes, question navigation, flags, explanations and results |
| Identity | Cloudflare Access policy protecting Preview and Production |
| Secure API | Cloudflare Pages Functions that verify signed Access identity tokens before data access |
| Persistence | Per-account D1 exam state and optimistic revision checks |
| Content licensing | Locally imported personal PDFs in browser storage; cloud sends only progress, not copyrighted content |

I used `exam-preview` to validate changes before the approved release to `main`. GitHub Actions helped catch regressions before deployment.

## 3. Build sequence

### Phase A — Build the foundation
1. Set up the GitHub application project and Cloudflare Pages.
2. Built a responsive exam menu and original, independently authored demonstration exercises.
3. Added Timed and Study modes, answer checking, navigation, flags, explanations, and result history.

### Phase B — Add cloud security
4. Configured Cloudflare Access-protected application hostnames for Preview and Production.
5. Created the D1 progress table and bound the database to Cloudflare Pages Functions.
6. Added API-side checks for Access JWT signature, issuer, audience, expiration, and authorized identity.
7. Kept account-scoped D1 progress independent of the browser's locally stored study documents.

### Phase C — Support realistic studying
8. Created a local PDF import/indexing workflow for legally acquired personal study materials.
9. Added support for multiple question banks and source-answer study references.
10. Built and refined interactive visual PBQ fields and kept scoring transparent: verified MCQs are automatically graded; graphical PBQs receive manual review and optional partial-credit entries.

### Phase D — Protect state across devices
11. Stored answer selections, flags, attempt metadata and result identifiers in D1.
12. Added revision-aware writes so older device state could not silently overwrite newer progress.
13. Tested conflict scenarios and cross-device synchronization logic with automated fixtures and real device checks.

### Phase E — Test and release
14. Ran nine automated regression suites and reviewed PBQ presentation.
15. Reviewed Production Cloudflare Access settings and D1 binding.
16. Deployed the approved engine to Production from the GitHub `main` branch.
17. Verified the Production site was accessible to the authorized account, showed `Synced`, retained five previous attempts, and matched Preview's cloud connection/test signal.

## 4. A difficult problem and how I handled it

**Challenge — outdated device state.** If I answered questions on a computer and later opened an older session on a tablet, a simple 'last write wins' design could lose the newer answers.

**Solution.** I used optimistic version numbers and conflict-aware reconciliation. On conflict, the app compares saved attempt records rather than overwriting the latest D1 row blindly. Completed-attempt timestamps also guard against reopening finished attempts from stale tabs.

**Security lesson.** Reliability and security overlap: preserving record integrity is just as important as restricting who can read it.

## 5. How I protected the project

- Cloudflare Access restricted entry to approved identities.
- Backend API checks validated the signed JWT instead of trusting a visible sign-in page.
- D1 reads and writes were scoped to the verified account.
- Same-origin checks and input validation guarded write requests.
- Browser-local PDF storage prevented copyrighted study pages from becoming hosted GitHub or cloud database records.
- The optional Cloudflare R2 PDF-upload path stayed disabled because third-party storage requires appropriate rights.

See the [security architecture](SECURITY-ARCHITECTURE.md) for more detail.

## 6. Results I verified

| Measure | Verified result |
|---|---|
| Private practice imports | Three 90-question exams: 85 MCQs plus five visual PBQs each |
| Other personally imported study content | 611-question test engine and 1,003-page study guide |
| Interactive exam layouts | Fifteen A/B/C PBQ layouts reviewed and approved |
| Automated validation | Nine regression suites passed at release |
| Production | Cloudflare Pages `main` deployment successful |
| Data continuity | Existing five exam attempts shown after release |
| Synchronization | Production and Preview connection identifiers and test signals matched |

**Important:** The commercially purchased questions and answer pages are **not** stored in this portfolio. This is not an independent audit of all licensed question text and is not an official CompTIA exam score.

## 7. Skills demonstrated

Identity and access management (IAM), Zero Trust access, signed-token verification, cloud security, API authorization, data minimization, client/server data consistency, GitHub version control, CI/CD, user acceptance testing, incident-style troubleshooting, and technical documentation.

## 8. What I'd improve next

- Extend real-browser automated end-to-end testing.
- Review dependency hardening and browser content-security policy.
- Improve keyboard/screen-reader accessibility.
- Consider a completely original, safely public live demonstration if separately approved.
- Expand concise evidence screenshots for original demonstration PBQ interactions.

## 9. Where the evidence lives

- [Screenshot walkthrough](SCREENSHOT-WALKTHROUGH.md) — historical build steps and sanitized Production evidence
- [Security architecture](SECURITY-ARCHITECTURE.md) — how boundaries and authorization work
- [Testing and results](TESTING-AND-RESULTS.md) — what was verified and what remains untested
- [Interview guide](INTERVIEW-GUIDE.md) — how to explain the project in practical terms

The live engine and purchased materials remain private; this public case study intentionally describes the work without publishing protected content.
