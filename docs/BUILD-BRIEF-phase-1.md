# ConVo Neighborhood Platform: Build Brief, Phase 1

This brief is the hand-off for Claude Code. Build Phase 1 in this repository: the login and registration system for the website's back end, plus the first version of the digital handbook that stays in sync with Google.

## 1. Who this is for

ConVo Neighborhood (CVN) is a branding and consulting firm in Austin, Texas, moving into software engineering. Its public site is https://convoneighborhood.com. The owner is a beginner developer, so keep setup steps simple and explain every command.

## 2. Source of truth (Google)

Everything is planned in Google first. Read these before building:

| What | Link |
|---|---|
| System Setup (build blueprint: Build Phases, Portal Login Map, Workstation Blueprint, Member Registry, Integrations & Data) | https://docs.google.com/spreadsheets/d/13vxvLJf9xPsm2L96mIgvuEucALEQvpy9Q55Ijw8wNnA/edit |
| OCD Handbook Map tab (master list of every handbook link and its status) | https://docs.google.com/spreadsheets/d/1krjnyLkdCZhWmQe65gqgzinzH-jHxSb3oQyqjhZho4c/edit#gid=2026112001 |
| CVN Handbook Map (Google Doc version of the same links) | https://docs.google.com/document/d/1Y5UxdRFR3IIy53UWCa1f_gPKtGQq5wkb1Zka90BIMZ0/edit |
| Contractor Handbook (original copy) | https://docs.google.com/document/d/1AgBkQniX65al57uUuz0oefJCraO3T8KGdwul7tU2Z7s/edit |
| CVN Google Apps Master List | https://docs.google.com/spreadsheets/d/17SbsmfPbADYvzXTtjd3sncBnLd9el0w7BLdgz86pHuY/edit |
| ConVo Neighborhood Branding Blueprint Kit | https://docs.google.com/document/d/1ljGTFjCvGJ8c4ybDLctQLnK3A6ZwR_lpUw5Psw4UbLA/edit |

## 3. Suggested stack

- Next.js (App Router, TypeScript), deployed on Vercel from this GitHub repo.
- Supabase for the member database and authentication (Google sign-in, email and password, magic link). The System Setup sheet lists "Supabase or Google Firebase"; Supabase is suggested because roles and approvals fit Postgres row-level security. Confirm with the owner before starting.
- Domains are hosted on Hostinger; point the domain to Vercel when the site is ready.

## 4. Phase 1A: Login and registration

### Login dropdown and account types

Build one login page with a dropdown of account types, taken from the Portal Login Map tab:

| Login option | Who | Self-register | Approval before full access | Access level |
|---|---|---|---|---|
| Residents | Contractors, including SE trainees | Yes | Admin Assistant or Owner | Standard |
| Kinfolks | Partners, brand ambassadors, mentors | Yes | Admin Assistant or Owner | Standard |
| Neighbors | Clients, customers, prospects | Yes | Automatic for prospects; Admin confirms paying clients | Client |
| Job Seekers | Job seekers from any state or country (filed as Neighbors) | Yes | Automatic; moves to Neighbor once paying, Owner and Admin notified | Client |
| Admin Assistant | Owner's admin support | Yes | Owner | Elevated |
| C-Suite | Executive officers | Yes | Owner | Advanced |
| Board of Directors | Board members | Yes | Owner | Advanced |
| Part Owner | Co-owners | Yes | Owner | Executive |
| Owner | Firm owner | Set up at launch | None | Full control |

### Requirements

- Register and sign in with Google, regular email, or a password account.
- New accounts that need approval land in a "pending" state and see a waiting screen until approved.
- Approvals queue for the Owner and Admin Assistant, with email notifications.
- Each account type is routed to its own workstation dashboard (placeholder pages are fine in Phase 1; full workstations are Phase 2).
- Language switch in the header.
- Mirror new registrations to the System Setup "Member Registry" tab until the database is the only record (Google Sheets API with a service account).
- Security: row-level security per role, no secrets in the repo (use Vercel environment variables), and two-factor sign-in for Owner and Part Owner accounts.

## 5. Phase 1B: Digital handbook (first version)

The handbook must open like a real textbook or creative magazine, and stay current automatically.

- Data: read the OCD Handbook Map tab through the Google Sheets API. Only rows with Status = Confirmed appear in the handbook; rows with Status = Review stay hidden.
- Sections come from the "Handbook Section" column; each link opens the Google file.
- Original copy: pull the Contractor Handbook Google Doc (Docs API or export as HTML) and render it as chapters.
- Auto-update: revalidate on a schedule (for example every 15 minutes) plus a "refresh now" button for the Owner, so changes made in Google, or in the site's front end or back end, reach every contractor.
- Reader: cover page, table of contents, one chapter per page with page-turn navigation, a search box, and links to training and coursework at the end of each chapter (Coursera Tracker, textbooks).
- Gameboard at the top of the contractor workstation, linking to the handbook and training.
- Build it as a reusable handbook template so the same reader can publish handbooks for other groups (clients, partners, other businesses).
- Only signed-in Residents (and roles above them) can open the contractor handbook.

## 6. Brand

- Colors: gold tones and orange. The gold handshake coin is the official logo and must not be replaced.
- Style: 70s retro groove, bold, modern and creative with a "hippie side," while staying professional. See the Branding Blueprint Kit.
- The owner prefers the original cover page of the current site over a redesigned hero.

## 7. Done when

- A new user can register as any account type, sign in with Google or email, and reach the right placeholder workstation after approval.
- The Owner can approve or reject pending accounts.
- A signed-in Resident can open the digital handbook, see only Confirmed links grouped by section, and see changes from the OCD tab within the refresh window.
- Setup steps for Supabase, Google service account and Vercel are written in `docs/SETUP.md` in plain language.

## 8. Later phases (do not build yet)

Workstations, SE Training Hub with Claude mentor, Job Seeker Center and vision boards, integrations (payments, SuiteDash, transcripts) and the CVN Game. See the Build Phases tab.
