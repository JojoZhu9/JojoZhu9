# GitHub Portfolio Curation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the `JojoZhu9` profile and owned public repositories into an English-first academic engineering portfolio that remains useful to open-source developers and recruiters.

**Architecture:** Treat every repository as an independent delivery unit with its own clean checkout, focused documentation changes, metadata update, validation, commit, and push. The profile repository acts as the portfolio index; project repositories remain authoritative for setup, architecture, ownership, and contribution details.

**Tech Stack:** Git, GitHub CLI, GitHub Markdown, PowerShell, repository-native validation commands.

## Global Constraints

- Audience priority is mentors, then open-source developers, then recruiters.
- Documentation is English-first with concise Chinese support.
- Preserve team and course attribution; do not imply sole authorship.
- Do not add a new license without explicit owner approval.
- Do not expose API keys, runtime databases, local paths, or generated artifacts.
- Do not modify the dirty local GeniusQ directory at `C:\Users\iphon\Documents\智慧足迹-极智DAAS-实习`.
- Use one focused commit per repository and verify the GitHub default branch after each push.

---

### Task 1: Prepare Isolated Repository Checkouts

**Files:**
- Inspect only: `C:\Users\iphon\Documents\JojoZhu9-profile`
- Inspect only: `C:\Users\iphon\Documents\摸鱼小插件`
- Create checkout root: `C:\Users\iphon\Documents\GitHub-portfolio-work`

**Interfaces:**
- Consumes: GitHub repositories owned by `JojoZhu9`.
- Produces: Clean local checkouts for repository-specific tasks without touching unrelated user changes.

- [ ] **Step 1: Reconfirm protected working trees**

Run in each existing checkout:

```powershell
git status --short --branch
git remote -v
```

Expected: profile is ahead only by the approved specification/plan commits; PeekDock is clean; the original GeniusQ directory remains dirty and untouched.

- [ ] **Step 2: Create the isolated checkout root**

```powershell
New-Item -ItemType Directory -Force -Path 'C:\Users\iphon\Documents\GitHub-portfolio-work'
```

Expected: the directory exists and contains no user-authored project files before cloning.

- [ ] **Step 3: Clone clean project checkouts**

```powershell
gh repo clone JojoZhu9/geniusq-daas-platform 'C:\Users\iphon\Documents\GitHub-portfolio-work\geniusq-daas-platform'
gh repo clone JojoZhu9/COMP3030J-EcoSync 'C:\Users\iphon\Documents\GitHub-portfolio-work\COMP3030J-EcoSync'
gh repo clone JojoZhu9/COMP3011J-CityGo 'C:\Users\iphon\Documents\GitHub-portfolio-work\COMP3011J-CityGo'
gh repo clone JojoZhu9/smart-site-planner 'C:\Users\iphon\Documents\GitHub-portfolio-work\smart-site-planner'
```

Expected: every checkout is on `main`, tracks `origin/main`, and has a clean working tree.

- [ ] **Step 4: Record repository baselines**

Run `git status --short --branch`, `git log -1 --oneline`, and `rg --files` in each checkout. Stop on any unexpected local changes or remote mismatch.

---

### Task 2: Curate the GitHub Profile

**Files:**
- Modify: `C:\Users\iphon\Documents\JojoZhu9-profile\README.md`
- Create: `C:\Users\iphon\Documents\JojoZhu9-profile\README_ZH.md`

**Interfaces:**
- Consumes: verified project descriptions and repository URLs.
- Produces: the English portfolio landing page, concise Chinese companion, and account-level bio.

- [ ] **Step 1: Rewrite the English profile structure**

Keep the existing name, institution, email links, and factual technology list. Use these sections in order:

```markdown
# Hi, I'm Jiuzhou Zhu

Software Engineering student at Beijing-Dublin International College (BDIC),
building AI-assisted data systems, full-stack platforms, mobile applications,
and practical developer tools.

## Current Focus
## Selected Work
## Engineering Practice
## Technical Toolbox
## Collaboration
## Contact
## 中文简介
```

The `Selected Work` table must contain GeniusQ DaaS, EcoSync, Smart Site Planner, CityGo, and PeekDock in that order. Each row states the problem domain, verifiable engineering evidence, and main stack. The collaboration section links `sheldonlecc/COMP2008J-Forbidden_Island` without claiming ownership.

- [ ] **Step 2: Add the concise Chinese profile**

Create `README_ZH.md` with:

```markdown
# 朱九州

北京都柏林国际学院软件工程专业学生，关注 AI 辅助数据系统、全栈平台、移动应用与实用开发工具。

## 当前方向
## 代表项目
## 工程实践
## 联系方式
```

Link back to `README.md` at the top. Keep project order and ownership wording consistent with the English page.

- [ ] **Step 3: Validate profile content**

```powershell
rg -n "GeniusQ|EcoSync|Smart Site Planner|CityGo|PeekDock|Forbidden Island" README.md README_ZH.md
rg -n "TODO|TBD|yourusername|localhost" README.md README_ZH.md
git diff --check
```

Expected: all six referenced projects appear appropriately; the placeholder scan returns no matches; `git diff --check` returns no output.

- [ ] **Step 4: Update GitHub account and repository metadata**

```powershell
gh api --method PATCH user -f bio='Software Engineering student building AI-assisted data systems, full-stack platforms, mobile apps, and practical developer tools.'
gh repo edit JojoZhu9/JojoZhu9 --description 'Academic engineering portfolio: AI-assisted data systems, full-stack platforms, mobile apps, and developer tools.' --add-topic github-profile --add-topic portfolio --add-topic software-engineering
```

Expected: the account bio and profile-repository description match the README focus; institution and location remain unchanged.

- [ ] **Step 5: Commit the profile update**

```powershell
git add README.md README_ZH.md docs/superpowers/specs/2026-07-21-github-portfolio-design.md docs/superpowers/plans/2026-07-21-github-portfolio-curation.md
git commit -m "docs: curate academic engineering profile"
git push origin main
```

Expected: push succeeds and `git status --short` is empty.

---

### Task 3: Polish GeniusQ DaaS

**Files:**
- Modify: `README.md`
- Create: `CONTRIBUTING.md`
- Create: `SECURITY.md`
- Create: `.github/ISSUE_TEMPLATE/bug_report.md`
- Create: `.github/ISSUE_TEMPLATE/feature_request.md`
- Create: `.github/PULL_REQUEST_TEMPLATE.md`

**Interfaces:**
- Consumes: existing FastAPI, React, SQLite, DeepSeek, tests, screenshots, and `start-demo.ps1` behavior.
- Produces: mentor-readable project framing and a complete contributor entry path.

- [ ] **Step 1: Improve README navigation and status**

Add an English-first opening summary before the bilingual body with badges for Python, FastAPI, React, TypeScript, and license status `No license`. Add a compact navigation block linking English, Chinese, screenshots, quick start, architecture, and testing. State clearly that the project is a local demonstration, offline mode works without an API key, and DeepSeek mode requires the user's own key.

- [ ] **Step 2: Add contribution guidance**

`CONTRIBUTING.md` must include environment setup, backend tests, frontend tests, frontend build, small focused pull requests, no committed secrets, and the commands:

```powershell
python -m pytest backend/tests -q
npm --prefix frontend run test:run
npm --prefix frontend run build
```

- [ ] **Step 3: Add security and community templates**

`SECURITY.md` must direct private reports to `jiuzhou.zhu@ucdconnect.ie`, prohibit real production data in reports, and identify API-key exposure, unsafe SQL execution, and dependency vulnerabilities as sensitive issues. Issue templates request reproduction steps and environment details; the PR template requires tests, screenshots for UI changes, and a secret scan confirmation.

- [ ] **Step 4: Validate documentation and native tests**

```powershell
rg -n "offline|DeepSeek|API key|pytest|test:run|npm --prefix frontend run build" README.md CONTRIBUTING.md SECURITY.md
rg -n "TODO|TBD|yourusername" README.md CONTRIBUTING.md SECURITY.md .github
git diff --check
python -m pytest backend/tests -q
npm --prefix frontend install
npm --prefix frontend run test:run
npm --prefix frontend run build
```

Expected: placeholder scan has no matches, diff check is clean, and repository-native tests/build pass. Record any environment-only failure without changing claims.

- [ ] **Step 5: Update GitHub metadata**

```powershell
gh repo edit JojoZhu9/geniusq-daas-platform --description 'A local intelligent data query platform with Text-to-SQL, schema-aware retrieval, SQL guardrails, and dashboards.' --add-topic fastapi --add-topic react --add-topic typescript --add-topic sqlite --add-topic text-to-sql --add-topic deepseek --add-topic data-visualization
```

- [ ] **Step 6: Commit and push**

```powershell
git add README.md CONTRIBUTING.md SECURITY.md .github
git commit -m "docs: polish GeniusQ repository experience"
git push origin main
```

Expected: push succeeds and the worktree is clean.

---

### Task 4: Polish EcoSync

**Files:**
- Modify: `README.md`
- Modify: `README_CN.md`
- Create: `CONTRIBUTING.md`
- Create: `SECURITY.md`
- Create: `.github/ISSUE_TEMPLATE/bug_report.md`
- Create: `.github/ISSUE_TEMPLATE/feature_request.md`
- Create: `.github/PULL_REQUEST_TEMPLATE.md`

**Interfaces:**
- Consumes: existing Spring Boot, Vue, MySQL, Docker Compose, CI/CD, screenshots, test accounts, and team context.
- Produces: a clearly attributed flagship course-project page and contributor workflow.

- [ ] **Step 1: Tighten the README opening**

Keep English first and preserve the bilingual links. Add a concise course/team statement near the title, a project-status note, and badges for Java 17, Spring Boot, Vue 3, MySQL, Docker, and license status `No license`. Ensure the English and Chinese pages describe the same role-based workflows, test accounts, startup commands, and deployment boundaries.

- [ ] **Step 2: Add team-aware contribution and security files**

`CONTRIBUTING.md` must state that EcoSync is a group course project, request scoped changes, and list backend/frontend validation commands. `SECURITY.md` must cover test credentials, JWT/authentication issues, object storage, deployment secrets, and private reporting to `jiuzhou.zhu@ucdconnect.ie`. Templates must request affected role, reproduction steps, migration impact, tests, and screenshots where relevant.

- [ ] **Step 3: Validate documentation and project commands**

```powershell
rg -n "group|course|Docker Compose|mvnw|vitest|test account" README.md README_CN.md CONTRIBUTING.md SECURITY.md
rg -n "TODO|TBD|yourusername" README.md README_CN.md CONTRIBUTING.md SECURITY.md .github
git diff --check
.\mvnw.cmd test -B
npm --prefix ecosync-frontend install
npm --prefix ecosync-frontend run build
npm --prefix ecosync-frontend exec -- vitest run --reporter=verbose
```

Expected: documentation checks pass; native test/build results are recorded accurately.

- [ ] **Step 4: Update GitHub metadata**

```powershell
gh repo edit JojoZhu9/COMP3030J-EcoSync --description 'A full-stack near-expiry inventory and ordering platform built with Spring Boot, Vue 3, MySQL, and Docker Compose.' --add-topic spring-boot --add-topic vue3 --add-topic typescript --add-topic mysql --add-topic docker-compose --add-topic inventory-management --add-topic full-stack
```

- [ ] **Step 5: Commit and push**

```powershell
git add README.md README_CN.md CONTRIBUTING.md SECURITY.md .github
git commit -m "docs: polish EcoSync repository experience"
git push origin main
```

Expected: push succeeds and the worktree is clean.

---

### Task 5: Polish CityGo

**Files:**
- Modify: `README.md`
- Modify: `README_CN.md`
- Create: `CONTRIBUTING.md`
- Create: `SECURITY.md`
- Create: `.github/ISSUE_TEMPLATE/bug_report.md`
- Create: `.github/ISSUE_TEMPLATE/feature_request.md`
- Create: `.github/PULL_REQUEST_TEMPLATE.md`

**Interfaces:**
- Consumes: existing Android app, Google Maps integration, Room persistence, screenshots, APK link, and team attribution.
- Produces: a safer and easier-to-evaluate mobile project page without changing its rights statement.

- [ ] **Step 1: Clarify project status and configuration**

Add a compact status block and badges for Android, Java, Google Maps, Room, and `All rights reserved`. Keep the course/group line and contributor table. State that users must supply restricted API keys and that the external APK is a convenience artifact rather than a reproducible release guarantee.

- [ ] **Step 2: Add rights-compatible community files**

`CONTRIBUTING.md` must say contributions require maintainer acceptance and do not grant a general license to reuse the project. `SECURITY.md` must cover exposed API keys, unrestricted Google Maps credentials, AI service credentials, and private reporting. Templates must request Android version, device/emulator, reproduction steps, logs with secrets removed, and screenshots for UI changes.

- [ ] **Step 3: Validate links, ignored files, and Android build**

```powershell
rg -n "All rights reserved|Google Maps|API key|gradlew|Contributors" README.md README_CN.md CONTRIBUTING.md SECURITY.md
rg -n "google_maps_api|local.properties" .gitignore app/.gitignore README.md README_CN.md
rg -n "TODO|TBD|yourusername" README.md README_CN.md CONTRIBUTING.md SECURITY.md .github
git diff --check
.\gradlew.bat assembleDebug
```

Expected: rights and secret guidance are consistent, placeholder scan is empty, and the Android build passes when the local SDK is available.

- [ ] **Step 4: Update GitHub metadata**

```powershell
gh repo edit JojoZhu9/COMP3011J-CityGo --description 'An Android city-walk planner with Google Maps routing, AI-assisted itineraries, Room persistence, and budget tracking.' --add-topic android --add-topic java --add-topic google-maps --add-topic room-database --add-topic travel-planner --add-topic mobile-app
```

- [ ] **Step 5: Commit and push**

```powershell
git add README.md README_CN.md CONTRIBUTING.md SECURITY.md .github
git commit -m "docs: polish CityGo repository experience"
git push origin main
```

Expected: push succeeds and the worktree is clean.

---

### Task 6: Repair and Polish Smart Site Planner

**Files:**
- Modify: `README.md`
- Modify: `README_ZH.md`
- Rename: `requirement.txt` to `requirements.txt`
- Modify: `.gitignore`
- Remove from version control if tracked: `.idea/`, `__pycache__/`, `src/__pycache__/`
- Create: `CONTRIBUTING.md`
- Create: `SECURITY.md`
- Create: `.github/ISSUE_TEMPLATE/bug_report.md`
- Create: `.github/ISSUE_TEMPLATE/feature_request.md`
- Create: `.github/PULL_REQUEST_TEMPLATE.md`

**Interfaces:**
- Consumes: existing Python solver, Streamlit visualizer, CSV workflow, screenshots, and `test_main.py`.
- Produces: correct setup documentation, clean repository tracking, and an open collaboration path without adding a license.

- [ ] **Step 1: Verify actual commands and source paths**

Inspect `main.py`, `src/config.py`, `src/solver.py`, `src/visualizer.py`, `test_main.py`, and `requirement.txt`. Record the actual input columns, default data path, generated outputs, dashboard command, and test command before editing claims.

- [ ] **Step 2: Normalize the dependency filename and ignores**

Use `git mv requirement.txt requirements.txt`. Ensure `.gitignore` includes:

```gitignore
.idea/
__pycache__/
*.py[cod]
.pytest_cache/
.venv/
venv/
data/output_*.csv
logs/
```

Remove tracked IDE/cache files from Git's index while leaving any unrelated local files alone.

- [ ] **Step 3: Rewrite English-first setup and architecture documentation**

Correct the clone command to:

```bash
git clone https://github.com/JojoZhu9/smart-site-planner.git
cd smart-site-planner
pip install -r requirements.txt
```

Document the actual CSV schema, configuration path `src/config.py`, solver command, Streamlit command, generated files, algorithm stages, limitations, tests, and existing screenshots. Mirror the factual content in `README_ZH.md` with Chinese navigation.

- [ ] **Step 4: Add community and security files**

Contribution guidance must require a reproducible sample dataset with no private location data, tests for algorithm changes, and screenshots for visualization changes. Security guidance must cover sensitive POI/location datasets, credentials, and dependency issues. Issue templates must request sample schema, command, traceback, expected coverage behavior, and environment.

- [ ] **Step 5: Validate repository hygiene and tests**

```powershell
rg -n "yourusername|requirement\.txt|Edit `config\.py`|TODO|TBD" README.md README_ZH.md CONTRIBUTING.md SECURITY.md .github
git ls-files | Select-String -Pattern '(^|/)(\.idea|__pycache__)/'
git diff --check
python -m pip install -r requirements.txt
python -m pytest test_main.py -q
```

Expected: placeholder and stale-name scans return no matches; no IDE/cache files remain tracked; diff check is clean; tests pass in the available Python environment.

- [ ] **Step 6: Update GitHub metadata**

```powershell
gh repo edit JojoZhu9/smart-site-planner --description 'A Python and Streamlit system for delivery-site optimization, coverage analysis, and interactive visualization.' --add-topic python --add-topic streamlit --add-topic optimization --add-topic geospatial --add-topic data-visualization --add-topic site-planning
```

- [ ] **Step 7: Commit and push**

```powershell
git add README.md README_ZH.md requirements.txt .gitignore CONTRIBUTING.md SECURITY.md .github
git add -u
git commit -m "docs: repair and polish site planner repository"
git push origin main
```

Expected: push succeeds and the worktree is clean.

---

### Task 7: Audit PeekDock and Final Portfolio Consistency

**Files:**
- Inspect: `C:\Users\iphon\Documents\摸鱼小插件\README.md`
- Inspect: `C:\Users\iphon\Documents\摸鱼小插件\CONTRIBUTING.md`
- Inspect: `C:\Users\iphon\Documents\摸鱼小插件\SECURITY.md`
- Inspect: `C:\Users\iphon\Documents\摸鱼小插件\.github\`
- Modify only if a verified mismatch is found.

**Interfaces:**
- Consumes: all final GitHub metadata and profile project links.
- Produces: a consistent public portfolio and a final verification report.

- [ ] **Step 1: Run PeekDock validation**

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\tests\validate.ps1
& 'C:\Users\iphon\AppData\Local\Programs\AutoHotkey\v2\AutoHotkey64.exe' /ErrorStdOut /Validate .\PeekDock.ahk
git diff --check
```

Expected: both validators pass and the worktree remains clean. Make no commit if no mismatch exists.

- [ ] **Step 2: Verify all repository metadata through GitHub**

```powershell
gh repo list JojoZhu9 --limit 100 --json name,description,url,homepageUrl,repositoryTopics,isPrivate,isArchived
gh api users/JojoZhu9 --jq '{name,bio,company,location,public_repos}'
```

Expected: six public repositories are present; descriptions and topics match the approved design; the profile bio is populated; no visibility or archive state changed.

- [ ] **Step 3: Verify final branch state**

For every modified checkout, run:

```powershell
git status --short --branch
git log -1 --oneline
git ls-remote --heads origin main
```

Expected: worktrees are clean, local `main` tracks `origin/main`, and pushed commit IDs agree with the remote head.

- [ ] **Step 4: Produce the completion summary**

Report each repository's commit ID, pushed metadata, validation commands, any skipped build/test with reason, and any licensing decision still awaiting the owner.
