# 🌟 InnerSource Program Guidelines (Baseline Framework)

## 1. Purpose

The purpose of this guideline is to define how internal software repositories and assets are classified, supported, and maintained within the engineering organization to enable sustainable reuse, collaboration, and innovation through inner sourcing.

All repositories are open for read access and available for individuals to create pull requests (PRs) against, encouraging transparency and collaboration. However, only repositories that meet defined asset standards are classified under Levels 1–3 as recognized **InnerSource Assets**; all other repositories remain open for contribution but are not treated as reusable assets.

It aligns with recognized open-source and inner-source norms (e.g., GitHub’s InnerSource Commons, Google’s Eng Productivity models, and Microsoft’s internal “OSS-style” programs).

---

## 2. Core Definitions

| Term | Definition |
|------|-------------|
| **InnerSource Asset** | A codebase, library, service, or infrastructure component intentionally shared across internal teams for reuse or contribution, meeting defined quality and support standards. |
| **Owner (Maintainer)** | The person or team responsible for stewardship of the repository’s roadmap, quality, and integration. |
| **Contributor** | Any engineer submitting changes, enhancements, or bug fixes under the repository’s contribution guidelines. |
| **Consumer** | Any team or system that depends on an InnerSource asset. |
| **Support Tier** | Defines expectations for responsiveness, maintenance, and quality assurance for an asset. |

---

## 3. Repository Classification Model

| Level | Description | Typical Use Case | Support Expectation | Ownership |
|-------|--------------|------------------|---------------------|------------|
| **Level 1 – Self-Managed / Experimental Asset** | Code shared “as-is.” No guaranteed support or roadmap. May be early stage, proof of concept, or team-specific tooling. | Internal experiment, niche automation | None (use at your own risk). Consumers should fork if critical. | Individual developer or team |
| **Level 2 – Developer-Managed (Reusable Asset)** | Any code or documentation asset that meets Level 2 quality. | Shared utilities, components, frameworks reused across squads | Limited support (e.g., best-effort issue response within 5 business days). Backward compatibility expected for stable releases. | A team consisting of at least two Maintainers. |
| **Level 3 – Organization-Endorsed (Strategic Asset)** | Highly reusable component or framework endorsed by the engineering organization. Governed for long-term sustainability and shared ownership, but not centrally hosted or operated. | Core frameworks, libraries, or patterns reused across multiple domains | Formal contribution process, roadmap transparency, and consistent quality. No uptime or SLA requirements; each consuming team deploys and operates independently. | Central engineering or cross-team maintainer group |

---

## 4. Quality and Engineering Standards (Baseline for Recognition)

To be formally recognized as an **InnerSource Asset** (Level 2+), the following **minimum standards** apply.

### 4.1. Code Quality

- Follows organization coding standards and naming conventions.
- Mandatory **code review by at least one maintainer** before merging.
- Static analysis, linting, and security scanning integrated in CI.
- **Automated unit test coverage ≥ 80% (target 90%+ for critical assets).**
- **SonarQube maintainability rating must be A** with zero blocker issues.
- Integration or end-to-end tests for key functionality.
- Repository must follow the **EET Code Asset Repository Template** or one of its approved language-specific derivatives to ensure structural and documentation consistency.

### 4.2. Documentation

- **README.md** including:
  - Overview, purpose, and intended use cases.
  - Installation / setup instructions.
  - Example usage.
  - Support contact or maintainer reference.
  - Contribution guidelines (`CONTRIBUTING.md`).
- **CHANGELOG.md** maintained for all public releases.
- **Architecture / Design Overview** for endorsed assets (e.g., diagrams, interfaces, dependencies).

### 4.3. Versioning & Releases

- Semantic Versioning (SemVer) used across all assets.
- Tagged releases with release notes.
- Deprecation and backward compatibility policy defined for public APIs.

### 4.4. Security & Compliance

- No embedded secrets or credentials.
- All dependencies scanned for vulnerabilities.
- License file present (`LICENSE.md`) clarifying internal usage rights.
- Follows internal threat modeling guidelines for exposed services.

---

## 5. Support & Contribution Expectations

| Category | Level 1 | Level 2 | Level 3 |
|-----------|----------|----------|----------|
| **Support Channel** | None / best effort | Issue tracker and internal chat channel | Defined communication and governance channel |
| **Response Time (Issues)** | No guarantee | ≤5 business days | Within defined contributor agreement timeframe |
| **Release Cadence** | Ad hoc | Quarterly or as needed | Regular, roadmap-driven cadence |
| **Deprecation Policy** | None | 1 minor version grace period | 2 minor versions grace period with communication |
| **Contribution Process** | Fork & PR (optional review) | PR with maintainer review | Structured contribution workflow with maintainers and reviewers |
| **Approval Rights** | Owner only | Maintainers | Steering or working group |
| **Visibility** | Internal only | Indexed in internal asset catalog | Featured / endorsed in engineering portal |

---

## 6. Endorsement Criteria (Recommended Assets)

Only assets meeting **Level 2 or higher** criteria will be **recognized and recommended** in the internal catalog or developer portal.

Baseline endorsement requires:

- Passing CI/CD quality gates.
- Conformance with documentation and testing standards.
- Identified maintainer(s) and support model.
- Security review approval for reuse.
- Listed under internal dependency and risk management processes.

---

## 7. Quality Maturity Ladder (Optional Internal Metric)

| Maturity | Description | Example KPI |
|-----------|--------------|--------------|
| **Bronze (Emerging)** | Meets minimal code & doc standards, not yet widely adopted. | 1+ consumers, basic tests |
| **Silver (Reusable)** | Stable API, multiple consumers, test coverage ≥80%. | ≥3 consumer teams |
| **Gold (Endorsed)** | High-quality reusable component, documented, and maintained collaboratively. | org-wide reuse, frequent contribution activity |

---

## 8. Governance and Lifecycle Management

- Each repository should declare whether it is an **InnerSource Asset**, along with its **owner**, **support level**, and **lifecycle status**: Active, Deprecated, or Archived.
- Governance board (InnerSource Working Group) will:
  - Periodically review compliance with standards.
  - Maintain the internal catalog / portal.
  - Recommend upgrades/downgrades in tier based on adoption and quality.
  - Sunset unused or abandoned assets.



---

## 9. Appendix: Promoting and Productizing Code into Recognized Assets

### 9.1. Purpose
This appendix outlines the process and technical considerations for extracting, refactoring, and maturing existing project code into reusable InnerSource Assets that can be shared across teams.

### 9.2. Identification
- **Assess candidate code**: Identify modules, libraries, or services within a project that provide generalizable functionality (e.g., authentication helpers, data mappers, configuration parsers, or reusable UI components).
- **Evaluate reusability**: Determine if the functionality is domain-neutral, stable, and beneficial to other teams.
- **Confirm ownership**: Assign at least two maintainers willing to steward the asset post-extraction.

### 9.3. Extraction
- **Isolate functionality** into its own repository or submodule with minimal external dependencies.
- **Refactor for separation of concerns**, ensuring the component is not tightly coupled to project-specific business logic.
- **Encapsulate configuration and dependencies**, moving project-specific details into external configuration or adapters.
- **Introduce clear interfaces** or APIs to enable multiple consumers to integrate the asset in varied contexts.

### 9.4. Refactoring for Extensibility and Configurability
- **Parameterize behaviors**: Replace hard-coded logic with configuration options, environment variables, or dependency injection.
- **Enable modular design**: Use plugin or strategy patterns to allow extension without modifying the core code.
- **Define versioned interfaces**: Stabilize public APIs to avoid breaking downstream consumers.
- **Document extension points**: Clearly describe how teams can extend or customize behavior safely.

### 9.5. Quality and Documentation Requirements
- Add full documentation per Section 4, including clear examples and integration guidance.
- Establish automated tests that validate independent operation (unit and integration coverage).
- Ensure backward compatibility for any previously dependent internal systems.
- Perform dependency review and security scan prior to catalog registration.

### 9.6. Promotion Process
1. **Nominate**: Maintainers submit a nomination to the InnerSource Working Group, outlining purpose, consumers, and ownership.
2. **Review**: The working group evaluates quality, test coverage, and documentation against Level 2 criteria.
3. **Endorse**: If accepted, the repository is classified as an InnerSource Asset and listed in the internal catalog.
4. **Monitor**: Maintain metrics (adoption, contribution frequency, issue activity) to sustain classification.

### 9.7. Benefits
- Reduces duplication of effort across teams.
- Promotes consistency and quality across codebases.
- Encourages ownership, collaboration, and discoverability of well-engineered components.
- Provides a path for evolving successful solutions from project-specific implementations to shared organizational assets.


### 9.8. Nomination Checklist Template
Teams preparing to nominate a repository for InnerSource Asset classification should complete the following checklist:

**Basic Information**
- [ ] Repository name and URL
- [ ] Proposed Level (1, 2, or 3)
- [ ] Primary maintainers (at least two)
- [ ] Short description of purpose and functionality

**Code Quality and Testing**
- [ ] Code follows organizational standards and naming conventions
- [ ] Code reviews performed for all merges
- [ ] Static analysis, linting, and security scanning enabled
- [ ] Unit test coverage ≥70%
- [ ] Integration tests implemented for critical paths

**Documentation**
- [ ] `README.md` includes overview, setup, and usage examples
- [ ] `CONTRIBUTING.md` outlines PR and review process
- [ ] `CHANGELOG.md` maintained for each release
- [ ] API or interface documentation provided

**Architecture and Extensibility**
- [ ] Component decoupled from project-specific logic
- [ ] Configuration and dependencies externalized
- [ ] Extension points documented
- [ ] Public interfaces versioned and stable

**Security and Compliance**
- [ ] Secrets removed and stored securely
- [ ] Dependency vulnerabilities scanned and remediated
- [ ] `LICENSE.md` present clarifying internal usage rights

**Governance and Ownership**
- [ ] Maintainers agree to ongoing stewardship and responsiveness
- [ ] Contribution model established (PR workflow, issue triage)
- [ ] Lifecycle status defined (Active, Deprecated, or Archived)

Once all boxes are checked and evidence documented, teams can submit the nomination form to the InnerSource Working Group for review and potential endorsement.

---

## 10. Review and Award Program for InnerSource Excellence

### 10.1. Purpose
To recognize and reward teams and contributors who create high-impact, high-quality InnerSource assets that demonstrate exceptional reusability, adoption, and engineering rigor. This program promotes healthy competition, continuous improvement, and pride in craftsmanship across the organization.

### 10.2. Evaluation Cadence
The InnerSource Working Group will conduct **quarterly reviews** of recognized assets and host an **annual InnerSource Awards** program.

### 10.3. Quarterly Review Process
- **Scope:** All Level 2 and Level 3 InnerSource assets listed in the internal catalog.
- **Data Sources:** Asset metrics such as usage statistics, contributor activity, issue response times, and test coverage.
- **Scoring Criteria:**
  1. **Adoption** – Number of teams actively using the component.
  2. **Quality** – Code health, test coverage, and adherence to standards.
  3. **Documentation** – Completeness, clarity, and ease of onboarding for new users.
  4. **Community Engagement** – Responsiveness to issues and pull requests, mentoring of new contributors.
  5. **Innovation** – Demonstrated technical excellence, unique patterns, or novel engineering approaches.

Each criterion will be rated on a 1–5 scale and combined for a composite score.

### 10.4. Quarterly Recognition
- **Quarterly Awards** will be presented for:
  - *Most Adopted Component* – Highest number of active consumers.
  - *Best Engineered Asset* – Highest composite quality score.
  - *Top Contributor(s)* – Individuals showing outstanding engagement or mentoring.
- Winners will be highlighted in internal communications and featured in the engineering portal.

### 10.5. Annual InnerSource Awards
At the end of each fiscal year, the InnerSource Working Group will host an **InnerSource Summit** featuring a ceremony for the **Top Three Assets of the Year**, recognizing:
1. **Best Overall Asset** – Highest combined adoption, quality, and impact score.
2. **Best New Asset** – Most impactful new addition within the past year.
3. **Community Choice Award** – Voted by engineers across the organization.

Award winners receive:
- Recognition in executive engineering communications.
- Featured placement in the internal developer portal.
- Optional innovation grant or additional resourcing for further development.

### 10.6. Continuous Feedback and Improvement
Post-review feedback will be shared with maintainers to identify strengths and improvement areas. The working group will update evaluation criteria periodically to align with evolving engineering priorities, ensuring fairness and transparency in the recognition process.

This recognition framework reinforces the InnerSource program’s goal: building a thriving ecosystem of shared, high-quality, and impactful engineering assets that accelerate organizational productivity and innovation.

### 10.7. Eligibility for Future Consideration
- Assets that have previously won an annual award are eligible for nomination again only if they have undergone a **major version update** (e.g., v2.0 → v3.0) that significantly changes architecture, usability, or scope.
- Major updates must demonstrate meaningful new value, enhancements, or improvements over the previous version.
- The review board will assess such entries as new submissions for the following calendar year.

### 10.8. Contributor Recognition and Metrics
While asset-level awards focus on maintainers and teams, the InnerSource program also values individual contributions that improve shared assets and foster collaboration across teams.

**Contributor Recognition Program:**
- Contributors will be recognized quarterly and annually based on measurable and qualitative criteria such as:
  - Number of **merged pull requests** across InnerSource assets.
  - Number of **resolved issues** or feature requests contributed to shared assets.
  - **Quality and impact** of contributions (e.g., design improvements, performance optimizations, or improved extensibility).
  - **Cross-team collaboration**—working with maintainers from other domains to implement and refine shared capabilities.
  - **Mentorship and community engagement**, including onboarding new contributors or providing peer reviews.

**Contributor Awards:**
- *Top Contributor Award (Quarterly)* – Based on contribution count and impact.
- *Most Valuable Contributor (Annual)* – Recognizing sustained excellence and leadership in InnerSource participation.
- *Emerging Contributor Award* – Highlighting newer engineers making meaningful early contributions.

Recognized contributors will be highlighted alongside asset awards in internal communications, with badges or acknowledgments visible in the developer portal.

### 10.9. Asset Nomination and Recognition Workflow
To streamline and simplify the awards process, the InnerSource recognition program will operate on a **nomination-based model** rather than automated discovery.

**Nomination Process:**
- Any engineer, team, or working group may nominate an InnerSource Asset for quarterly or annual recognition.
- Nominations should include:
  - Asset name and repository link.
  - Summary of the asset’s purpose and usage.
  - Evidence of adoption (e.g., dependent repositories, integration examples).
  - Quality indicators (test coverage, documentation maturity, stability).
  - Community indicators (number of contributors, PRs merged, response times, collaboration examples).
- Nominations are submitted through a standard form in the internal developer portal.

**Review Cycle:**
- The InnerSource Working Group reviews all nominations quarterly.
- Reviewers apply the evaluation criteria from Section 10.3 to determine award winners.
- Final results and recognition announcements are made during quarterly and annual review ceremonies.

This approach ensures visibility for impactful work without requiring the working group to manually track or discover new assets.

### 10.10. Metrics Tracking and Dashboards
To support transparency and fairness in both asset and contributor recognition, the InnerSource program will maintain **automated dashboards** that consolidate data from internal repositories and collaboration tools.

**Metrics Tracked for Assets:**
- Active consumers (dependent repositories or projects).
- Total commits, releases, and code churn over time.
- Pull request activity (opened, merged, time to merge).
- Issue resolution time and backlog trends.
- Test coverage percentage and CI/CD success rate.

**Metrics Tracked for Contributors:**
- Number of PRs merged across repositories.
- Number of issues resolved or closed.
- Review participation and feedback quality.
- Contribution diversity (across multiple projects or domains).
- Peer endorsements or votes within the developer portal.

**Dashboards and Reporting:**
- Dashboards will be visible within the internal engineering analytics portal.
- Metrics are refreshed weekly to ensure currency.
- Award nomination forms and review boards will have direct access to this data for validation.

These dashboards provide quantitative context to complement qualitative nominations, supporting a balanced and transparent recognition process.

### 10.11. Nomination Form Template and Submission Workflow

To facilitate consistent and transparent nominations for both asset and contributor recognition, the InnerSource program provides a standardized nomination form. This form will be embedded within the internal developer portal and linked directly from each eligible repository’s catalog entry.

#### 10.11.1. Asset Nomination Form Fields
| Field | Description |
|--------|-------------|
| **Asset Name** | The name of the InnerSource Asset being nominated. |
| **Repository URL** | Link to the repository in the internal code hosting system. |
| **Level** | Current classification level (1, 2, or 3). |
| **Maintainers** | List of primary maintainers or owning team. |
| **Nominee(s)** | Person(s) submitting the nomination. |
| **Category** | Select from: Most Adopted, Best Engineered, Best New Asset, Community Choice. |
| **Summary of Impact** | Describe what makes the asset notable (adoption, performance, innovation, etc.). |
| **Evidence of Adoption** | Include dependent repository count, consumer testimonials, or integration examples. |
| **Quality Metrics** | Provide data points such as test coverage, code review activity, and CI/CD health. |
| **Community Metrics** | Contributions from other teams, response times, and collaborative examples. |
| **Supporting Artifacts** | Links to documentation, architecture diagrams, or dashboards. |

#### 10.11.2. Contributor Nomination Form Fields
| Field | Description |
|--------|-------------|
| **Nominee Name** | Contributor being nominated. |
| **Email / Handle** | Internal contact identifier. |
| **Nominating Party** | Individual or team submitting the nomination. |
| **Award Category** | Select from: Top Contributor, Most Valuable Contributor, Emerging Contributor. |
| **Summary of Contributions** | Overview of the individual’s contributions and impact. |
| **Quantitative Evidence** | Number of merged PRs, resolved issues, or review participation. |
| **Qualitative Evidence** | Examples of innovation, collaboration, or mentorship. |
| **Supporting Links** | Repository links or dashboard screenshots showing contributions. |

#### 10.11.3. Submission Workflow
1. **Access Form:** Navigate to the InnerSource section of the developer portal and open the nomination form (asset or contributor).
2. **Complete Fields:** Provide all required information and attach evidence or links.
3. **Review and Validation:** Nominations are validated by the InnerSource Working Group for eligibility and completeness.
4. **Evaluation:** Qualified nominations are scored according to Section 10.3 criteria.
5. **Announcement:** Award recipients are announced during quarterly and annual InnerSource ceremonies and featured in the engineering portal.

This nomination form ensures fairness, structure, and repeatability in the recognition process while encouraging teams to highlight innovation and collaboration within the InnerSource ecosystem.

---

## 11. Community Roles and Contribution Framework

### 11.1. InnerSource Champions at the Town Level
To foster a culture of InnerSource collaboration and advocacy, each organizational **Town** (or major product group) designates one or more **InnerSource Champions**.

**Role Overview:**
- Serve as the local point of contact for InnerSource awareness, education, and engagement.
- Promote adoption of InnerSource best practices within their Town.
- Mentor new contributors and help identify candidate repositories for promotion to asset status.
- Encourage nomination submissions for quarterly and annual awards.
- Gather feedback from teams to inform updates to InnerSource policies and tooling.

**Responsibilities:**
- Conduct onboarding sessions or short “InnerSource 101” talks quarterly.
- Facilitate coordination between local teams and the central InnerSource Working Group.
- Track InnerSource activity metrics and report insights at quarterly alignment meetings.
- Champion open collaboration and recognition across functional boundaries.

### 11.2. Trusted Committer Model
As participation in InnerSource grows, some contributors demonstrate deep understanding, consistent quality, and strong collaboration. The **Trusted Committer** model formalizes advancement and establishes shared governance.

**Eligibility and Advancement:**
- Demonstrated track record of 10+ merged PRs or equivalent significant contributions across InnerSource assets.
- Positive review feedback from maintainers and peers.
- Demonstrated consistency in adhering to organizational code quality, testing, and documentation standards.
- Recommendation by at least one existing maintainer or InnerSource Champion.

**Responsibilities and Privileges:**
- Granted write or merge access to specific repositories or classes of assets.
- Authorized to review and approve PRs within their domain of expertise.
- Expected to uphold InnerSource contribution and review standards.
- Participate in code reviews, mentoring, and contributor onboarding.
- May serve as interim maintainers for orphaned or transitioning assets.

**Governance:**
- Trusted Committers are reviewed annually by the InnerSource Working Group.
- Status may be renewed, expanded, or sunset based on contribution activity and code quality.
- Recognition is recorded in the contributor’s profile and the engineering portal.

### 11.3. Default Contribution Guidelines and Guardrails
To maintain consistency and fairness in contribution workflows, all InnerSource Assets should implement the following **default contribution model** unless an approved repository-specific variant exists.

**Pull Request Workflow:**
1. Contributors fork or branch from the main repository.
2. Each PR must:
   - Include linked issue or context for the change.
   - Pass all CI/CD checks.
   - Receive at least one maintainer or trusted committer approval.
3. PR titles and descriptions should follow the standardized conventional commit format.
4. All code must meet Section 4 quality and testing standards.

**Quotas and Guardrails:**
- Limit any single PR to a reasonable size (e.g., ≤ 500 changed lines) to promote effective review.
- Large feature additions must be broken into incremental PRs.
- No contributor should open more than five active PRs per repository simultaneously without prior coordination.
- Refactors or changes that alter established interfaces require prior discussion through an RFC or design proposal.

**Disagreement and Conflict Resolution:**
- If a disagreement arises between contributors and maintainers:
  1. The discussion should occur transparently within the PR or issue thread.
  2. If unresolved, escalation should be directed to the repository’s maintainers group.
  3. Persistent or cross-team disputes are referred to the **InnerSource Working Group** for review.
  4. The group may request mediation from an InnerSource Champion or neutral Trusted Committer.

**Contributor Recognition:**
- Contributors demonstrating exemplary collaboration or conflict resolution behavior may be nominated for contributor recognition (Section 10.8).
- Constructive feedback and mentorship are valued over raw contribution volume.

This framework ensures scalable, respectful, and transparent collaboration across teams, while reinforcing fairness and shared ownership within the InnerSource ecosystem.
