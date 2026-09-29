---
name: application-guardrails
description: Control blocking conditions and confirmation gates in the job application and resume optimization workflow. Use this skill to handle mandatory language restrictions, hidden application instructions, unusual application methods, low profile-match confirmation, and workflow stop/resume decisions.
---

# Application Guardrails

## Purpose

Control whether the job application workflow is allowed to continue.

This skill acts as a gatekeeper between:

- Job analysis
- Resume evaluation
- Resume optimization
- Application writing

Its responsibility is to prevent the workflow from continuing when an important condition requires either:

1. Immediate termination, or
2. Explicit user confirmation.

This skill does not analyze the resume in depth and does not rewrite it.

---

# Core Principle

Never continue automatically when a blocking condition or confirmation gate has been triggered.

A resume optimization that ignores an important application instruction may harm the user's application.

The workflow must therefore check guardrails before generating an optimized resume.

---

# Guardrail Priority

Evaluate guardrails in this order:

1. Mandatory unsupported language
2. Special or hidden application instructions
3. Application-channel restrictions
4. Eligibility restrictions
5. Profile Match below 50%
6. Resume optimization eligibility

Higher-priority blocks take precedence over lower-priority conditions.

---

# Guardrail 1 — Mandatory Language

The user's supported application languages for this workflow are:

- English
- Turkish

If the vacancy explicitly requires another language, stop the workflow.

Examples:

- Dutch required
- Fluent Dutch required
- German B2 required
- Professional French required
- Spanish required
- Native Polish required
- Swedish fluency required

Do not optimize the resume.

Do not generate a cover letter.

Do not attempt to compensate for the language requirement through stronger technical alignment.

---

# Mandatory vs Preferred Language

Only block when the language is mandatory.

Blocking examples:

"Fluent Dutch is required."

"You must speak German at B2 level."

"Professional proficiency in French is mandatory."

"Candidates must be fluent in Spanish."

Non-blocking examples:

"Dutch is a plus."

"German would be advantageous."

"French is preferred."

"Knowledge of Spanish is beneficial."

"Swedish is nice to have."

---

# Job Posting Language

Do not assume that the language in which the vacancy is written is automatically mandatory.

Example:

A vacancy written in Dutch may still only require English.

Analyze the actual requirements.

Likewise, a vacancy written in German does not automatically prove that German is mandatory.

---

# Language Block Output

When an unsupported mandatory language is detected, stop immediately.

Output only:

Company: <company_name>
<job_level>
Profile match: N/A
Required language: <language>

Do not add:

- Explanations
- Recommendations
- Resume content
- Alternative jobs
- Cover letters
- Analysis

---

# Multiple Mandatory Languages

If multiple unsupported languages are explicitly mandatory, list them concisely.

Example:

Company: Example Company
Mid Level
Profile match: N/A
Required language: Dutch, German

Then stop.

---

# Guardrail 2 — Hidden or Special Application Instructions

Inspect the vacancy for instructions designed to test whether the applicant actually read the posting.

Examples:

- "Include the word BLUE in your application."
- "Start your cover letter with..."
- "Mention your favorite Android API."
- "Include a specific phrase in the subject line."
- "Answer the following question in your application."
- "Tell us which feature of our product you like."
- "Include your GitHub username in the first paragraph."
- "Mention this job code when applying."

These instructions must not be silently ignored.

---

# Special Instruction Confirmation

When such an instruction exists, inform the user before resume optimization.

Output:

Company: <company_name>
<job_level>
Profile match: <percentage_if_available_or_N/A>

Dikkat: <short description of the instruction>

Devam etmem için "tamam" yaz.

Stop after this output.

Do not generate the resume yet.

---

# Guardrail 3 — Application Channel Restrictions

Detect when the vacancy requires a specific application method.

Examples:

- Apply only through the company website.
- Applications by email only.
- Do not apply through LinkedIn.
- LinkedIn applications will not be reviewed.
- Send the application directly to a recruiter.
- Apply through a specific external portal.
- Applications through recruitment agencies are not accepted.

These instructions can materially affect whether the application is valid.

---

# Normal Application Links

A normal company application link is not automatically a special warning.

For example:

"Apply here"

followed by the company's careers page is normal.

Only trigger a confirmation gate when the posting contains a meaningful restriction or unusual instruction that the user could easily miss.

---

# Application Channel Warning

When a meaningful application-channel restriction exists:

Output:

Company: <company_name>
<job_level>
Profile match: <percentage_if_available_or_N/A>

Dikkat: Başvuru yalnızca <required_method> üzerinden kabul ediliyor.

Devam etmem için "tamam" yaz.

Do not continue until confirmed.

---

# Guardrail 4 — Important Eligibility Restrictions

Detect explicit restrictions that could make the user ineligible regardless of resume quality.

Examples:

- Must already have authorization to work in a specific jurisdiction.
- No visa sponsorship available.
- Must reside in a specific country.
- Must be able to work from a specific office.
- Security clearance required.
- Specific professional license required.
- Mandatory travel requirement.
- Mandatory relocation requirement.
- Candidate must be enrolled as a student.
- Internship requires active university enrollment.

Do not automatically treat every eligibility condition as a hard block.

Determine whether the condition clearly conflicts with known supported information.

---

# Unknown Eligibility

If eligibility cannot be determined from available information, do not invent an answer.

If the requirement is critical to applying, ask the user.

Example:

Company: <company_name>
<job_level>
Profile match: <percentage_if_available_or_N/A>

Dikkat: İlan aktif öğrenci statüsü gerektiriyor. Bu şartı karşılayıp karşılamadığını doğrulamam gerekiyor.

Stop and wait for the user's answer.

---

# Eligibility Already Supported

If available project context clearly establishes that the user satisfies an eligibility requirement, do not unnecessarily interrupt the workflow.

Do not repeatedly ask for information already available in the current workflow context.

---

# Guardrail 5 — Low Profile Match

After `resume-match-evaluator` calculates the current Profile Match, check the result.

If:

Profile Match < 50%

resume optimization requires explicit confirmation.

---

# Low Match Output

Output:

Company: <company_name>
<job_level>
Profile match: <percentage>%
Eşleşme %50'nin altında. Resume'yi optimize etmemi istiyor musun?

Stop.

Do not generate HTML.

---

# Low Match Confirmation

The workflow may continue when the user clearly confirms.

Examples of acceptable confirmations:

- tamam
- evet
- devam
- optimize et
- yap
- proceed
- yes

Interpret obvious affirmative responses naturally.

Do not require the exact word `tamam` when the user's intention is unambiguous.

---

# Negative Response

If the user declines optimization after a low match score, stop the resume workflow.

Do not generate the HTML resume.

---

# Multiple Guardrails

More than one guardrail may apply to the same vacancy.

Do not overwhelm the user with separate sequential warnings when multiple known confirmation-level issues can be presented together.

Example:

Company: Example Company
Senior
Profile match: 43%

Dikkat:
- Başvurular yalnızca şirketin websitesinden kabul ediliyor.
- Cover letter içinde "ANDROID2026" kodunun belirtilmesi gerekiyor.
- Profile match %50'nin altında.

Devam etmem için "tamam" yaz.

This allows one confirmation to acknowledge all currently known confirmation-level conditions.

---

# Hard Blocks vs Confirmation Gates

Distinguish between:

## Hard Block

The workflow must terminate.

Primary example:

Mandatory unsupported language.

No confirmation should override a hard language block within the normal workflow.

---

## Confirmation Gate

The workflow pauses but may continue after user approval.

Examples:

- Hidden application instruction
- Special application channel
- Low Profile Match
- Important unusual application condition
- Eligibility uncertainty requiring user clarification

---

# Confirmation State

Once the user has confirmed a specific warning, do not repeatedly ask for confirmation for the same condition during the same vacancy workflow.

Example:

1. Profile Match is 46%.
2. User says `tamam`.
3. Resume optimization begins.

Do not ask again because the match remains 46%.

---

# New Guardrail After Confirmation

If a new important condition is discovered after the previous confirmation, the workflow may pause again.

Example:

The user confirmed a low match.

Later analysis reveals:

"Applications must include the phrase MOBILE-FIRST."

This new condition should be surfaced before final application material is produced.

---

# New Vacancy Reset

Confirmation applies only to the current vacancy.

When the user starts a new job posting, reset confirmation state.

Do not assume that confirmation from a previous vacancy applies to a new one.

---

# Resume Match >= 85%

If no other guardrail applies and:

Profile Match >= 85%

the workflow terminates normally with:

Company: <company_name>
<job_level>
Profile match: <percentage>%
Bu hali iyidir

Do not optimize the resume.

---

# Resume Match 50–84%

If:

Profile Match >= 50%

and:

Profile Match < 85%

and no other guardrail applies:

Resume optimization may proceed automatically.

No additional confirmation is required solely because optimization will occur.

---

# Resume Match < 50%

If:

Profile Match < 50%

optimization is blocked until confirmation.

After confirmation, `resume-optimizer` may proceed.

---

# Guardrail Decision Table

| Condition | Action |
|---|---|
| Mandatory English | Continue |
| Mandatory Turkish | Continue |
| Mandatory other language | Stop |
| Other language preferred only | Continue |
| Hidden application instruction | Warn + wait |
| Special application restriction | Warn + wait |
| Critical eligibility uncertainty | Ask + wait |
| Profile Match >= 85% | No optimization |
| Profile Match 50–84% | Optimize |
| Profile Match < 50% | Ask + wait |
| User confirms low match | Optimize |
| User declines low match | Stop |

---

# No Unnecessary Interruptions

Do not interrupt the workflow for minor details.

Examples that normally do not require confirmation:

- Standard Equal Opportunity statements
- Generic company culture descriptions
- Benefits
- Normal application links
- Optional certifications
- Preferred technologies
- Preferred languages
- Generic requests for a resume
- Generic requests for a cover letter
- Normal background-check notices

The guardrail system should catch meaningful application risks, not create unnecessary friction.

---

# Do Not Invent Warnings

Only warn about conditions actually supported by the vacancy.

Do not speculate that:

- Easy Apply may not work.
- The recruiter may expect a cover letter.
- A language might secretly be required.
- Relocation may be necessary.
- Sponsorship may be unavailable.
- A portfolio may be mandatory.

unless the posting provides evidence.

---

# User-Facing Style

Guardrail messages must be:

- Short
- Direct
- Actionable

Do not provide lengthy explanations.

The user should immediately understand:

1. What the issue is.
2. Whether the workflow has stopped.
3. Whether they need to respond.

---

# Workflow Integration

Normal workflow:

Job Posting
    ↓
job-analyzer
    ↓
application-guardrails
    ↓
resume-match-evaluator
    ↓
application-guardrails
    ↓
resume-optimizer
    ↓
Final HTML Resume

The guardrails may be checked more than once because some conditions become known only after the Profile Match has been calculated.

---

# Pre-Match Guardrails

Before Profile Match calculation, check:

- Mandatory languages
- Hidden instructions
- Application restrictions
- Obvious eligibility restrictions

---

# Post-Match Guardrails

After Profile Match calculation, check:

- Profile Match >= 85%
- Profile Match 50–84%
- Profile Match < 50%

---

# Workflow Boundary

This skill controls workflow permission.

It does not:

- Perform detailed vacancy analysis.
- Calculate Profile Match.
- Rewrite resume content.
- Modify HTML.
- Generate CSV logs.
- Write cover letters.
- Write motivation letters.
- Generate resume change reports.

Those responsibilities belong to the corresponding skills.