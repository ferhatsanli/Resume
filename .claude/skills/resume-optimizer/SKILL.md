---
name: resume-optimizer
description: Optimize the user's existing HTML resume for a specific job posting while preserving the original HTML structure, visual format, factual accuracy, and professional history. Use only after job analysis and profile-match evaluation determine that optimization is required and permitted.
---

# Resume Optimizer

## Purpose

Optimize the user's existing HTML resume for a specific job vacancy.

The goal is to make small, targeted, truthful improvements that increase the resume's relevance to the job while preserving the existing HTML template and the user's real professional history.

The target is an optimized Profile Match of at least 80% whenever this can realistically be achieved without inventing information.

This skill must never fabricate experience merely to reach the target.

---

# Required Inputs

Before optimization begins, obtain:

1. The analyzed job posting from `job-analyzer`.
2. The match evaluation from `resume-match-evaluator`.
3. The user's current HTML resume.
4. The user's current PDF resume when available.
5. Relevant existing project/profile sources when they are already part of the project context.

The HTML resume is the primary source for structure and formatting.

The PDF resume may be used to verify the currently presented professional information.

---

# Preconditions

Do not optimize the resume unless the previous workflow stages allow it.

## Do Not Optimize When Profile Match >= 85%

If the current resume already has a Profile Match of at least 85%, the resume must remain unchanged.

The workflow should already have terminated with:

Company: <company_name>
<job_level>
Profile match: <percentage>%
Bu hali iyidir

---

## Do Not Optimize When Profile Match < 50% Without Confirmation

If the current Profile Match is below 50%, optimization requires explicit user confirmation.

Do not generate HTML until confirmation has been received.

Accepted confirmation may include:

tamam

or another clear affirmative response.

---

## Do Not Optimize When Blocked by Language

If the vacancy requires a mandatory language other than:

- English
- Turkish

and the job analyzer has marked this as a blocking requirement, do not optimize the resume.

---

## Do Not Optimize Before Special-Instructions Confirmation

If the job analyzer detected an application trap or special application requirement that requires confirmation, wait for the user's confirmation before proceeding.

---

# Optimization Objective

Optimize the resume specifically for the supplied vacancy.

Target:

Optimized Profile Match >= 80%

This is a target, not permission to fabricate information.

If the candidate's real background cannot reasonably support an 80% match, create the strongest truthful version possible.

Never invent information merely to satisfy the numerical target.

---

# Optimization Philosophy

Make the smallest set of changes that creates the strongest legitimate improvement.

Prefer:

- Better terminology
- Better emphasis
- Better ordering
- More relevant descriptions
- Stronger technical specificity
- Removal of irrelevant skills
- Highlighting existing relevant experience
- Highlighting relevant projects
- Aligning terminology with the vacancy

Avoid unnecessary rewriting.

If a section already strongly supports the vacancy, preserve it.

---

# Source of Truth

The user's real background is the absolute constraint.

Resume content may only be based on:

- Existing professional experience
- Existing projects
- Existing education
- Existing technical skills
- Existing responsibilities
- Existing project sources
- Reasonable descriptions of work already supported by those sources

Do not treat the vacancy itself as evidence that the user possesses a skill.

A technology appearing in the job posting does not authorize adding it to the resume.

---

# Truthfulness Rules

Never fabricate:

- Employers
- Clients
- Projects
- Technologies
- Programming languages
- Frameworks
- Responsibilities
- Leadership experience
- Team sizes
- Certifications
- Degrees
- Job titles
- Employment dates
- Years of experience
- Production deployments
- Application download numbers
- Performance improvements
- Revenue impact
- User counts
- Awards
- Metrics
- Testing experience
- Architecture ownership

unless supported by existing sources.

---

# Reasonable Reframing

Existing experience may be rewritten to align more clearly with the terminology used by the vacancy.

Example:

Original:

"Integrated backend services using Retrofit."

Vacancy emphasizes:

"REST API integration."

A truthful optimized version could be:

"Integrated REST APIs using Retrofit to retrieve and process backend data."

This does not invent experience.

It makes existing experience easier for recruiters and ATS systems to recognize.

---

# Related Technology Rule

Do not convert related technologies into technologies the user has not used.

Example:

Existing evidence:

GitHub Actions and CI/CD

Vacancy:

Jenkins

Allowed:

"Built and worked with CI/CD workflows using GitHub Actions."

Not allowed:

"Built CI/CD pipelines using Jenkins."

The optimized resume can emphasize transferable experience without claiming the missing technology.

---

# Experience Section

Professional experience is the most important optimization area.

For each role:

1. Preserve the employer.
2. Preserve the employment dates.
3. Preserve the factual role.
4. Preserve the real responsibilities.
5. Reorder bullets when necessary.
6. Rewrite bullets when stronger job-aligned terminology is supported.
7. Remove low-value bullets if space is needed.
8. Emphasize technologies relevant to the vacancy.
9. Emphasize responsibilities similar to the target role.

Do not completely rewrite every bullet merely to make the resume look different.

---

# Experience Ordering Within Roles

Within each job, prioritize bullets according to vacancy relevance.

A useful general ordering is:

1. Core technology
2. Main responsibility
3. Architecture
4. Backend/API integration
5. State/data management
6. Testing
7. Performance/debugging
8. CI/CD
9. Collaboration
10. Secondary responsibilities

Change this ordering when the vacancy clearly prioritizes something else.

---

# Job Title Rule

Preserve job titles unless a minor clarification is genuinely supported by the user's existing professional history.

Never change a title merely to imitate the vacancy.

Examples of prohibited manipulation:

Android Developer -> Senior Android Engineer

Software Developer -> Mobile Architect

Developer -> Engineering Lead

Do not inflate seniority.

---

# Freelance / Independent Experience

Do not invent clients or commercial engagements.

Do not imply that personal development work was paid client work unless supported.

Existing independent development may be described using its real engineering activities.

Relevant projects may support the Independent Android Developer section when they genuinely belong to that period and work.

---

# Skills Section

Optimize the Skills section aggressively but truthfully.

The Skills section should prioritize technologies relevant to the vacancy.

## Reordering

Move the most relevant supported skills toward the top.

For an Android/Kotlin vacancy, this may include:

- Kotlin
- Android SDK
- Jetpack Compose
- MVVM
- Clean Architecture
- Coroutines
- StateFlow
- Retrofit
- REST APIs
- Room
- Hilt
- Firebase
- Testing
- CI/CD

Only include skills supported by the user's background.

---

# Removing Skills

Remove skills when they:

- Are irrelevant to the vacancy.
- Consume valuable resume space.
- Distract from stronger matching technologies.
- Add little recruiter value for the target position.

Do not remove important skills merely because they are not explicitly listed in the vacancy when they materially strengthen the candidate's engineering profile.

---

# Adding Skills

A skill may be added only when there is evidence that the user actually possesses or has used it.

Evidence may come from:

- Existing resume content
- Existing project descriptions
- Existing project sources
- Existing professional history available to the workflow

Never add a technology solely because the vacancy requests it.

---

# Skill Naming

When possible, use industry-standard terminology matching the vacancy.

Examples:

If supported:

REST APIs / JSON

may become:

REST APIs

or:

REST API Integration

depending on the vacancy wording.

Do not use unnatural keyword stuffing.

---

# Projects Section

Projects should strengthen requirements that professional experience does not demonstrate strongly enough.

Prioritize projects that overlap with:

- Target technologies
- Architecture
- APIs
- Networking
- Backend integration
- Real-time communication
- Persistence
- State management
- Testing
- Platform features
- The target business domain

---

# Project Selection

If space is limited, keep the projects most relevant to the vacancy.

Do not preserve a weaker project merely because it existed in the original resume if a more relevant existing project is available and supported by project sources.

However, do not invent new projects.

---

# Project Descriptions

Project descriptions may be rewritten to emphasize relevant existing technical characteristics.

For example, if a real project uses:

- Kotlin
- Jetpack Compose
- MVVM
- StateFlow
- Retrofit
- Ktor
- Firebase
- Raspberry Pi
- Linux

and several of these technologies are relevant to the vacancy, emphasize them naturally.

Avoid turning project descriptions into keyword lists.

---

# Education Section

Preserve the user's real education.

Do not alter:

- Institution
- Degree
- Field of study

unless correcting formatting against the project's authoritative source.

Education wording may be slightly adjusted to align with a broad vacancy requirement.

For example:

BSc Information Systems Engineering

should remain factual.

Do not convert it into:

BSc Computer Science

even when the vacancy asks for Computer Science.

---

# Languages Section

Preserve the user's supported language information.

Do not increase proficiency.

Do not add languages based on location or vacancy requirements.

---

# ATS Optimization

Improve ATS recognition without making the resume unnatural.

Prefer exact industry-standard terminology when truthful.

For example, if the resume says:

"backend communication"

and the actual implementation used REST APIs, writing:

"REST API integration"

may improve ATS recognition while remaining truthful.

---

# Keyword Placement

Important supported keywords should preferably appear in meaningful context.

Strong:

"Integrated REST APIs using Retrofit and handled local persistence with Room."

Weak:

"Kotlin, REST, Retrofit, APIs, Room, Android, architecture."

Avoid keyword stuffing.

---

# Required vs Preferred Requirements

Prioritize required requirements first.

Optimization priority:

1. Critical mandatory requirements
2. Core technical requirements
3. Relevant responsibilities
4. Architecture and engineering practices
5. Preferred technologies
6. Domain terminology
7. General soft skills

Do not consume significant resume space optimizing for minor bonus requirements while major required skills remain underrepresented.

---

# Missing Requirements

If a requirement is genuinely missing from the user's background:

Do not add it.

Instead, strengthen adjacent real experience where appropriate.

Example:

Vacancy requires Jenkins.

User has GitHub Actions.

Emphasize:

CI/CD workflows using GitHub Actions.

Do not mention Jenkins as experience.

---

# Seniority

Do not manipulate the resume to falsely satisfy a seniority requirement.

You may emphasize:

- Ownership
- Independent development
- Architecture decisions
- Debugging
- Stakeholder collaboration
- End-to-end implementation

when these are supported.

Do not invent:

- Mentoring
- Team leadership
- Staff-level architecture
- Engineering management
- Technical leadership

to make the candidate appear more senior.

---

# Domain Alignment

If the user's existing experience naturally overlaps with the target company's domain, make that overlap more visible.

Examples:

A healthcare monitoring vacancy may benefit from emphasizing real-time monitoring and data visualization experience.

An IoT vacancy may benefit from emphasizing Android-to-device communication.

An automation vacancy may benefit from emphasizing UiPath and process monitoring.

A backend-connected mobile role may benefit from emphasizing REST APIs, Firebase, Ktor, or real-time communication when supported.

Do not claim direct industry experience when only technical similarities exist.

---

# HTML Template Preservation

The existing HTML resume template must be preserved.

The optimizer edits resume content, not the design system.

Preserve:

- `<!doctype html>`
- HTML document structure
- `<head>`
- Existing CSS
- Page dimensions
- Header structure
- Colors
- Typography
- Column layout
- Sidebar
- Main content structure
- Right column structure
- Contact area
- Profile photo element
- Existing CSS class names
- General section hierarchy

Do not redesign the resume.

---

# CSS Rule

Do not modify CSS unless a small adjustment is absolutely necessary to prevent content overflow caused by legitimate resume optimization.

Content reduction should be attempted before CSS modification.

Preferred order:

1. Remove irrelevant content.
2. Shorten verbose bullets.
3. Remove weak bullets.
4. Shorten project descriptions.
5. Remove irrelevant skills.
6. Only then consider a minimal spacing adjustment.

Never redesign the template simply to fit more keywords.

---

# Page Layout

The existing resume is designed for A4 output.

Preserve the intended page layout.

Avoid causing:

- Education to unexpectedly move to another page.
- Skills to overflow.
- Sections to overlap.
- Text to leave the printable area.
- Columns to become unbalanced.
- Excessive blank space.
- Header overflow.

Keep the resume visually usable when rendered or printed.

---

# Full HTML Output Requirement

When optimization occurs, always output the complete HTML document.

Never output only:

- Changed sections
- Diff
- Snippets
- Replacement bullets
- Partial HTML

The output must begin with:

<!doctype html>

and include the complete document through:

</html>

The user must be able to replace the previous HTML resume directly with the generated output.

---

# Existing Structure

When the source resume contains sections such as:

- Experience Overview
- Languages
- Skills
- Projects
- Education

preserve these sections unless there is a strong vacancy-specific reason to modify their content.

Do not accidentally omit existing sections.

---

# Contact Information

Preserve existing contact information exactly unless the user explicitly requests a change.

Do not invent or modify:

- Phone number
- Email address
- LinkedIn URL
- GitHub URL

---

# Profile Photo

Preserve the existing profile image reference and image element unless the user explicitly requests otherwise.

Do not rename the image file unnecessarily.

---

# HTML Safety

Keep the generated HTML valid and self-contained relative to the existing template.

Do not add:

- JavaScript
- External frameworks
- Tracking
- External CSS libraries
- Unnecessary dependencies

unless already part of the template or explicitly requested.

---

# Final Quality Check

Before returning the optimized resume, verify:

## Accuracy

- No fabricated technologies
- No fabricated experience
- No fabricated responsibilities
- No inflated seniority
- No changed employment dates
- No false education claims
- No invented metrics

## Relevance

- Important job requirements are visible where supported.
- Relevant technologies receive priority.
- Irrelevant content has been reduced where useful.
- Strong existing evidence has not been accidentally removed.

## HTML Integrity

- Complete HTML document
- Original template preserved
- CSS preserved unless minimal changes were necessary
- All sections properly closed
- Contact links preserved
- Profile image preserved
- Layout remains suitable for A4 rendering

## Resume Quality

- No obvious keyword stuffing
- No unnecessary repetition
- Bullets remain readable
- Technical wording is natural
- Strongest evidence appears first

---

# Optimized Profile Match

After optimization, internally reassess the resume against the vacancy.

Target:

>= 80%

Do not fabricate information to reach this target.

The Profile Match shown in the user-facing header remains the original recruiter-style match unless the workflow explicitly requires reporting a post-optimization score.

The purpose of optimization is to improve the resume from that baseline.

---

# User-Facing Output

When optimization is performed, output only:

Company: <company_name>
<job_level>
Profile match: <original_profile_match>%
HTML Resume:

<complete optimized HTML>

Do not add:

- Explanations
- Analysis
- Change summaries
- Recommendations
- Introductory text
- Closing comments

The HTML must immediately follow:

HTML Resume:

---

# Change Tracking

Internally retain a concise record of every meaningful resume modification.

Examples:

- Reordered Kotlin and Jetpack Compose to the top of Skills.
- Removed Linux / Raspberry Pi because it was irrelevant to the vacancy.
- Reworded AKTEK API bullet to emphasize real-time backend integration.
- Emphasized StateFlow in the relevant project.
- Shortened WhoConnected description.
- Reordered freelance bullets around architecture and testing.

This information is intended for the `report` command.

Do not show the change record during the normal optimization workflow.

---

# Report Compatibility

If the user later sends:

report

the workflow should be able to provide only the changes made during the most recent resume optimization.

The report itself belongs to the application-writing/report skill.

---

# Minimal Change Principle

Do not optimize for the sake of changing something.

Every modification should have a reason related to:

- Vacancy relevance
- Recruiter readability
- ATS recognition
- Space efficiency
- Technical clarity
- Stronger evidence presentation

If a line already works well for the vacancy, keep it.

---

# Workflow Boundary

This skill is responsible for producing the optimized HTML resume.

It does not:

- Perform the initial job analysis.
- Determine whether a mandatory language blocks the application.
- Determine the original Profile Match.
- Produce CSV job logs.
- Write cover letters.
- Write motivation letters.
- Produce the user-facing `report`.

Those responsibilities belong to other skills.