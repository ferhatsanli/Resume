---
name: resume-match-evaluator
description: Evaluate how well the user's existing resume matches a previously analyzed job posting. Produce a recruiter-style Profile Match percentage and determine whether the resume should remain unchanged, be optimized, or require user confirmation before optimization.
---

# Resume Match Evaluator

## Purpose

Evaluate the user's current resume against an analyzed job posting.

This skill determines:

1. The current recruiter-style Profile Match percentage.
2. Whether the existing resume is already strong enough.
3. Whether resume optimization is necessary.
4. Whether optimization must wait for explicit user confirmation.

This skill evaluates the existing resume.

It does not rewrite or modify the resume.

---

# Required Inputs

Before evaluating the match, obtain:

1. The structured job analysis produced by the job analyzer.
2. The user's current PDF resume.

The HTML resume may be consulted when useful for understanding the source content, but the initial Profile Match must represent the resume the user would currently submit.

Prefer the PDF resume when determining the current match.

Do not calculate the match based on a hypothetical optimized resume.

---

# Evaluation Perspective

Evaluate the resume from the perspective of a recruiter reviewing the application for the specific vacancy.

The percentage should represent the approximate strength of the candidate's visible profile for that particular job.

Do not inflate the percentage simply because the resume could potentially be rewritten to match the vacancy better.

Evaluate what is currently visible and supported.

---

# Evidence Rules

Only count experience, technologies, responsibilities, education, projects, and achievements that are supported by the user's existing resume or available project sources.

Do not assume that the user knows a technology merely because it is related to another technology they know.

Examples:

Kotlin experience does not automatically prove Kotlin Multiplatform experience.

Jetpack Compose experience does not automatically prove XML/View-system expertise.

Firebase experience does not automatically prove Google Cloud Platform experience.

REST API experience does not automatically prove GraphQL experience.

GitHub Actions experience does not automatically prove Jenkins experience.

Android experience does not automatically prove iOS development experience.

Do not award points for unsupported experience.

---

# Match Dimensions

Evaluate the vacancy across the following dimensions.

The weights are guidelines rather than a mechanical ATS formula.

## 1. Core Technical Match — 30%

Evaluate the technologies and engineering skills central to the role.

Examples:

- Kotlin
- Android SDK
- Jetpack Compose
- Java
- Coroutines
- Flow / StateFlow
- MVVM
- Clean Architecture
- REST APIs
- Retrofit
- Room
- Dependency Injection
- Firebase
- Testing frameworks
- CI/CD

Give significantly more importance to technologies explicitly marked as required.

---

## 2. Relevant Professional Experience — 25%

Evaluate:

- Relevant years of experience
- Android/mobile development experience
- Production-like development experience
- Similar responsibilities
- Ownership level
- Professional versus personal-project experience

Professional experience should normally carry more weight than personal projects.

Projects may strengthen evidence but should not automatically replace explicitly required professional experience.

---

## 3. Role and Responsibility Match — 15%

Compare what the candidate has done with what the new role expects.

Examples:

- Feature development
- Architecture
- API integration
- Performance optimization
- Debugging
- Code reviews
- Testing
- CI/CD
- Cross-functional collaboration
- Product ownership
- Release management
- Mentoring
- Technical leadership

---

## 4. Architecture and Engineering Practices — 10%

Evaluate relevant engineering practices such as:

- MVVM
- Clean Architecture
- Separation of concerns
- Dependency Injection
- State management
- Modularization
- Testing
- Maintainability
- Git workflows
- CI/CD
- Code quality practices

Only count practices supported by the resume.

---

## 5. Domain Match — 5%

Evaluate whether the user's background overlaps with the company's domain.

Examples:

- Fintech
- Healthcare
- Payments
- E-commerce
- IoT
- Remote monitoring
- Automation
- Enterprise software

Domain mismatch should usually have limited impact unless domain experience is explicitly required.

---

## 6. Education and Formal Requirements — 5%

Evaluate explicit requirements such as:

- Bachelor's degree
- Computer Science
- Software Engineering
- Information Systems
- Related technical education
- Certifications

A related engineering degree may satisfy a broad technical degree requirement when reasonable.

Do not claim equivalence when the posting explicitly requires a specific qualification that the user does not possess.

---

## 7. Collaboration and Product Skills — 5%

Evaluate supported evidence for:

- Agile development
- Working with stakeholders
- Cross-functional collaboration
- Translating requirements
- Iterative development
- Product thinking
- Communication

Do not award substantial points for generic soft skills that are merely expected of all candidates.

---

## 8. Preferred / Bonus Requirements — 5%

Evaluate technologies and experience explicitly marked as:

- Preferred
- Nice to have
- Bonus
- Advantage
- Plus
- Desirable

Missing bonus requirements should have much less impact than missing mandatory requirements.

---

# Critical Requirements

Some requirements should affect the match more strongly than their raw weighting suggests.

Examples:

- Required minimum years of experience
- A core programming language
- Required Android experience
- Required platform experience
- Required architecture experience
- Required location eligibility
- Required professional experience
- Explicit seniority expectations

If the candidate clearly misses a critical requirement, reflect this realistically in the final percentage.

Do not compensate for a missing critical requirement merely by matching many minor keywords.

---

# Seniority Mismatch

Seniority mismatch must materially affect the score.

Examples:

A candidate with approximately 2–3 years of relevant experience applying for a role requiring 7+ years and senior technical leadership should not receive a high match merely because the technology stack overlaps.

Likewise, a candidate with relevant professional experience should not automatically be treated as entry-level merely because a job title was unusual.

Consider:

- Years of relevant experience
- Independence
- Architecture ownership
- Scope
- Mentoring
- Leadership
- Production responsibility
- Complexity of previous work

---

# Keyword Matching Rules

Do not calculate Profile Match as simple keyword overlap.

Recruiters evaluate context.

For example:

A resume containing:

"Kotlin, Jetpack Compose, MVVM, Retrofit"

does not automatically strongly match a Senior Android position requiring:

- Architecture ownership
- Modularization
- mentoring
- large-scale production experience
- release ownership

Technical overlap is only one component of the match.

---

# Closely Related Technologies

Related technologies may receive partial credit when reasonable.

Examples:

StateFlow may support evidence of reactive state management.

Retrofit may support evidence of REST API integration.

Hilt may support evidence of dependency injection.

GitHub Actions may support evidence of CI/CD experience.

However, never present related technologies as identical.

Example:

GitHub Actions can provide partial CI/CD relevance to a Jenkins requirement, but the resume must not be treated as proving Jenkins experience.

---

# Recruiter Visibility Rule

Score what a recruiter can reasonably identify from the resume.

If the user actually has relevant knowledge but it is not visible in the resume or project sources, do not fully count it.

This is important because the purpose of the initial score is to evaluate the current resume, not the user's entire possible knowledge.

A skill that is genuinely supported elsewhere in the user's existing professional/project history but poorly expressed in the resume may be considered weakly visible.

Such cases are strong candidates for later resume optimization.

---

# Profile Match Scale

Use the following ranges as calibration guidance.

## 90–100%

Exceptionally strong alignment.

The candidate satisfies nearly all important requirements and has highly relevant experience.

## 85–89%

Strong match.

The resume is already sufficiently aligned that optimization is unnecessary under this workflow.

## 75–84%

Good match.

The candidate is credible for the role, but targeted resume optimization could materially improve positioning.

## 60–74%

Moderate match.

There is meaningful overlap, but several requirements or important signals are missing or weakly represented.

## 50–59%

Weak-to-moderate match.

There is enough relevant background to justify targeted optimization, but substantial gaps exist.

## Below 50%

Low match.

Important requirements, experience, seniority, domain, or core technologies are missing.

Optimization must not begin automatically.

---

# Decision Thresholds

The Profile Match percentage controls the next workflow step.

## Profile Match >= 85%

Do not modify the resume.

The workflow ends.

User-facing output:

Company: <company_name>
<job_level>
Profile match: <percentage>%
Bu hali iyidir

Do not add explanations.

Do not generate HTML.

Do not suggest improvements.

---

## Profile Match 50–84%

Resume optimization is allowed.

Pass the job requirements, resume evidence, gaps, and match analysis to the resume optimizer.

The resume optimizer should attempt to strengthen the resume toward at least an 80% match where truthfully possible.

Do not ask for confirmation solely because the score is within this range.

---

## Profile Match < 50%

Do not optimize the resume yet.

Ask the user for confirmation.

User-facing output:

Company: <company_name>
<job_level>
Profile match: <percentage>%
Eşleşme %50'nin altında. Resume'yi optimize etmemi istiyor musun?

Stop.

Do not generate HTML.

Do not invoke resume optimization until the user explicitly confirms.

A confirmation such as:

tamam

allows the workflow to continue.

---

# Language Block Priority

If the job analyzer has already identified a mandatory language other than English or Turkish, do not perform resume optimization.

The language restriction takes priority over the Profile Match workflow.

Do not attempt to improve the score by ignoring the language requirement.

---

# Application Trap Priority

If the job analyzer identified an application trap or special instruction requiring confirmation, stop before continuing.

Do not bypass that confirmation even if the Profile Match would otherwise be high.

---

# Optimization Potential

When the score is below 85%, identify internally which gaps can truthfully be improved through resume presentation.

Classify gaps into:

## Present but Underrepresented

The user has evidence for the requirement, but the resume does not emphasize it sufficiently.

These are strong optimization candidates.

## Closely Related

The user has related experience that can truthfully be reframed without claiming direct experience.

These may receive careful optimization.

## Missing

There is no evidence that the user has the required skill or experience.

These must not be added to the resume.

## Structural

The relevant information exists but is located poorly, lacks visibility, or uses terminology that does not align with the vacancy.

These may be improved through wording or placement.

---

# Truthfulness Constraint

Never increase the Profile Match by inventing experience.

Forbidden examples include:

- Adding technologies the user has never used.
- Increasing years of experience.
- Changing job titles to falsely imply seniority.
- Inventing production deployments.
- Inventing leadership responsibilities.
- Inventing metrics.
- Inventing team sizes.
- Inventing certifications.
- Inventing clients.
- Inventing projects.
- Inventing responsibilities.
- Converting personal projects into professional experience.
- Claiming professional experience with a technology when only theoretical knowledge exists.

Resume optimization means improving presentation of real evidence.

It does not mean manufacturing evidence.

---

# Match Analysis Handoff

When optimization is required, prepare an internal handoff containing:

Company: <company_name>
Role: <job_title>
Level: <job_level>
Current Profile Match: <percentage>%

Critical Requirements:
- <requirement>
- <requirement>

Strong Matches:
- <supported match>
- <supported match>

Present but Underrepresented:
- <item>
- <item>

Closely Related:
- <item>
- <item>

Missing Requirements:
- <item>
- <item>

Recommended Resume Focus:
- <area>
- <area>

This information is intended for the resume optimizer.

Do not expose this analysis to the user during the normal resume workflow unless the user explicitly asks for analysis.

---

# Output Discipline

The normal user-facing response must remain short.

Do not provide:

- Scoring breakdowns
- Recruiter commentary
- Explanations
- Gap analysis
- Recommendations
- Tables
- ATS commentary

unless the user explicitly requests them.

The standard workflow output begins with:

Company: <company_name>
<job_level>
Profile match: <percentage>%

The next lines depend on the threshold rules defined above.

---

# Workflow Boundary

This skill determines whether resume optimization should happen.

It does not:

- Rewrite the HTML resume.
- Modify resume layout.
- Generate new experience.
- Generate cover letters.
- Produce the job-log CSV.
- Generate the `report` output.

If optimization is required and permitted, hand off to:

resume-optimizer