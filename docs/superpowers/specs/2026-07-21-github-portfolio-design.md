# GitHub Portfolio Curation Design

## Objective

Curate the `JojoZhu9` GitHub profile and public repositories for three audiences, in this order:

1. Academic mentors evaluating technical depth, research interests, and reproducibility.
2. Open-source developers trying to understand, run, and contribute to the projects.
3. Recruiters reviewing engineering range and delivery quality.

The portfolio will be English-first with concise Chinese support. It will present team projects honestly and distinguish personal contributions from group outcomes.

## Scope

The work covers the profile repository and these owned public projects:

- `JojoZhu9/JojoZhu9`
- `JojoZhu9/geniusq-daas-platform`
- `JojoZhu9/COMP3030J-EcoSync`
- `JojoZhu9/COMP3011J-CityGo`
- `JojoZhu9/smart-site-planner`
- `JojoZhu9/peekdock`

`peekdock` has already received repository documentation and community files. It will only receive consistency fixes if the portfolio audit finds a concrete mismatch.

## Profile Design

The profile README will use a compact academic-engineering structure:

1. Identity, institution, and one-sentence engineering focus.
2. Current interests in AI-assisted data systems, full-stack platforms, mobile workflows, and optimization tools.
3. Selected projects grouped by domain, including PeekDock.
4. Evidence of engineering practice: reproducible setup, testing, safe data access, deployment, and documentation.
5. A concise technical toolbox grounded in technologies visible in the repositories.
6. Contact information and a link to a separate Chinese summary.

The English README remains the default. A `README_ZH.md` file will provide a shorter Chinese overview instead of duplicating every badge and table.

The GitHub account bio will be filled with a concise description aligned with the profile. Existing institution and location fields will be preserved. Public contact details already present in the README will not be expanded.

## Repository Tiers

### Tier 1: Flagship Systems

- `geniusq-daas-platform`
- `COMP3030J-EcoSync`

These repositories should make architecture, project status, screenshots, setup, tests, security constraints, and contribution paths easy to find. Their descriptions and topics should reflect the actual implementation.

### Tier 2: Focused Applications

- `COMP3011J-CityGo`
- `smart-site-planner`
- `peekdock`

These repositories should prioritize a clear problem statement, real screenshots where available, reliable setup commands, configuration guidance, known limitations, and verification instructions.

### Profile and Collaborative Work

The externally owned pinned repository `sheldonlecc/COMP2008J-Forbidden_Island` remains visible as collaboration evidence. It will not be modified as part of this work.

## Repository Standards

Each owned project will be audited against the following standards:

- An accurate GitHub description with no leading whitespace or vague wording.
- Relevant repository topics, avoiding broad or unsupported tags.
- A README that identifies the problem, audience, status, primary features, stack, setup, and verification path.
- English-first navigation with a Chinese companion where useful.
- Screenshots or real product media when they already exist or can be produced from the runnable project.
- Correct clone URLs, filenames, paths, commands, and dependency names.
- A `.gitignore` that excludes IDE files, caches, build output, runtime databases, and secrets.
- Community files appropriate to the repository: contribution guidance, issue templates, pull request template, and security reporting instructions.
- No invented performance claims, deployment claims, research results, or personal contribution claims.

## Project-Specific Work

### GeniusQ DaaS

- Preserve the detailed bilingual product documentation and screenshots.
- Improve the top-level summary, status, prerequisites, and navigation for faster scanning.
- Add accurate repository description and topics.
- Document offline mode and API-key handling prominently.
- Add community and security files where missing.

### EcoSync

- Preserve the course and team context.
- Improve the repository description and topics.
- Make architecture, demo accounts, Docker startup, tests, and deployment boundaries easy to scan.
- Ensure contribution wording does not imply sole authorship.
- Add community and security files where missing.

### CityGo

- Preserve team attribution and the existing all-rights-reserved statement.
- Improve repository metadata and topic coverage.
- Keep API-key risks and local configuration prominent.
- Check screenshot links, APK link, Gradle commands, SDK requirements, and ignored secret files.
- Add only community files compatible with the existing rights statement.

### Smart Site Planner

- Correct the placeholder clone URL and repository directory name.
- Resolve `requirement.txt` versus `requirements.txt` documentation inconsistency.
- Align the documented configuration path with the actual source tree.
- Remove tracked cache and IDE artifacts from version control when confirmed safe.
- Improve metadata, setup, data format, algorithm explanation, and test instructions.

### PeekDock

- Confirm profile links, description, topics, installation instructions, and validation workflow remain accurate.
- Avoid unrelated changes if the current repository already meets the common standard.

## Licensing and Ownership

No new open-source license will be added automatically.

- CityGo keeps its existing all-rights-reserved statement.
- Team and course repositories remain unlicensed unless their owners explicitly approve a license.
- Personal repositories may receive a license only after an explicit licensing decision.
- Documentation will not describe an unlicensed repository as open source merely because its source is public.

## GitHub Presentation

The six current pinned repositories provide a balanced view: one external collaboration and five owned projects. The profile README will order owned projects by relevance to mentors rather than repository creation date.

Recommended order in the README:

1. GeniusQ DaaS
2. EcoSync
3. Smart Site Planner
4. CityGo
5. PeekDock

## Verification

For each repository, verification will include:

- Inspecting the final diff before commit.
- Checking README relative links against repository paths.
- Running existing documentation or validation scripts when present.
- Running lightweight build or test commands when dependencies and runtimes are available locally.
- Confirming the pushed default branch, repository description, topics, and homepage fields through GitHub.
- Reporting any command that cannot be run and the remaining risk.

Each repository will receive its own focused commit so changes can be reviewed or reverted independently.

## Success Criteria

- A mentor can identify the user's technical interests and strongest work from the profile within 30 seconds.
- A developer can determine how to run each flagship project without searching through source code.
- Project descriptions, topics, README claims, and repository contents agree.
- Team projects clearly preserve course context and shared authorship.
- No secrets, generated caches, or unsupported claims are introduced.
- All modified repositories are pushed with clean working trees and verified GitHub metadata.
