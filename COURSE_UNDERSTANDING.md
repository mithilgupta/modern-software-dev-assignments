# Course Understanding: CS146S — The Modern Software Developer

A plain-language overview of what this course is, what it covers, and how the
assignments in this repo fit in. Written for self-paced study (not enrolled).

- **Course site:** https://themodernsoftware.dev/ (Fall 2026; the older Fall 2025 version is at `/fall2025`)
- **School:** Stanford University, Fall 2026, 3 units
- **Instructor:** Mihail Eric · **TAs:** Isaac Kan, Vijay Daita
- **Upstream repo:** https://github.com/mihail911/modern-software-dev-assignments
- **My fork:** https://github.com/mithilgupta/modern-software-dev-assignments

---

## The one-sentence version

Software development is shifting from *writing code by hand* to *directing AI
coding agents* (like Claude Code), and this course teaches how to do that well:
how agents work inside, how to give them the right context and tools, and how to
build reliable workflows around them.

## The big idea

The course treats a coding agent as a system you can understand and engineer,
not a magic box. The arc goes:

1. **Understand the agent**: what's inside it (weeks 1–2)
2. **Extend the agent**: give it new tools and skills (weeks 2–3)
3. **Customize the agent and your repo**: so it works well on your code (weeks 4–5)
4. **Use agents for team work**: code review, security, background tasks (weeks 6–8)
5. **Scale it up**: AI-native teams and "software factories" (weeks 9–10)

## Weekly syllabus (Fall 2026)

| Week | Topic | What it covers | Guest |
|---|---|---|---|
| 1 | **The Internals of Coding Agents** | What an LLM is; the "agent loop"; the core tools (read, write, edit, bash); how real agents structure system prompts and tool definitions. Lecture builds a mini Claude Code in ~200 lines. | — |
| 2 | **Advanced Context Engineering** | Advanced prompting; **RePPIT** (Research, Propose, Plan, Implement, Test); spec-driven development; **MCP** fundamentals; designing tools agents can use well; when to compact context. | — |
| 3 | **Agent Skills and CLI** | What skills are (`SKILL.md` + scripts that encode a workflow); web skills; working effectively from the command line. | Lee Robinson |
| 4 | **Customizing Your Agent and Repository** | `CLAUDE.md` / `AGENTS.md` (what goes where); **hooks** for lint, tests, and guardrails; subagent patterns (planner / implementer / reviewer). | Boris Cherny (creator of Claude Code) |
| 5 | **Agent-Ready Codebases** | What makes a repo easy for agents: structure, docs, tests, checks; auditing readiness; common gaps. | Eno Reyes (Factory) |
| 6 | **Agentic Code Review** | What AI review catches and misses; review architectures and custom rules; fitting AI review into PR workflows. | Silas Alberti (Cognition) |
| 7 | **Security** *(title not shown on site)* | SAST/SCA scanning, dependency and leaked-secret vulnerabilities; **prompt injection** and agent-specific attacks; agent-assisted triage and fixes. | Isaac Evans (Semgrep) |
| 8 | **Background Agents** | Agents that run asynchronously in the cloud; managing many agents in parallel; issue-to-PR pipelines triggered from Slack, Linear, GitHub. | Rajesh Bhatia (Cloudflare) |
| 9 | **Building an AI-Native Team** | MCP portals (central, permissioned tool access); LLM gateways, model routing, cost optimization; org-wide adoption. | Elad Gil, Amjad Masad (Replit) |
| 10 | **The Software Factory + The Future** | Self-running, self-improving software systems; running and securing agents after deployment; where the field is heading. | — |

Plus a **final project** showcasing these practices.

## Assignments in this repo (so far)

Each week folder has `assignment.md` (the task) and `writeup.md` (a template
with `TODO`s to fill in).

| Week | Assignment | What you actually do | Main skill practiced |
|---|---|---|---|
| 1 | **Trace Dissection of a Real Claude Code Session** | Put a proxy (mitmproxy) between Claude Code and Anthropic's API, record a real coding session, then analyze the hidden system prompt, tool list, error recovery, planning, and context management. | Understanding how an agent works inside |
| 2 | **Build an MCP Server for a Third-Party API** | Build an MCP server (with FastMCP) that wraps an OAuth-based API (GitHub, Google, Notion, Spotify…). At least 3 tools that chain together, one write tool, real OAuth with token refresh. Graded mostly on *agent ergonomics*: can the model use your tools correctly? | Designing tools for agents |
| 3 | **Author a Skill** | Pick a repeatable workflow (PR review, bug reproduction, test writing…), write a `SKILL.md` for it, and test whether it triggers when it should (and doesn't when it shouldn't) on a real open-source repo. | Encoding workflows for agents |

More weeks will appear upstream over time; pull them with `git pull upstream master`.

## Glossary (useful words when talking to Claude)

- **LLM**: Large Language Model; the AI model (e.g. Claude) that generates text.
- **Coding agent**: an LLM wrapped in a loop that can use tools (read files, run commands, edit code) to complete tasks. Claude Code is one.
- **Agent loop**: the cycle of *model thinks → calls a tool → sees the result → thinks again*, until the task is done.
- **System prompt**: hidden instructions sent to the model on every request that shape its behavior.
- **Tool / tool schema**: a capability the agent can call, described by a name, a description, and a JSON schema of its parameters. The model only "sees" the tool through this description.
- **Context / context window**: everything the model can see at once (system prompt, tools, conversation). It's limited, so what goes in matters.
- **Context engineering**: deliberately choosing what information the agent sees, and when.
- **Compaction**: summarizing older conversation to free up context space.
- **MCP (Model Context Protocol)**: an open standard for plugging external tools and data (APIs, databases, services) into any agent. An *MCP server* exposes tools; the agent is the *client*.
- **Skill**: a folder with a `SKILL.md` that teaches an agent a reusable procedure; it loads only when relevant.
- **`CLAUDE.md` / `AGENTS.md`**: files in a repo that give an agent standing instructions about that project.
- **Hooks**: scripts that run automatically at certain points (e.g. before a tool call, after an edit) to enforce rules like "always run the linter."
- **Subagent**: a separate agent the main agent spins up to handle a sub-task with its own fresh context.
- **Spec-driven development**: writing a clear specification first, then having the agent implement against it.
- **RePPIT**: Research → Propose → Plan → Implement → Test; the course's structured workflow for agent tasks.
- **Background agent**: an agent that works asynchronously (e.g. in the cloud) while you do other things, often turning an issue into a pull request.
- **Prompt injection**: an attack where malicious text (in a file, web page, or API response) tricks an agent into doing something unintended.
- **SAST / SCA**: Static Application Security Testing (scanning your code) / Software Composition Analysis (scanning your dependencies).
- **LLM gateway / model routing**: a central layer that sends requests to different models based on cost, speed, or task.
- **Software factory**: the end-state vision; software systems that largely build, test, and improve themselves with agents.
- **OAuth**: the standard "Log in with Google/GitHub" authorization flow; issues tokens that expire and must be refreshed.

## Practical notes

- **Time:** the course expects ~10–12 hours/week.
- **Languages:** language-agnostic; examples mostly Python and JavaScript.
- **Prereqs:** solid programming fundamentals (Stanford CS111/CS161 level). No prior AI-tool experience needed.
- **Tools needed:** Claude Code (or a similar agent like Cursor), plus per-week tools (e.g. mitmproxy for week 1, FastMCP for week 2).
- **Self-paced:** as a non-enrolled learner, skip the Gradescope / add-collaborators submission steps. The `writeup.md` files are still a good record of what you learned.

## Local setup (already done)

```bash
cd ~/workspace/modern-software-dev-assignments
conda activate cs146s        # Python 3.12 env with the course packages
git pull upstream master     # get new weeks from the teacher
git push                     # save your work to your fork
```
