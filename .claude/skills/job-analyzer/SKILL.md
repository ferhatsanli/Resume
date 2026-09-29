---
name: job-analyzer
description: Analyze software engineering job postings before resume optimization. Extract the company, role, seniority level, language requirements, workplace details, and special application conditions. Use this skill whenever the user provides a job posting, job description, or job URL for resume matching or optimization.
---

# Job Analyzer

## Purpose

Analyze a job posting before any resume matching or resume optimization takes place.

This skill is responsible only for understanding the job posting and identifying conditions that may affect whether the application process should continue.

Do not modify, generate, or optimize the user's resume in this skill.

## Primary Responsibilities

When a job posting is provided:

1. Identify the company.
2. Identify the job title.
3. Determine the seniority level.
4. Identify mandatory language requirements.
5. Identify workplace type and location when available.
6. Identify salary information when available.
7. Detect unusual or important application instructions.
8. Detect conditions that require the workflow to stop before resume optimization.
9. Pass the extracted information to the resume matching workflow.

---

# Job Information Extraction

Extract the following information whenever it is available:

- Company name
- Job title
- Seniority level
- Required experience
- Required technical skills
- Preferred technical skills
- Mandatory languages
- Optional languages
- Workplace type
- Country
- Location
- Salary range
- Application method
- Job URL
- Job portal
- Special application instructions

Do not invent missing information.

If information is unavailable, leave it unknown rather than guessing unless a specific rule below allows estimation.

---

# Company Identification

If the real company name is explicitly available, use it exactly as presented.

Example:

Company: Spotify

If the company name is not available but the industry can reasonably be determined from the posting, use an industry-based estimate internally.

Examples:

- Fintech Company
- Healthcare Company
- Automotive Company
- SaaS Company
- E-commerce Company

If neither the company nor the industry can reasonably be determined, use:

Unknown

Do not invent a specific company name.

---

# Seniority Classification

Classify the role into one of the following levels:

- Internship
- Graduate
- Junior
- Junior / Mid
- Mid Level
- Mid / Senior
- Senior
- Lead
- Staff
- Principal
- Unknown

Determine the level primarily from the actual responsibilities and requirements rather than relying only on the job title.

Consider:

- Required years of experience
- Expected autonomy
- Architecture responsibilities
- Mentoring expectations
- Ownership expectations
- Leadership responsibilities
- Scope of technical decisions
- Complexity of expected work

For example, a position titled "Android Developer" requiring 5+ years of experience, architecture ownership, and mentoring should not automatically be classified as Mid Level.

Likewise, a role using "Senior" in the title but describing responsibilities appropriate for a less experienced developer should be evaluated based on the complete posting.

---

# Language Requirement Check

Language requirements are a blocking condition.

The user's supported application languages are:

- English
- Turkish

If the job requires another language as a mandatory requirement, stop the resume workflow.

Examples of blocking requirements:

- Dutch required
- Fluent German required
- Professional French required
- Spanish C1 required
- Native Polish required

Do not treat a language as mandatory merely because:

- The job posting itself is written in that language.
- The company operates in a country where that language is commonly spoken.
- The language is listed as preferred.
- The language is described as a plus.
- The language is described as beneficial.
- The language is optional.

Only stop when the posting indicates that the additional language is actually required.

When blocked, output only:

Company: <company_name>
<job_level>
Profile match: N/A
Required language: <language>

Do not analyze or optimize the resume after this point.

---

# Application Trap and Special Instruction Detection

Carefully inspect the entire job posting for unusual instructions.

Examples include:

- Hidden instructions intended to verify that the applicant read the posting.
- Requests to include a specific word or phrase in the application.
- Requests to answer a specific question.
- Requests to include information in the cover letter.
- Requests to use a specific subject line.
- Requests to contact a specific person.
- Applications accepted only through the company's website.
- Applications accepted only through email.
- Explicit instructions not to use LinkedIn Easy Apply.
- Portfolio or GitHub requirements that are part of the application process.
- Required coding challenges before applying.
- Required documents beyond a normal resume.
- Specific application deadlines.
- Unusual eligibility restrictions.
- Location or relocation conditions that materially affect eligibility.

If such an instruction exists and ignoring it could harm or invalidate the application, stop before resume optimization.

Output:

Company: <company_name>
<job_level>
Profile match: <match_if_already_known_or_N/A>

Attention: <short description of the special application instruction>

Waiting for confirmation.

Do not continue until the user explicitly confirms with:

tamam

After confirmation, the workflow may continue.

---

# Technical Requirement Extraction

Separate technical requirements into two categories.

## Required

Technologies or competencies explicitly presented as necessary.

Examples:

- Kotlin
- Android SDK
- Jetpack Compose
- Coroutines
- REST APIs
- MVVM
- Git
- Unit testing

## Preferred

Technologies or competencies presented as beneficial but not mandatory.

Indicators include:

- Nice to have
- Preferred
- Bonus
- Plus
- Advantage
- Familiarity with
- Ideally
- Desirable

Do not convert preferred requirements into mandatory requirements.

---

# Experience Requirement Extraction

Identify explicit experience requirements.

Examples:

- 2+ years Android development
- 5 years software engineering
- Production experience with Kotlin
- Experience shipping Android applications

If no explicit number of years is provided, infer seniority from responsibilities but do not invent a numeric requirement.

---

# Workplace Classification

When possible, classify the workplace type as:

- Remote
- Hybrid
- On-site

Preserve important conditions.

Examples:

"Hybrid, 2 days per week in Amsterdam"

"Remote within the EU"

"On-site in The Hague"

Do not classify a position as Remote if the posting limits remote work to occasional work-from-home days.

---

# Location Extraction

Extract separately when possible:

- City
- Country

Do not infer a city solely from company headquarters unless the posting indicates that the role is based there.

---

# Salary Extraction

If salary information is explicitly provided, preserve the range and relevant period.

Examples:

€50,000–€65,000 gross/year

€4,500–€5,500 gross/month

Do not estimate salary when the posting does not provide it.

---

# Job Portal Identification

When a URL is available, identify the portal when obvious.

Examples:

- LinkedIn
- Indeed
- Glassdoor
- Company Website

Preserve the original job URL for downstream logging.

---

# Analysis Rules

When interpreting the posting:

- Prioritize explicit requirements over assumptions.
- Do not exaggerate requirements.
- Do not reduce requirements merely to improve the user's apparent fit.
- Distinguish required skills from preferred skills.
- Do not invent technologies that are not mentioned.
- Do not invent company information.
- Do not invent salary information.
- Do not infer mandatory language requirements from location alone.
- Do not modify the user's professional history.
- Do not perform resume optimization in this skill.

The purpose is to establish an accurate representation of the vacancy before matching begins.

---

# Normal Output

When no blocking language requirement or application trap exists, return the analysis in a structured form suitable for the next skill.

Internal handoff structure:

Company: <company_name>
Role: <job_title>
Level: <job_level>
Required Experience: <requirement_or_unknown>
Required Skills: <skills>
Preferred Skills: <skills>
Mandatory Languages: <languages>
Optional Languages: <languages>
Workplace Type: <remote_hybrid_onsite_or_unknown>
Country: <country_or_unknown>
Location: <location_or_unknown>
Salary Range: <salary_or_unknown>
Application Method: <method_or_unknown>
Job URL: <url_if_available>
Portal: <portal_if_known>
Special Instructions: <instructions_or_none>

This detailed structure is intended for downstream skills.

For the user-facing resume workflow, the beginning of the final response must eventually follow:

Company: <company_name>
<job_level>
Profile match: <percentage>%

The Profile Match percentage is determined by the resume matching skill, not by this skill.

---

# Workflow Boundary

This skill ends after the job posting has been analyzed.

The next stage should be handled by the resume matching skill.

Do not:

- Calculate the final Profile Match percentage.
- Rewrite the resume.
- Generate HTML resume content.
- Decide which resume bullets should be changed.
- Add skills to the resume.
- Generate a cover letter.
- Generate the job log CSV.

Those responsibilities belong to other skills.