---
tags: [ai-first, blueprint, engineering-system, thought-leadership]
type: framework
created: 2026-01-03
status: active
context: General version, decoupled from any employer. Evolved from the DevSecAI version when it became clear that role might not continue. All original work by Abiola Fatunla.
related:
  - "[[devsecai-version]]"
  - "[[anthropic-cursor-research]]"
  - "[[engineering-system-as-service]]"
  - "[[stakeholder-engineering-agent]]"
  - "[[agent-verification-layer]]"
  - "[[moonshot-builds]]"
---

# Building an AI-First Engineering Organisation

## A Blueprint for Establishing Engineering Culture from Day One

**Author:** Abiola Fatunla

---

## Executive summary

This document captures my blueprint for building an AI-first engineering organisation from the ground up. I've spent considerable time researching how frontier AI companies, particularly Anthropic and Cursor, have structured their engineering practices. My research has led me to synthesise what I believe is a compelling framework for any organisation looking to build this way from day one.

The opportunity here is significant. If you're building something new, you have the rare advantage of establishing AI-first principles into your foundation rather than retrofitting them onto legacy processes. I'm convinced this head start matters enormously. Organisations trying to transform existing ways of working face resistance that greenfield teams simply don't encounter.

What makes this particularly interesting for teams operating in the DevSecOps and AI security space is the potential for a virtuous cycle. You're building AI security products whilst simultaneously operating as an AI-native organisation. You can dogfood your own security practices, which creates continuous feedback between product improvement and operational excellence.

That said, while this blueprint is framed around building from day one, the principles apply equally to organisations transforming existing practices. The core ideas around primitive fluency, delegation frameworks, and cultural foundations don't change. What changes is the sequencing and the change management required to get there. I'll touch on this briefly after laying out the case for starting fresh.

**Core principles I believe matter:**

1. **Primitive fluency as foundation.** Workflows need to be expressed in explicit, agent-legible primitives: state, artifacts, diffs, tests, approvals, rollback, and traceability. GUI abstractions that hide these primitives block agents from acting autonomously.

2. **Security as first-class primitive, not bolt-on.** For anyone in this domain, secure automation means agents operating within built-in guardrails. Policy-as-code validation, audit trails, and segregation of duties should all be expressed as workflow primitives, not GUI steps.

3. **Terminal-native, artifact-centric workflows.** Code and markdown as systems of record. Agents execute end-to-end by manipulating explicit artifacts, not navigating opaque interfaces.

4. **Everyone semi-technical by default.** The entire organisation, engineers, product, design, GTM, should understand repos, diffs, and PR flows to leverage agents effectively.

5. **Aggressive AI use with disciplined supervision.** Push boundaries on delegation whilst maintaining high standards for validation, especially for security-sensitive work.

---

## The case for AI-first from day one

### What the data tells us

My research into Anthropic's internal study of 132 engineers, 53 in-depth interviews, and 200,000 agent transcripts reveals the magnitude of change that's possible.

**Productivity transformation:**
- Engineers using AI in 60% of their work (up from 28% twelve months prior)
- 50% self-reported productivity gains (up from 20%)
- 67% increase in merged pull requests per engineer per day after adopting agentic coding tools
- 27% of AI-assisted work consists of tasks that wouldn't have been done otherwise. These are the "papercuts" and quality-of-life improvements that compound over time

**Workflow revolution:**
- 79% of interactions with terminal-based agents classified as "automation" versus 49% on chat interfaces
- Agents now chain 21 consecutive tool calls without human intervention (up from 10 six months ago)
- Human interventions per coding session decreased by 33%

**The "fullstack" effect:**
- Backend engineers building complex UIs
- Security team members analysing unfamiliar codebases in languages they don't typically use
- Non-technical employees debugging systems and building internal tools

### Why I believe this matters

Based on what I've observed, organisations positioned to get this right share certain characteristics:

1. **They're building AI-native products.** If your customers will need to work with AI systems, you should understand AI-native operations intimately to build effective solutions.

2. **They bring DevSecOps expertise.** Domain expertise in secure software delivery provides a natural framework for safe AI adoption. Policy-as-code, automated compliance, audit trails. These aren't new concepts, they're just applied differently.

3. **They're starting fresh.** Unlike enterprises constrained by legacy processes, new organisations can design workflows from first principles without technical debt or cultural baggage.

4. **They can attract talent that understands both security and AI.** This rare combination enables sophisticated implementation of guardrails that balance velocity with safety.

### Applying this to existing organisations

If you're not starting fresh, the same principles apply. The difference is in how you get there.

The approach I'd recommend is a beachhead strategy. Start with one team or one project that adopts these practices fully. Let them prove it works, document what they learn, and build internal credibility. Then expand from there. Trying to flip an entire organisation at once rarely works. You're fighting too many battles simultaneously.

The key obstacles in transformation are usually cultural, not technical. Legacy processes exist because someone built them for good reasons at the time. GUI-heavy workflows persist because they're familiar. The abstraction tax framework still applies, but you'll need to make the case for why change is worth the short-term disruption.

The good news: the productivity gains documented in this blueprint create their own momentum. Once a team experiences 50%+ improvement, the argument for expanding becomes much easier to make.

---

## Core architectural principles

### Primitive fluency: the shared substrate

**What are primitives?** The explicit, agent-legible building blocks that enable autonomous operation.

| Primitive | Description | Implementation |
|-----------|-------------|----------------|
| **State & Domain Memory** | Current system condition and persistent context | `progress.txt`, feature lists, `memory.md` files |
| **Artifacts** | Versioned representations of work | Code, markdown, policies-as-code, configs in Git |
| **Change Records** | Deltas between states | Git commits with descriptive messages |
| **Checks/Tests** | Objective validation | Unit tests, security scans, policy validation |
| **Approvals/Gates** | Human oversight points | PR reviews, production deploy approvals |
| **Rollback** | State restoration | Git revert, feature flags, infrastructure snapshots |
| **Traceability** | Audit trails | Git logs, PR history, agent session transcripts |

**Why this matters.** Cursor spent $57K on a CMS before realising it created an "abstraction tax". Agents couldn't operate end-to-end because state was hidden in opaque GUIs. After migrating to markdown + Git in three days (using 344 agent requests), their team could delegate entire content workflows to agents.

The lesson I take from this: GUI abstractions become walls between agents and work. Every tool should be evaluated against the question: "Can an agent use this?"

### The abstraction tax framework

Before adopting any tool or process, I believe you should evaluate:

1. **Does it hide state?** If yes, agents can't reason about it. That's an abstraction tax.
2. **Does it require GUI interaction?** If yes, agents can't automate it. That's an abstraction tax.
3. **Does it introduce dependencies?** If yes, agents manage more complexity. That's an abstraction tax.
4. **Does it simplify work for agents?** If yes, it's a useful abstraction.

This framework should guide all tooling decisions.

### Security as first-class primitive

For anyone operating in the security space, security cannot be a bolt-on. It must be encoded into workflow primitives from the start.

**Policy-as-code everywhere:**
- Security policies defined in Open Policy Agent (OPA) or similar
- Automated policy checks in CI/CD
- Agents can read and propose changes to security policies, but not unilaterally modify them

**Audit trails as default:**
- All agent actions logged with full context
- Non-compliance triggers immediate alerts
- Evidence generation automated for SOC2/ISO 27001 compliance

**Segregation of duties without GUI fallback:**
- Role-based permissions defined in code
- An agent can generate a security policy, but a security engineer must review and approve
- Production changes require human approval, even when agents prepare them

**AI-specific security checks:**
- Prompt injection tests in CI/CD
- Model output validation
- Jailbreak detection for AI features
- Secret scanning (GitGuardian, TruffleHog) on all commits

---

## The harness pattern: enabling long-running agents

### The problem of multi-session memory

Even the most capable AI models fail at complex projects when given only high-level prompts. Anthropic's research documented two failure modes that I've observed repeatedly:

1. **One-shotting.** Agents attempt everything at once, run out of context mid-task, and leave half-finished work.
2. **Premature completion.** Agents declare victory after partial progress, missing large portions of functionality.

### The solution: session-based workflow with persistent state

Adapted from Anthropic's research, I believe in implementing a structured workflow pattern for complex projects.

**Project initialisation** (one-time setup):
- Create `dev-setup.sh` script to bootstrap and verify the development environment (idempotent, safe to run repeatedly)
- Create a comprehensive feature list with all requirements marked "failing"
- Initialise Git repository with scaffolding
- Create `progress.txt` for tracking work across sessions
- Create `memory.md` with project conventions and context
- Define acceptance criteria and test requirements

**Session workflow** (every working session):
1. Read progress files and Git logs to understand prior work
2. Run `dev-setup.sh` to verify environment health
3. Select a single feature to implement
4. Implement and test the feature end-to-end
5. Commit changes with descriptive messages
6. Update progress logs and feature list
7. Leave codebase in "clean state". No major bugs, well-documented

**Why this works.** It mirrors how effective engineers operate. Orient using history, tackle one task at a time, test thoroughly, document progress, leave clean state. The workflow externalises these practices into explicit artifacts that persist across sessions.

### Security-enhanced harness

For security-focused organisations, the harness should include additional security gates:

```
Session Start:
├── Read progress files and Git logs
├── Run dev-setup.sh (verify environment)
├── Execute security scan baseline
├── Verify no outstanding vulnerability tickets
└── Select next feature

Implementation:
├── Write failing tests (TDD)
├── Implement feature
├── Run unit tests
├── Run security tests (SAST)
├── Run dependency scan (SCA)
└── Iterate until all pass

Session End:
├── Commit with descriptive message
├── Update progress logs
├── Generate security evidence artifact
├── Update feature list status
└── Leave clean state
```

---

## Cultural foundations

### Building an AI-native organisation from day one

The approach isn't merely technical. It requires establishing specific cultural norms from the outset. Based on my research, I believe these are the ones that matter most.

**1. Aggressive AI use as default**

Expectation: AI should be the first tool reached for. Engineers justify *not* using AI rather than justifying its use.

Implementation:
- Onboarding includes mandatory training on agent tools and effective prompting
- Code review templates ask "Could AI have helped here? Was it used?"
- Performance reviews explicitly assess AI leverage and productivity gains
- Internal success stories shared widely
- Recognition for engineers who push AI boundaries responsibly

**2. High supervision standards**

I'm convinced that aggressive use must be balanced with validation requirements, especially for high-stakes work.

Implementation:
- Code review checklists verify AI outputs were validated
- Security-sensitive code requires explicit human review regardless of origin
- Incident postmortems examine whether AI was used appropriately
- Training includes case studies of AI-generated bugs and how to catch them

**3. Explicit discussion of trade-offs**

Organisations should acknowledge AI's potentially negative impacts openly rather than suppressing concerns.

Implementation:
- Regular forums dedicated to discussing AI's impact on work and careers
- Include concerns and mitigation strategies in internal documentation
- Leadership acknowledges trade-offs honestly
- Anonymous feedback mechanisms for raising issues without career risk

**4. "Docs to demos": prototype-first development**

Instead of lengthy specification documents, I believe in prototyping rapidly and gathering real feedback.

Traditional flow: Idea → specification → roadmap debate → implementation → launch → feedback

Better flow: Idea → Claude prototype → immediate internal launch → usage tracking → data-driven prioritisation

Benefits:
- Features go from concept to working prototype in hours, not weeks
- Real behaviour data over theoretical opinions
- Intense dogfooding feedback loop
- Reduced planning overhead

Risk mitigation:
- Initial prototypes internal-only
- Prototype phase gathers edge cases before production design
- Production implementation may differ substantially from prototype

**5. Everyone semi-technical**

The entire organisation, engineers, product, design, GTM, should understand repos, diffs, and PR flows.

Training requirements:
- All employees complete Git basics (clone, commit, push, PR)
- Provide templates and `memory.md` examples
- Visual diff UIs (Cursor, VS Code) lower barriers
- Marketers submit blog posts as PRs
- Designers commit UI changes
- Product managers prototype features with agents

This eliminates handoff friction and enables anyone with an idea to implement it.

**6. Fuzzing rituals**

Before every major release, the team gathers for "fuzz sessions". Structured chaos testing.

For security-focused organisations, this includes adversarial testing:
- Prompt injection attempts
- Privilege escalation scenarios
- Policy bypass attempts
- Data exfiltration probes

These sessions function as quality assurance, security hardening, and team cohesion building.

---

## Skill development and preservation

### The paradox of supervision

The central challenge I keep coming back to: effectively supervising AI-generated code requires the very coding skills that may atrophy from AI overuse.

Research findings on skill atrophy concerns:
- "If you were to debug a hard issue yourself, you'd spend time reading docs and code, building a model of how the system works. There's a lot less of that when Claude gets you to the problem right away."
- "I used to explore every config to understand what the tool can do but now I rely on AI to tell me how to use new tools."
- Junior engineers face highest risk. They may never develop the deep skills that enable senior-level judgement.

### My recommended mitigation strategy

**1. Deliberate practice without AI**

Monthly "no-AI days" where engineers work on small features or refactors without AI assistance. Purpose: maintain deep skills through regular exercise.

**2. Redesigned mentorship**

Traditional mentorship is eroding as junior engineers "just ask Claude instead." I believe organisations need to counter this by:
- Structured pairing programmes where junior and senior engineers work together with AI as tool but relationships as priority
- Regular "office hours" where senior engineers are explicitly available for discussion
- Performance reviews expecting senior engineers to actively mentor, measured through junior feedback

**3. Learning pathways for AI augmentation**

Training that teaches fundamentals deeply *and* effective AI use:
- "AI debugging" skills. Recognising when AI is wrong, recovering, generating better prompts
- Progression from AI as learning aid → productivity tool → supervised autonomous agent
- Checkpoints requiring demonstrated independent capability before advancing

**4. Supervision certification**

For high-stakes work (security-sensitive code, core infrastructure), I believe organisations should require demonstrated ability to:
- Identify subtle bugs in AI-generated code
- Understand security and performance implications
- Generate alternative approaches when AI's first attempt fails
- Explain architectural trade-offs in the engineer's own words

---

## Organisational structure

### Roles and responsibilities

**Software Engineers** (core team):

Primary responsibilities:
- Decompose problems into AI-delegable and human-retained components
- Write effective prompts and provide sufficient context
- Supervise agent outputs for correctness, security, maintainability
- Conduct final reviews and make architectural decisions
- Maintain deep technical skills through deliberate practice
- Mentor junior engineers in both traditional and AI-augmented workflows

Key capabilities:
- Strong CS fundamentals (to enable effective supervision)
- Prompt engineering and agent orchestration
- Judgement about appropriate delegation
- Security and compliance awareness
- Communication and collaboration (increasingly important as direct coding decreases)

**Security Engineers:**

Primary responsibilities:
- Define policies-as-code (OPA, Sentinel)
- Audit agent-generated changes for security implications
- Manage secrets and credentials
- Operate compliance automation
- Build AI-specific security checks (prompt injection, jailbreak detection)

Key capabilities:
- Deep security expertise across application, infrastructure, and AI domains
- Policy-as-code fluency
- Threat modelling for AI systems
- Incident response for AI-related failures

**AI Platform Engineers:**

Primary responsibilities:
- Build and maintain agent harnesses and tooling
- Optimise agent performance (latency, cost, reliability)
- Create observability for agent systems
- Build reusable agent patterns and tools
- Integrate security controls into agent execution

Key capabilities:
- Deep understanding of LLM capabilities and limitations
- Developer tooling expertise
- Systems thinking for distributed systems
- Security engineering for sandboxing and permission controls

**Product and Design** (with primitive fluency):

Expectations:
- Understand Git, PRs, diffs at operational level
- Prototype features using agents
- Submit PRs for specs, content, and minor features
- Participate in code review for UI/UX changes

### Example organisation structure (15-20 people)

```
Engineering Leadership (1)
├── Software Engineers (8)
│   ├── Backend Focus (3)
│   ├── Frontend Focus (2)
│   └── Fullstack (3)
├── Security Engineers (3)
│   ├── Application Security (2)
│   └── AI Security (1)
├── AI Platform Engineers (2)
│   ├── Agent Infrastructure (1)
│   └── Prompt Engineering & Observability (1)
├── Product Manager (1)
│   └── Primitively fluent, submits PRs
├── Designer (1)
│   └── Ships code via Cursor, participates in review
└── DevOps/SRE (1)
    └── CI/CD, infrastructure-as-code, observability
```

---

## Delegation policies

### Risk-based delegation framework

**Green Zone** (high delegation, light supervision):
- Exploratory prototypes for internal use
- Documentation generation (README, API docs)
- Test case generation
- Boilerplate code and repetitive patterns
- Refactoring (when covered by comprehensive tests)
- Debugging assistance and root cause analysis

**Amber Zone** (moderate delegation, active supervision):
- Feature implementation in well-understood domains
- Database schema changes (with DBA review)
- API design and implementation (with architectural review)
- Performance optimisation (with benchmarking)
- UI implementation (with design review)
- Non-critical infrastructure-as-code

**Red Zone** (minimal delegation, intense supervision):
- Authentication and authorisation logic
- Cryptographic implementations
- Payment processing
- PII handling
- Security-critical code (input validation, access control)
- Compliance-related features (GDPR, SOC2)
- Core platform services
- Disaster recovery systems

**Human-Only** (no delegation):
- Final architectural decisions with long-term implications
- Selection of core technologies and dependencies
- Security incident response decisions
- Privacy and ethics determinations
- Trade-offs involving compliance or legal risk
- Decisions affecting customer trust or reputation

---

## Tooling stack

### Recommended stack

**Code and repository management:**
- Git as canonical system of record for all artifacts
- GitHub for PR workflows, code review, CI/CD integration
- Trunk-based development with short-lived feature branches

**IDE-centric agent tools** (for rapid iteration):
- Cursor or similar AI IDE
- Use cases: feature development, debugging, refactoring, UI design

**Terminal-centric agent tools** (for long-running work):
- Terminal-based agentic assistants for batch processing, migrations, CI/CD integration
- Custom harnesses for multi-session projects

**CI/CD, tests, and policy checks:**
- GitHub Actions for automated testing, linting, security scans
- Policy-as-code (OPA) for automated policy enforcement
- Secret scanning (GitGuardian, TruffleHog)
- SAST/DAST integrated into pipelines

**Agent harnesses and orchestration:**
- Custom session workflow scripts (`dev-setup.sh`, `memory.md`, `progress.txt`)
- MCP servers for extensible tool access
- Docker Dev Containers for isolated agent execution

**Observability:**
- Datadog/New Relic for production monitoring
- Agent-specific logging (sessions, token usage, success rates)
- Git as audit trail for all changes

**Security and compliance:**
- HashiCorp Vault for secrets management
- Vanta/Drata for compliance automation
- Snyk/Dependabot for dependency scanning

**Documentation:**
- Markdown repos for all design docs, runbooks, policies
- `memory.md` files documenting conventions for agent consumption
- llms.txt directories for agent-accessible knowledge

---

## Implementation roadmap

### Phase 1: Foundation

**Month 1: Infrastructure and tooling**
- Set up core tooling stack (Git, CI/CD, agent tools)
- Establish repository structure with `memory.md` and agent convention files
- Define initial delegation policies and security guardrails
- Document target workflows and success metrics

**Month 2: First hires and onboarding**
- Onboard first hires with IDE-based and terminal-based agentic tools
- Establish primitive fluency training as part of onboarding
- Build first agent harnesses for common workflows
- Begin initial product development using AI-first practices

**Month 3: Expand practices across team**
- Ensure all team members (including non-engineers) understand Git and PR workflows
- Run first "fuzz session" to establish the ritual
- Refine workflows based on early learnings
- Document what's working and what needs adjustment

**Success criteria:**
- All team members using AI tools daily
- No security incidents from AI-generated code
- Team feedback confirms workflows are effective
- Clear documentation of established practices

### Phase 2: Scaling

**Month 4: Deepen AI-first practices**
- Evaluate any new tools against abstraction tax framework
- Ensure all workflows remain artifact-centric
- Build more sophisticated agent harnesses for complex projects

**Month 5: Mature policy-as-code**
- Expand security policies in code
- Automate comprehensive policy checks in CI/CD
- Establish security review processes for agent-generated code

**Month 6: Optimise and document**
- Refine agent harnesses based on usage patterns
- Monitor agent performance (success rate, token cost, review time)
- Document mature practices for future team members

**Success criteria:**
- All engineers using AI daily as default workflow
- Harness patterns successfully enabling complex projects
- Zero critical security incidents
- Clear onboarding documentation for new hires

### Phase 3: Maturity

**Months 7-9: Scale with growth**
- Maintain primitive fluency as team grows
- Standardise workflows (design doc → agent impl → PR → deploy)
- Ensure all new hires adopt AI-first practices from day one

**Months 10-12: Advanced capabilities and governance**
- Implement comprehensive agent oversight frameworks
- Integrate AI-specific security checks across all workflows
- Generate compliance evidence automatically
- Conduct retrospective and refine approach

**Success criteria:**
- All content and docs managed via PR workflow
- Compliance evidence generation fully automated
- All team members (including non-engineers) regularly submitting PRs
- AI-first culture firmly established as "how we work"

---

## Measuring success

### Key performance indicators

| Category | Metric | Target |
|----------|--------|--------|
| **Productivity** | Merged PRs per engineer per day | Industry-leading (benchmark against Anthropic's 67% improvement data) |
| **Productivity** | Cycle time (idea → production) | Hours to days, not weeks |
| **Productivity** | "Net new" work enabled by AI | 25%+ of total work |
| **Quality** | Bug escape rate to production | Below industry average |
| **Quality** | Security vulnerability density | Zero critical, minimal others |
| **Adoption** | % engineers using AI daily | 80%+ |
| **Adoption** | % work AI-assisted | 60%+ |
| **Skill Health** | Performance on fundamental assessments | Track and maintain over time |
| **Skill Health** | Mentorship activity levels | Active and documented |
| **Culture** | Employee satisfaction scores | High (establish baseline early) |
| **Culture** | Retention rates | Above industry average |
| **Safety** | AI-related incidents per quarter | Zero critical |
| **Safety** | Policy violation frequency | Near zero |
| **Compliance** | Time to generate audit reports | Fully automated |

---

## Risk mitigation

### Phase 1 risks

| Risk | Mitigation |
|------|------------|
| Early hires not adapting to AI-first approach | Screen for AI-first mindset in hiring; provide comprehensive onboarding |
| Security incident early on | Start with strong guardrails; comprehensive logging from day one |
| Over-engineering before product-market fit | Keep tooling simple initially; add complexity only when needed |

### Phase 2 risks

| Risk | Mitigation |
|------|------------|
| Skill atrophy as team scales | Implement deliberate practice programmes early; monitor assessments |
| New hires diluting AI-first culture | Strong onboarding; clear documentation of "how we work here" |
| Governance bottlenecks slowing velocity | Streamline approval workflows; delegate to teams; escalate only for high-risk |

### Phase 3 risks

| Risk | Mitigation |
|------|------------|
| Over-reliance on AI | Maintain "no-AI" capabilities through regular practice |
| Complacency about security | Red-team agent systems; regular security reviews; external audits |
| Rapid growth outpacing culture | Document practices thoroughly; hire for cultural fit; maintain rituals |

---

## Conclusion

This blueprint represents my framework for building an AI-first engineering organisation from day one. Based on my research, I'm convinced the opportunity is significant: sustained 50%+ productivity improvements, expanded engineering capabilities, and competitive advantage through superior execution speed. All baked into the foundation rather than retrofitted later.

I believe this approach should guide how organisations build. We're not merely selecting tools. We're establishing how work is structured, what skills we value, and what engineering means in this new era.

Organisations operating at the intersection of DevSecOps and AI security have advantages that most lack. They understand security deeply. They can encode guardrails as primitives, not afterthoughts. They can dogfood their own AI security practices whilst building products that help others do the same.

The companies that build AI-first from the start will thrive. Those that try to retrofit these practices later will struggle with legacy processes and cultural resistance.

I believe this is the way to build. Not just as internal practice, but as an example for others navigating similar challenges. This is the opportunity to get it right from the beginning.

---

*This document synthesises research from Anthropic's internal transformation study (132 engineers, 53 interviews, 200,000 agent transcripts), Cursor's engineering practices, and my analysis of how these patterns apply to organisations building at the intersection of AI and security.*
