# Testing and Production Verification

## What I tested

This project combined **automated tests**, **manual UI acceptance**, and **live Cloudflare checks**. I distinguish them because passing simulated tests does not automatically prove a real cloud deployment works.

### Automated regression coverage

Nine GitHub Actions test suites were run on the application release branch:

| Test focus | What it checks |
|---|---|
| Application validation | JavaScript parsing, internal references, original demo data structure |
| UI smoke testing | Exam selection, navigation, study/timed states and result screens |
| Cloud API security | JWT requirements, invalid requests, D1 persistence and conflicting revisions |
| Cross-device simulation | Answer/flag/resume/complete reconciliation using simulated clients |
| Optional R2 API tests | Permission gate and isolation behaviors in mock tests; **not an authorized live PDF upload** |
| PDF parsing | Structural parser behavior using synthetic fixtures |
| Interactive PBQ layouts | Question-specific field/layout rules and regression checks |
| Original test-bank importer | Parser behavior with sanitized/synthetic test inputs |
| Study guide handling | Indexing and document-viewer regression logic |

These checks passed before Version 1.0. Test fixtures did **not** publish the purchased PDF materials.

### Manual acceptance

- Exam A, B, C question indexing: 90 questions each, including five manually reviewed visual PBQs.
- Interactive PBQ field placement and separate question-specific layouts were reviewed and approved.
- Timed and Study modes, explanations, flags, and results history were accepted in the private app.
- Exact answer grading boundary checked: 85 auto-graded MCQs, five manually reviewed PBQs on a full 90-item exam.
- Existing attempt history was examined; prior MCQ-only attempts were not mistaken for a completed full-exam result.

### Production verification

1. Cloudflare Pages deployment showed success for the `main` release.
2. Production had its expected D1 binding `DB` and names of Access configuration variables.
3. The authorized learner loaded the protected Production exam homepage and observed `Synced`.
4. Five existing exam attempts remained listed in Production Results History.
5. Preview and Production displayed matching Connection IDs and synchronized test signals in the original private verification session.
6. Locally importing the purchased practice PDF resulted in A/B/C each showing 85 verified MCQs and five visual PBQs.

## What these checks do *not* prove

- They do not certify exam readiness or an official CompTIA scaled score.
- They do not provide licensed question or explanation content for public consumption.
- They do not establish that all possible mobile browsers, all accessibility scenarios, or every graphical PBQ grading rubric have been exhaustively tested.
- They do not prove that Cloudflare R2 document uploads are authorized or active; those uploads remain disabled for licensed content.
- They do not imply that demonstration questions and personally imported licensed banks are the same assets.

## Release outcome

**Version 1.0: privately deployed, owner-verified.** After release, the app retained synchronized account history and supported per-device PDF import. This public portfolio contains documentation and sanitized evidence only.

See [project case study](PROJECT-CASE-STUDY.md) and [screenshot walkthrough](SCREENSHOT-WALKTHROUGH.md).
