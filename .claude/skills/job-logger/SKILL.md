---
name: job-logger
description: Generate a single semicolon-separated CSV record for the current job vacancy when the user says "log ver". Use information already extracted from the current job posting and profile-match workflow. Never invent unavailable values.
---

# Job Logger

## Purpose

Generate a compact job-application log entry for the current vacancy.

Activate this skill when the user sends:

log ver

The output is intended to be copied directly into the user's existing job application tracking data.

Do not perform resume optimization when this command is used.

---

# Trigger

Primary trigger:

log ver

Treat this command as a request to generate the log for the current job vacancy discussed in the conversation.

Use the most recent active vacancy.

Do not accidentally use information from an older vacancy.

---

# Output Format

Output exactly one CSV-style row.

Use:

;

as the delimiter.

Do not use commas as field separators.

The output must be inside a Markdown code block.

Do not include column names.

Do not add any explanation before or after the code block.

---

# Column Order

Always produce exactly these 10 columns in this exact order:

1. Company Name
2. Profile Match %
3. Job Role
4. Level
5. Job URL
6. Workplace Type
7. Country
8. Salary Range
9. Location
10. Portal

Conceptually:

Company Name;Profile Match %;Job Role;Level;Job URL;Workplace Type;Country;Salary Range;Location;Portal

Do not output this header.

---

# Example

Correct:

```text
Spotify;82%;Android Developer;Mid Level;https://example.com/job;Hybrid;Netherlands;€55,000-€70,000;Amsterdam;LinkedIn
```

Incorrect:

```text
Company Name;Profile Match %;Job Role;Level;Job URL;Workplace Type;Country;Salary Range;Location;Portal
Spotify;82%;Android Developer;Mid Level;...
```

Never include the header.

---

# Missing Information

If a value is unavailable, leave the field empty.

Preserve the delimiters.

Example:

```text
Example Company;76%;Android Developer;Mid Level;;Hybrid;Netherlands;;Amsterdam;
```

Do not replace missing values with:

- N/A
- Unknown
- Not provided
- None
- -
- ?

unless a specific company-name rule below requires `[Unknown]`.

---

# Company Name

If the real company name is known, use the real company name.

Example:

Booking.com

Do not use brackets around a real company name.

Correct:

Booking.com

Incorrect:

[Booking.com]

---

# Unknown Company — Industry Can Be Inferred

If the real company name is unavailable but the company's industry can reasonably be inferred from the vacancy, use a concise industry description inside square brackets.

Examples:

[Fintech Company]

[Healthcare Company]

[Automotive Company]

[EdTech Company]

[SaaS Company]

[E-commerce Company]

[Cybersecurity Company]

[Telecommunications Company]

Do not invent a specific company name.

---

# Completely Unknown Company

If neither the company name nor its industry can reasonably be determined, use:

[Unknown]

This rule applies only to the Company Name column.

Other missing columns should normally remain empty.

---

# Profile Match

Use the Profile Match percentage already determined by `resume-match-evaluator`.

Format:

<number>%

The `%` symbol must appear immediately after the number.

Correct:

80%

Incorrect:

80

Incorrect:

%80

Incorrect:

80 %

Do not recalculate the Profile Match merely because `log ver` was requested.

Use the match associated with the current vacancy.

---

# Missing Profile Match

If Profile Match has not been calculated for the current vacancy, leave the field empty.

Example:

```text
Example Company;;Android Developer;Mid Level;...
```

Do not invent a percentage.

---

# Job Role

Use the vacancy's actual job title whenever available.

Examples:

Android Developer

Android Engineer

Senior Android Engineer

Kotlin Developer

Mobile Software Engineer

Backend Engineer

Preserve the meaningful title from the vacancy.

Do not replace it with the user's current profession.

---

# Level

Use the level determined by `job-analyzer`.

Preferred standardized values:

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

If the level genuinely cannot be determined, leave the field empty.

Do not invent seniority.

---

# Job URL

If the user supplied a URL with the vacancy, use that URL in the Job URL column.

This includes URLs from:

- LinkedIn
- Company career pages
- Indeed
- Glassdoor
- Recruitment agencies
- Other job portals

Preserve the original vacancy URL when possible.

Do not replace the original job URL with a company's homepage.

---

# URL Priority

When multiple URLs exist, prioritize:

1. URL explicitly supplied by the user for the vacancy.
2. Direct job listing URL.
3. Company career listing URL.
4. Recruitment portal listing URL.

Do not use unrelated links.

---

# Workplace Type

Use one of these values when determinable:

Remote

Hybrid

On-site

If the vacancy provides additional useful constraints, keep this field concise.

Preferred:

Hybrid

rather than:

Hybrid - 2 days office and 3 days remote

Detailed workplace conditions belong to analysis, not this compact log.

---

# Remote Restrictions

A geographically restricted remote position is still:

Remote

Country restrictions should be represented through the Country column when appropriate.

Example:

Remote;Netherlands

or:

Remote;European Union

depending on the vacancy.

---

# Country

Use the country where the position is based.

Examples:

Netherlands

Germany

Belgium

France

Bulgaria

Spain

United Kingdom

If the vacancy is explicitly remote across a region rather than tied to one country, a region may be used when that is the most accurate available information.

Examples:

European Union

Europe

EMEA

Do not infer the country solely from the company's headquarters.

---

# Salary Range

Only include salary information explicitly provided by the vacancy or reliable vacancy context.

Examples:

€50,000-€65,000/year

€4,500-€5,500/month

€70/hour

Keep the representation concise.

---

# Salary Rules

Do not:

- Estimate market salary.
- Insert the user's desired salary.
- Calculate a likely salary.
- Convert salary unless necessary.
- Invent missing salary information.

If the vacancy does not provide compensation information, leave the field empty.

---

# Location

Use the city or specific job location when available.

Examples:

Amsterdam

Utrecht

The Hague

Rotterdam

Zaandam

Sofia

Sant Cugat del Vallès

If the role is remote and no meaningful city is associated with the position, leave the Location field empty.

Do not use company headquarters unless it is also the job location.

---

# Portal

Identify the source or platform of the vacancy when possible.

Examples:

LinkedIn

Indeed

Glassdoor

Company Website

Recruiter

EURES

If a URL clearly identifies the portal, use that information.

Example:

A `linkedin.com/jobs/...` URL should produce:

LinkedIn

A vacancy hosted directly on the employer's careers website should generally produce:

Company Website

---

# Portal vs Application Method

Portal means where the vacancy came from.

It does not necessarily mean where the application must ultimately be submitted.

Example:

The user provides a LinkedIn vacancy that says applications must be completed through the employer website.

Portal:

LinkedIn

The special application instruction is handled by `application-guardrails`.

Do not change Portal to Company Website merely because the final application occurs there.

---

# Semicolon Safety

Because semicolon is the delimiter, do not use unnecessary semicolons inside field values.

If the source contains semicolons, rewrite the field concisely without changing its meaning.

The final row must always contain exactly 10 logical fields.

---

# No Header

Never output:

Company Name;Profile Match %;Job Role;Level;Job URL;Workplace Type;Country;Salary Range;Location;Portal

The user already knows the schema.

Only output the data row.

---

# No Commentary

When `log ver` is requested, do not output:

- Explanation
- Analysis
- Resume recommendations
- Match reasoning
- Job summary
- Introductory sentence
- Closing sentence

Output only the Markdown code block containing the row.

---

# Example — Complete Data

```text
ExampleTech;81%;Android Developer;Mid Level;https://example.com/jobs/android-developer;Hybrid;Netherlands;€55,000-€70,000/year;Amsterdam;LinkedIn
```

---

# Example — Missing Salary

```text
ExampleTech;81%;Android Developer;Mid Level;https://example.com/jobs/android-developer;Hybrid;Netherlands;;Amsterdam;LinkedIn
```

---

# Example — Unknown Company but Known Industry

```text
[Fintech Company];68%;Android Engineer;Mid Level;https://example.com/job;Remote;Netherlands;;;LinkedIn
```

---

# Example — Unknown Company and Industry

```text
[Unknown];57%;Kotlin Developer;Junior / Mid;;Hybrid;Germany;;Berlin;
```

---

# Language-Blocked Vacancy

A vacancy may still be logged even when the application workflow was stopped because of a mandatory unsupported language.

If the Profile Match was never calculated because the language check stopped the workflow, leave Profile Match empty.

Example:

```text
Example GmbH;;Android Developer;Mid Level;https://example.com/job;Hybrid;Germany;;Berlin;LinkedIn
```

Do not invent a match score merely to complete the log.

---

# Low-Match Vacancy

If Profile Match is below 50% and the user has not approved resume optimization, the vacancy can still be logged.

Example:

```text
ExampleTech;43%;Senior Android Engineer;Senior;https://example.com/job;Hybrid;Netherlands;;Amsterdam;LinkedIn
```

Logging does not require resume optimization approval.

---

# Optimized Resume Case

If the resume was optimized after the initial evaluation, use the standard Profile Match associated with the vacancy workflow.

Unless explicitly instructed otherwise, do not replace the original recruiter-style Profile Match with a hypothetical post-optimization score.

This keeps application logs comparable across vacancies.

---

# Current Vacancy Rule

Always associate `log ver` with the most recently active vacancy.

If several jobs were discussed, identify the current one from the conversation context.

Do not merge information from multiple vacancies.

---

# Information Priority

When conflicting information exists, prioritize:

1. Explicit information from the vacancy.
2. Explicit information supplied by the user about that vacancy.
3. Structured output from `job-analyzer`.
4. Existing workflow state.
5. Reasonable industry inference only where explicitly allowed.

Do not use unrelated information from other vacancies.

---

# Workflow Independence

`log ver` can be executed at different stages.

It may be requested:

- Immediately after job analysis.
- After Profile Match calculation.
- After resume optimization.
- After a language block.
- After the user declines optimization.
- After cover-letter generation.

Fill only the information currently available.

Do not force missing workflow stages merely to populate the log.

---

# Final Validation

Before returning the row, verify:

- Exactly 10 fields exist.
- Fields are separated by `;`.
- No header is present.
- Profile Match uses `<number>%`.
- Real company names are not wrapped in brackets.
- Estimated industry names are wrapped in brackets.
- Completely unknown company uses `[Unknown]`.
- Missing information is empty.
- Job URL is the original vacancy URL when available.
- Salary was not invented.
- Level was not invented.
- The row refers to the current vacancy.
- Output contains only one Markdown code block.

---

# Workflow Boundary

This skill only generates the job log.

It does not:

- Analyze the vacancy from scratch when structured analysis already exists.
- Calculate Profile Match.
- Optimize the resume.
- Modify HTML.
- Generate cover letters.
- Generate motivation letters.
- Generate resume change reports.
- Override application guardrails.
