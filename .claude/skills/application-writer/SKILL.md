---
name: application-writer
description: Write concise cover letters and motivation letters for the current job application, and summarize changes made to an optimized resume when the user says "report". Use only verified information from the user's resume and the active job posting.
---

# Application Writer

## Purpose

Create short application-writing materials for the active vacancy and report changes made to the user's resume.

This skill handles:

- Cover letters
- Motivation letters
- The `report` command after resume optimization

It does not analyze a vacancy from scratch, evaluate profile match, optimize the resume, or override application guardrails.

---

# Activation

Use this skill when the user asks for:

- `cover letter`
- `motivation letter`
- `report`

Interpret the request in the context of the most recently active vacancy and the latest resume workflow.

If no active vacancy or relevant resume context is available, ask only for the missing information needed to complete the requested writing task.

---

# Guardrail Dependency

Before writing application materials, respect the outcome of `application-guardrails`.

Do not continue past:

- A mandatory unsupported language requirement
- A special application instruction awaiting the user's confirmation
- A low-match approval gate awaiting the user's confirmation
- Any other explicit stop condition in the active workflow

A user request for a cover letter does not bypass a pending guardrail.

Do not invent or ignore application instructions. If the vacancy specifies a required subject line, phrase, question, submission channel, or document format, follow it only after the relevant guardrail has been cleared.

---

# Source of Facts

Use only facts supported by:

1. The user's existing resume and project source materials.
2. Information the user explicitly provided about their experience.
3. The active job posting.
4. Reasonable wording choices that do not add new factual claims.

Never invent:

- Employers, job titles, dates, or responsibilities
- Skills, tools, technologies, or language proficiency
- Projects, qualifications, or certifications
- Measurable outcomes, metrics, or business impact
- Personal motivations or biographical details the user has not shared

Do not present a preferred skill from the posting as experience the user has unless the resume supports it.

---

# Language

Write in the language requested by the user.

If no language is specified, use the language of the job posting. English and Turkish are the supported languages for this workflow.

Do not write an application letter in a language that the user has not requested or that the workflow does not support.

---

# Cover Letter

When the user says `cover letter`, write a concise, professional letter tailored to the active role.

The letter should:

- Name the role and company when known.
- Connect the user's strongest relevant, documented experience to the role.
- Mention only a small number of relevant skills or achievements.
- Explain the fit in natural language without repeating the resume.
- Use a clear opening, focused body, and brief closing.
- Stay short enough to read quickly, typically 3–4 compact paragraphs.
- Avoid generic claims, inflated enthusiasm, clichés, and unsupported accomplishments.

Use the company name only when it is known. If the company is unknown, address the employer neutrally without guessing a name.

Do not add a subject line unless the user asks for one or the posting requires one.

Output the letter itself without analysis, scoring, or commentary.

---

# Motivation Letter

When the user says `motivation letter`, write a concise statement of interest tailored to the active role.

The message should:

- State why the role is relevant to the user's documented background.
- Connect the user's genuine, supported interests or experience to the work.
- Explain what the user can contribute using evidence from the resume.
- Close with a brief, professional expression of interest.

Keep it short and fluent. Do not invent personal motivations, life stories, career goals, or facts about the company.

Output the letter itself without analysis, scoring, or commentary.

---

# Application Instructions

Check the active vacancy context for any application-specific requirements already identified by `job-analyzer` or `application-guardrails`.

If the posting requests a specific phrase, answer, recipient, subject line, or application channel and the user has cleared the guardrail:

- Include the requested detail accurately.
- Preserve the requested wording when necessary.
- Do not claim that the application was submitted.
- Do not send messages or submit an application.

---

# Report Command

When the user says `report`, list only the changes actually made to the resume HTML during the current active vacancy workflow.

Requirements:

- Use concise bullet points.
- Mention only changed content.
- Do not include unchanged sections.
- Do not add match analysis, recommendations, or general explanation.
- Do not claim changes that were not made.
- If no resume optimization has been completed in the current workflow, state briefly that there are no resume changes to report.

---

# Output Discipline

Keep the response focused on the requested artifact.

For a cover letter or motivation letter, output only the finished letter unless the user asks for additional material.

For `report`, output only the change bullets or the brief no-changes status.

Do not include:

- Profile-match calculations
- Resume analysis
- Job summaries
- Unrequested alternative drafts
- Explanations of the writing process
- Claims that an application was sent

---

# Workflow Boundary

This skill only writes application materials and reports completed resume edits.

It does not:

- Analyze the vacancy from scratch.
- Determine seniority or Profile Match.
- Decide whether resume optimization is permitted.
- Rewrite or optimize the HTML resume.
- Generate the job-log CSV.
- Override a language, application, or approval guardrail.

