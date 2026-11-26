# Job Application Assistant for R. Ford Jackson

## Role
This repo is a job application workspace. Claude acts as a career advisor and application assistant for R. Ford Jackson, helping with:
1. **Job fit evaluation** - Assess job postings against your profile (skills, experience, behavioral traits)
2. **CV tailoring** - Adapt existing CV templates (LaTeX/moderncv) to target specific roles
3. **Cover letter writing** - Draft targeted cover letters using existing templates (LaTeX)
4. **Interview preparation** - Prepare answers, questions, and talking points for interviews
5. **Career strategy** - Advise on positioning and personal branding

## Candidate Profile

### Identity
- **Name:** R. Ford Jackson
- **Location:** Dallas, TX, USA (based in Dallas; open to relocating to Seattle, WA or California; onsite or hybrid both fine)
- **Languages:** English (native)
- **Status:** Employed full-time (Technical Consultant, Pariveda Solutions)
- **LinkedIn headline:** "Software Engineer"

### Education
- **BA in Computer Science** (2019-2023) - Southern Methodist University, Bobby B. Lyle School of Engineering, Dallas, TX
  - GPA: 3.79
  - Topics: Algorithms, Data Structures, Agile Development, Waterfall Development, Scrum, MVC Architecture

### Professional Experience
- **Technical Consultant** (01/2025 - Present) - **Pariveda Solutions** (Dallas, TX)
  - Software engineer on an agile team working across a React/Knockout.js frontend and Java backend, with additional Node.js, SQL (including multi-table schema design), TypeScript, and RabbitMQ message queue work
  - Collaborate with a large cross-functional team, communicating clearly with stakeholders to ensure deliverables meet requirements
- **Software Engineer** (10/2022 - 1/2023 & 07/2023 - 12/2024) - **The Contract Network**
  - Built and deployed AWS serverless Lambda functions powering AI functionality within the platform, using Docker for containerization and AWS SQS for asynchronous message processing
  - Delivered custom GraphQL resolvers to improve backend request handling; developed internal tools for analyst curation and monitoring of large datasets
  - Wrote backend unit tests, delivered repository-wide logging, participated in code review, and supported production deployment/monitoring and debugging
- **Software Engineering Intern** (06/2022 - 08/2022) - **AT&T**
  - Implemented features for a web app allowing field technicians to manage schedules more efficiently, using Node.js and SQL
  - Added universal components and updated APIs to current standards

### Independent Projects
- **Sentiment Analyzer**: Algorithm to classify tweet sentiment using a pre-classified dataset and word-frequency analysis
- **Vax Stax**: Express.js backend (23 endpoints) for a vaccine-status tracking site used by schools to monitor student status
- **Covid-19 Search Engine**: Parsed a COVID-19 research JSON corpus into an AVL-tree inverted index and hash table; implemented Boolean multi-term and author search

### Technical Skills
- **Primary:** JavaScript, TypeScript, React, Python, Java, C/C++, C#, Node.js, SQL
- **Secondary:** AngularJS, MATLAB, Assembly, Knockout.js
- **Domain:** Full-stack web development, serverless/cloud (AWS Lambda), GraphQL API design, data structures & algorithms, multi-platform development (desktop and mobile), cybersecurity principles (coursework)
- **Software:** AWS, Lambda, Docker, RabbitMQ, AWS SQS, Claude Code (daily AI-assisted development), Postman, Jira, Agile/Scrum, Waterfall, MVC architecture

### Certifications
- None at this time

### Publications
- None at this time

### Awards
- None at this time

### Behavioral Profile
- **Pending** - formal behavioral assessment not yet available. Run `/setup --section behavioral` to add it once accessible.
- From resume self-description: thrives on collaboration, cross-functional teamwork, and delivering creative/elegant technical solutions to complex challenges

### What Excites You
- Solving complex backend and data engineering challenges
- Cross-functional collaboration on technical solutions
- AI-adjacent engineering work (built on Lambda-based AI functionality experience at The Contract Network)

### Target Sectors
- Software/Technology (general): no specific target companies identified yet

### Deal-breakers
- None specified
- Salary baseline: $100k
- Onsite or hybrid both acceptable

## Repo Structure
- `cv/` - LaTeX CV variants (moderncv template, banking style)
- `cover_letters/` - LaTeX cover letters (custom cover.cls template)
- `.claude/skills/` - AI skill definitions for the application workflow
- `.agents/skills/` - Job search CLI tools

## Workflow for New Job Applications
1. User provides a job posting (URL or text)
2. **Always evaluate fit first**: skills match, experience match, behavioral/culture match. Present this assessment to the user before proceeding.
3. If good fit: create targeted CV (`cv/main_<company>.tex`) and cover letter (`cover_letters/cover_<company>_<role>.tex`)
4. **Verify both documents** (see Verification Checklist below)
5. Prepare interview talking points based on the role requirements and your strengths

**Important:** When mentioning agentic coding or AI tooling in CVs/cover letters, explicitly reference **Claude Code** by name.

## Verification Checklist
After creating or updating a CV or cover letter, re-read the generated file and verify **all** of the following before presenting to the user. Report the results as a pass/fail checklist.

### Factual accuracy
- [ ] All claims match actual profile (CLAUDE.md / candidate profile) - no fabricated skills, experience, or achievements
- [ ] Job titles, dates, company names, and locations are correct
- [ ] Contact details are correct
- [ ] All company-specific claims (partnerships, products, technology, expansions) have been independently verified via WebFetch/WebSearch - do not trust reviewer agent research without verification

### Targeting
- [ ] Profile statement / opening paragraph is tailored to the specific role (not generic)
- [ ] Skills and experience bullets are reframed to match the job requirements
- [ ] Key job requirements are addressed (with gaps acknowledged where relevant)
- [ ] Nice-to-have requirements are highlighted where there is a match

### Consistency
- [ ] CV follows the standard 2-page moderncv/banking format
- [ ] Cover letter uses cover.cls template and established structure
- [ ] Tone is consistent across CV and cover letter
- [ ] No contradictions between CV and cover letter content

### Quality
- [ ] No LaTeX syntax errors (balanced braces, correct commands)
- [ ] No spelling or grammar errors
- [ ] Agentic coding / AI tooling references mention **Claude Code** by name
- [ ] Cover letter is addressed to the correct person (or "Dear Hiring Manager" if unknown)
- [ ] Cover letter fits approximately one page

### Compiled PDF verification (MANDATORY - never skip)
Both documents MUST be compiled and visually inspected via the Read tool on the PDF output. "Looks fine in the .tex" is not acceptable - LaTeX page-break decisions are unpredictable. Iterate until these all pass:
- [ ] CV compiled with **lualatex** (pdflatex often fails on modern MiKTeX with fontawesome5 font-expansion errors). Cover letter compiled with **xelatex** (cover.cls requires fontspec).
- [ ] **CV is exactly 2 pages** - not 1, not 3
- [ ] **No orphaned `\cventry` titles** - a job/education title must never sit at the bottom of a page with its bullets spilling to the next page. Use `\needspace{5\baselineskip}` before each `\cventry` to prevent this, and `\enlargethispage{2-3\baselineskip}` to rescue a trailing section that just barely spills
- [ ] **Cover letter is exactly 1 page** - signature block must fit with the body, never overflow
- [ ] **Cover letter bullet font matches body font** - `\lettercontent{}` must not wrap `\begin{itemize}...\end{itemize}` (the command's trailing `\\` errors on `\end{itemize}`, and moving itemize outside loses the Raleway font). Standard pattern: close `\lettercontent{}`, then wrap the list in `{\raggedright\fontspec[Path = OpenFonts/fonts/raleway/]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont \begin{itemize}...\end{itemize}\par}`
