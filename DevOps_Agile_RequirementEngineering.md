# DevOps, Agile Practices, and Requirement Engineering

**Name:** Jatin Wadhwani | **Roll No:** 64 | **Class:** D12A

---

## 1. What Is DevOps?

DevOps is a set of practices and a supporting culture that closes the gap between the people who
write software and the people who run it in production. Historically, development and operations
functioned as two separate teams with separate goals — developers were measured on how much
new functionality they shipped, while operations was measured on how stable the systems stayed.
That mismatch in incentives is exactly what caused friction: developers wanted to push change,
operations wanted to avoid it. DevOps addresses this by putting both responsibilities on the same
team, so the group that builds a feature is also on the hook for keeping it running.

Once security responsibilities are folded into this same shared ownership, the practice is usually
called **DevSecOps** — security checks (dependency scanning, static analysis, secret detection) get
built directly into the pipeline instead of being bolted on right before release.

DevOps rests on a handful of practices that, together, make frequent and safe releases possible:

- **Continuous Integration (CI):** every code change is merged into a shared branch frequently and
  verified automatically (build + test), so integration problems surface within minutes, not weeks.
- **Continuous Delivery / Deployment (CD):** a change that passes CI is automatically packaged and
  is either one click away from production (delivery) or pushed straight to production (deployment).
- **Infrastructure as Code (IaC):** environments (servers, networks, permissions) are described in
  version-controlled config files rather than clicked together by hand, so they can be recreated
  identically and reviewed like code.
- **Containerization and orchestration:** packaging an application with its dependencies (e.g.
  Docker) and letting a scheduler (e.g. Kubernetes) handle where and how it runs.
- **Observability:** logging, metrics, and tracing that let a team see what's actually happening in a
  running system, rather than guessing after something breaks.

Organizations invest in DevOps for the same reason they invest in automation anywhere else: it
converts a slow, error-prone, manual process (releasing software) into a fast, repeatable, low-risk
one — which matters more every year as software becomes the product itself rather than just
something that supports the product.

---

## 2. Agile vs DevOps: A Comparison

Agile and DevOps get lumped together often, but they're solving different halves of the same
problem — Agile is about deciding *what* to build, DevOps is about *shipping* it reliably.

| Aspect | Agile | DevOps |
|---|---|---|
| Primary focus | Adapting quickly to changing requirements | Automating build, test, and release |
| Scope | Mostly the development/product team | Dev, ops, QA, and often security together |
| Unit of work | Sprints (typically 2 weeks) | Continuous stream of small releases |
| Central question | Are we building the right thing? | Can we ship this safely, over and over? |
| Key artifacts | Backlog, user stories, sprint board | CI/CD pipeline, IaC scripts, dashboards |
| Feedback source | Stakeholders/users each sprint review | Production monitoring after every deploy |

The two are complementary, not competing. A team can run picture-perfect two-week sprints and
still ship badly if every release is a manual, risky, all-hands event — that's Agile without DevOps.
Equally, a team can have a beautifully automated pipeline pushing out the wrong features because
nobody is validating requirements with users — that's DevOps without Agile. The strongest setups
pair Agile's short feedback loop on *what to build* with DevOps' automation of *how it gets shipped*.

---

## 3. Case Study: Trello and Linear in Real Projects

Project-management tools tend to specialize toward either lightweight simplicity or engineering
depth, and Trello and Linear sit at opposite ends of that spectrum.

**Trello** is built around the Kanban board metaphor — cards on lists, dragged from column to
column. Its strength is how little friction it has: almost anyone on a team, technical or not, can
understand a Trello board within a minute of looking at it. It's commonly adopted by small teams,
student groups, and cross-functional projects where the priority is visibility over process rigor.
The tradeoff is that Trello doesn't have much opinion on *how* software should be built — there's
no built-in sprint velocity tracking, no native concept of a release, and scaling it to a large
engineering org usually means bolting on a pile of Power-Ups (Trello's plugin system) to
approximate what dedicated dev tools give you out of the box.

**Linear** was built specifically for software teams and is opinionated about it. It has fast keyboard-
driven workflows, native cycles (Linear's version of sprints), automatic linking between issues and
Git branches/PRs, and built-in roadmaps and triage flows. Because it's purpose-built for engineering
work, it tends to feel much faster and more structured for developers day-to-day, but that same
specialization makes it a less natural fit for non-technical stakeholders (marketing, sales) who just
want a simple view of what's happening.

**How teams actually combine the two:** a common pattern is for the engineering team to live in
Linear for day-to-day ticket work — bugs, technical tasks, cycles — while a lighter Trello board (or
a shared view) is kept for cross-functional stakeholders who need visibility without needing to
understand engineering-specific concepts like cycles or triage queues.

**Practical takeaway:** the right tool follows the audience — Linear (or JIRA) for structured,
engineering-heavy workflows with tight Git integration; Trello (or Asana) for lightweight,
cross-functional visibility where ease of adoption matters more than process depth.

---

## 4. Writing Effective User Stories and Acceptance Criteria

A **user story** captures a requirement from the perspective of the person who benefits from it,
in plain language rather than technical spec-speak. The standard template is:

> As a **[type of user]**, I want **[an action/goal]**, so that **[benefit/reason]**.

**Example:**
> As a security analyst, I want to receive an alert when a login occurs from a new device, so that I
> can quickly investigate potentially compromised accounts.

Good user stories are commonly checked against the **INVEST** criteria:

- **Independent** — doesn't require another story to be finished first
- **Negotiable** — a starting point for discussion, not a locked-in contract
- **Valuable** — delivers something a user or the business actually cares about
- **Estimable** — the team can reasonably size the effort
- **Small** — fits comfortably within a single sprint
- **Testable** — has a clear, checkable definition of done

**Acceptance criteria** turn that story into specific, checkable conditions. The most common format
is **Given–When–Then**:

> Given **[a starting context]**, When **[an action happens]**, Then **[an expected outcome occurs]**.

Continuing the example above:

- Given a user has 2FA enabled and logs in from a device not seen in the last 90 days, When the
  login succeeds, Then an email alert is sent to the account owner within 60 seconds.
- Given a user logs in from a previously recognized device, When the login succeeds, Then no
  new-device alert is triggered.

Well-written acceptance criteria are agreed on *before* development starts, so that developers,
testers, and whoever requested the feature are all working against the same definition of "done" —
and they should cover not just the happy path but realistic edge cases and failure conditions too.

---

## 5. Advanced Requirement Elicitation Techniques

Requirement elicitation is the process of figuring out what stakeholders actually need — which is
harder than it sounds, since people are often better at describing symptoms of a problem than the
underlying requirement, and different stakeholders frequently want contradictory things.

**Surveys and questionnaires** are useful when requirements need to be gathered from a large or
geographically spread group of stakeholders where one-on-one interviews aren't practical. They
scale well and produce data that's easy to aggregate, but the quality of what comes back depends
entirely on how well the questions were designed — a poorly worded question produces
unreliable answers at scale, which is worse than a small sample of good interviews.

**Prototyping** involves building a rough, often non-functional mockup of a system and putting it in
front of stakeholders to react to. This works especially well when stakeholders struggle to
articulate requirements in the abstract but can immediately tell you what's wrong when they see
something concrete — "that's not quite it, but if it did X instead" is far easier to extract from a
prototype walkthrough than from a blank-page interview.

Other techniques used alongside these include structured/unstructured **interviews**,
**ethnography** (observing stakeholders in their actual working environment rather than relying on
self-reported descriptions of their work), **brainstorming and focus groups**, and **JAD (Joint
Application Design) workshops** that bring multiple stakeholders together to hash out
requirements collaboratively in a single session. In practice, analysts rarely rely on just one
technique — a common pattern is a prototype to get concrete reactions, followed by targeted
interviews to clarify the details the prototype exposed. Which combination makes sense depends
on project size, how well stakeholders already understand their own needs, and how much time is
available.

---

## 6. Requirement Traceability Matrix (RTM)

A **Requirement Traceability Matrix** is a table — often a spreadsheet, or a view generated by a
requirement-management tool — that maps every requirement to the artifacts that implement and
verify it: design documents, code components, and test cases. Its purpose is to prove **coverage**:
that every requirement was actually built and tested, and that no test case or design element
exists without a requirement behind it. This two-directional check (requirement → implementation
→ test, and test → back to requirement) is called **bidirectional traceability**.

A typical RTM includes:

- Requirement ID and short description
- Source (which stakeholder, document, or meeting the requirement came from)
- Priority and current status
- Linked design/spec element(s)
- Linked test case(s) and their pass/fail results
- Linked defects, if any were raised against it

**Why it matters in practice:**

- It exposes **gaps** immediately — a requirement with no linked test case is a red flag, and so is a
  test case that traces back to nothing.
- It supports **impact analysis** — when a requirement changes mid-project, the RTM shows every
  design element, code module, and test that needs to be revisited.
- It provides **audit evidence** for regulated domains (aerospace, medical devices, automotive)
  where a regulator may literally ask "show me the test that proves requirement #214 was met."
- It gives non-technical stakeholders a real-time view of how much of the requirement set is
  actually done versus still in progress.

An RTM is only useful if it's kept current — one that isn't updated as requirements evolve quickly
becomes misleading rather than helpful.

---

## 7. Tools for Requirement Management

Once a project outgrows tracking requirements in a shared document, dedicated requirement-
management tools take over. These typically provide structured requirement authoring, version
history, built-in traceability links (an RTM baked into the tool itself), and change-impact analysis
across a distributed team.

**Jama Connect** is one of the more widely adopted tools in this space outside of the traditional
aerospace/defense-only tools. It's built around "living" requirements that stay linked to design,
risk, and test artifacts throughout the project, with review workflows that let stakeholders
formally sign off on requirement changes. It's used heavily in regulated hardware/software
industries (medical devices, automotive, industrial systems) where proving compliance is not
optional.

**IBM Engineering Requirements Management DOORS (and DOORS Next)** is the longest-established
tool in this category, known for its rigor: hierarchical requirement structuring, full bidirectional
linking, and a complete audit history of every change. It's the default choice on large, long-lived,
safety-critical government and defense programs specifically because that audit trail is often a
contractual requirement, not just a nice-to-have.

Other tools in this space include **Polarion**, **Helix ALM**, and **Visure Requirements** for
heavier, compliance-driven projects, while agile teams on smaller or less-regulated projects often
manage requirements well enough inside their existing tracker (JIRA epics/stories, or even Linear)
paired with a simple RTM spreadsheet — the heavyweight tools earn their complexity only once
the regulatory or scale pressure justifies it.

---

## 8. Conclusion

Agile and DevOps solve two different problems that both matter: Agile keeps a team honest about
building the *right* thing by looping in stakeholder feedback every sprint, while DevOps makes sure
that thing can actually be *shipped* — quickly, safely, and repeatedly. Tools like Trello and Linear
show how this plays out in practice: lightweight tools win where broad, cross-functional visibility
matters most, while purpose-built engineering tools win where speed and process depth matter
most for the people actually writing the code — and many real teams end up running both side by
side. None of this works, though, without solid requirement engineering underneath it: user
stories with clear, testable acceptance criteria; elicitation techniques (surveys, prototyping,
interviews, ethnography) chosen to match the project instead of applied by default; a traceability
matrix that proves every requirement was actually built and tested; and, for larger or regulated
projects, a dedicated tool like Jama Connect or IBM DOORS to manage all of it formally. Together
these practices are what let a software project move from a vague idea to something reliably
built, tested, and shipped.

---

## References

1. Amazon Web Services — *What is DevOps?* (aws.amazon.com/devops/what-is-devops)
2. Atlassian — *What is DevOps?* (atlassian.com/devops)
3. Linear — *Linear Method* (linear.app/method)
4. Trello — *Trello Guide* (trello.com/guide)
5. TestRail — *Requirements Traceability Matrix: A How-To Guide* (testrail.com/blog/requirements-traceability-matrix)
6. Jama Software — *What is Requirements Traceability?* (jamasoftware.com/requirements-traceability)
7. IBM — *Engineering Requirements Management DOORS* (product documentation)
8. Scaled Agile Framework (SAFe) — *INVEST in Good User Stories* (scaledagileframework.com)
