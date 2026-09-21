# Developer

## Role Summary

Developers design, build, test, and maintain software that delivers value to customers and the business. Their primary responsibility is turning ideas into reliable, maintainable applications while balancing speed, quality, and security. Developers spend as much time (or more) navigating development tools, infrastructure, and collaboration as they do writing code. They rely on consistent environments, fast feedback loops, and access to the right tools to stay productive. The less time they spend configuring environments or troubleshooting infrastructure, the more time they can spend solving customer problems and shipping software.

## Related Titles

- Software Engineer
- Backend Engineer
- Full-Stack Engineer
- Application Developer
- Senior Software Engineer
- Staff Software Engineer
- Principal Software Engineer

Although some organizations distinguish between *Developers* and *Software Engineers*, the distinction is often inconsistent across the industry. Both roles share similar responsibilities, workflows, tooling, and day-to-day challenges, so this summary treats them as a single audience while recognizing that specific job expectations may vary by organization.

## Primary Goals

- Deliver high-quality software that solves customer and business problems while meeting performance, security, and reliability expectations.
- Move from idea to production as efficiently as possible by minimizing time spent on environment setup, infrastructure requests, and manual processes.
- Maintain development velocity while balancing new feature work, bug fixes, technical debt, and operational responsibilities.
- Write maintainable code that other developers can understand, extend, and operate over time.
- Continuously improve technical skills and adopt tools that increase productivity without sacrificing quality.

## Core Responsibilities

Developers typically split their time across several activities rather than writing code continuously.

- Design, implement, and maintain application features and services.
- Debug defects identified during development, testing, or production.
- Review pull requests and provide constructive technical feedback.
- Write automated tests to improve software quality and reliability.
- Integrate applications with APIs, databases, cloud services, and internal platforms.
- Refactor existing code to improve maintainability and performance.
- Participate in architecture discussions, sprint planning, and technical design reviews.
- Collaborate with product managers, designers, QA engineers, and platform teams.
- Use AI coding assistants to accelerate implementation, documentation, testing, and debugging where appropriate.

## Daily Workflow

A typical day is a mix of focused development work and collaboration. Developers regularly move between writing code, reviewing pull requests, debugging issues, running tests, attending standups, responding to Slack messages, and working through design discussions.

Throughout the day they interact with source control systems, cloud infrastructure, CI/CD pipelines, databases, APIs, and increasingly AI coding assistants. They frequently switch contexts between multiple repositories, environments, and projects.

Long waits for builds, environment provisioning, dependency installation, or infrastructure access interrupt flow and reduce productivity. The best development experience minimizes these interruptions so developers can stay focused on solving technical problems.

## Success Metrics

Developers are typically evaluated by the quality, reliability, and impact of the software they deliver rather than raw output. Common success metrics include:

- Delivering planned work on time while maintaining high engineering standards.
- Reducing production defects through testing, code reviews, and thoughtful design.
- Writing maintainable code that other engineers can understand and extend.
- Improving application performance, scalability, and reliability.
- Contributing positively during code reviews and technical discussions.
- Helping teammates solve technical problems and sharing knowledge across the team.
- Successfully balancing feature delivery with long-term technical health.

## What Matters Most

### Fast feedback loops

Developers want immediate feedback while writing software. Quickly compiling code, running tests, rebuilding environments, or validating AI-generated code helps maintain momentum and encourages experimentation. Every minute spent waiting breaks concentration and slows delivery.

### Reliable development environments

Developers need environments that behave consistently across their laptop, teammates' machines, CI pipelines, and production. Consistent environments reduce time spent debugging configuration issues and increase confidence that software will behave as expected after deployment.

### Freedom to use familiar tools

Developers are most productive when they can use their preferred IDE, terminal, extensions, keyboard shortcuts, and AI coding assistants. While organizations often standardize infrastructure, developers still expect flexibility in how they interact with it.

### Self-service infrastructure

Waiting for another team to provision an environment or grant permissions interrupts development. Developers value platforms that allow them to create, rebuild, or modify environments independently while remaining within organizational guardrails.

### Minimal operational friction

Authentication, networking, secrets management, and infrastructure should work predictably without requiring constant attention. The development platform should simplify engineering work rather than becoming another system developers have to manage.

## Biggest Challenges

### Environment setup and onboarding

Joining a new project often requires configuring dependencies, requesting access, installing tools, and troubleshooting setup issues before meaningful work can begin. Even experienced developers can lose hours or days getting productive.

### Environment drift

Differences between developer machines, CI pipelines, and production environments make bugs difficult to reproduce and consume valuable engineering time.

### Context switching

Developers regularly move between feature work, production issues, meetings, code reviews, and support requests. Frequent interruptions make it difficult to maintain focus and complete complex technical work efficiently.

### Infrastructure bottlenecks

Provisioning environments, requesting permissions, or waiting for shared infrastructure slows development even when application work is otherwise straightforward.

### Growing tooling complexity

Modern development requires familiarity with containers, Kubernetes, cloud services, CI/CD systems, infrastructure as code, observability platforms, security tooling, and AI assistants. Keeping up with this expanding ecosystem while continuing to deliver software is increasingly challenging.

## Common Frustrations

- Spending hours debugging environment issues that are unrelated to application code.
- Repeating manual setup every time they join a new project or rebuild a machine.
- Waiting for infrastructure changes or permissions before continuing development.
- Working on underpowered hardware that struggles with large repositories, containers, or AI-assisted workflows.
- Discovering that documentation is outdated or incomplete.
- Being forced into restrictive workflows that limit tool choice or reduce productivity.
- Losing work because development environments are difficult to rebuild or reproduce.

## Tools They Use

### Development

- Visual Studio IDEs/forks (e.g. Cursor)
- JetBrains IDEs
- Vim / Neovim
- Terminal applications
- Git

### AI Coding

- Cursor
- Claude Code
- OpenAI Codex
- GitHub Copilot
- Devin
- Every other coding agent that released this week…

### Source Control

- GitHub
- GitLab
- Bitbucket

### Build/Package Management

- npm
- pnpm
- Yarn
- Maven
- Gradle
- pip
- Cargo
- Go modules

### Infrastructure

- Docker
- Kubernetes
- Terraform
- AWS
- Azure
- Google Cloud

### Collaboration

- Slack
- Jira
- GitHub
- GitLab
- Notion
- Confluence
- Linear

## Collaboration

Developers rarely work in isolation. They collaborate daily with product managers to clarify requirements, designers to implement user experiences, QA engineers to validate functionality, and platform engineers to improve development workflows. They also work closely with security teams, site reliability engineers, and other developers through architecture reviews, code reviews, pair programming, and incident response. Strong communication skills are increasingly important as engineering organizations become larger and more distributed.

## What They Need from Platform Engineering

Developers want platform teams to provide infrastructure that accelerates software delivery without requiring developers to become infrastructure experts. They value:

- Standardized development environments that eliminate repetitive setup while still allowing reasonable customization.
- Self-service provisioning that removes manual approval processes for routine development work.
- Secure access to repositories, internal services, secrets, and cloud resources without unnecessary friction.
- Fast, reliable workspace provisioning that minimizes waiting between idea and implementation.
- Infrastructure that scales with developer needs instead of laptop limitations.

When platform engineering succeeds, developers spend more time building software and less time thinking about infrastructure.

## How Coder Helps

Coder provides developers with consistent, self-service development environments that run on infrastructure managed by their organization. For developers, this means:

- Starting new projects without lengthy local setup.
- Rebuilding environments in minutes instead of hours.
- Working from browser-based or desktop IDEs using familiar workflows.
- Accessing internal repositories, services, and cloud resources securely.
- Running workloads on infrastructure sized appropriately for the project instead of being constrained by laptop hardware.
- Sharing reproducible environments with teammates to simplify debugging, onboarding, and collaboration.
- Working alongside AI coding assistants and coding agents while keeping development infrastructure under organizational control.

Rather than changing how developers build software, Coder standardizes the underlying environment so they can focus on writing code instead of maintaining development machines.

## Buying Influence

Developers are rarely the economic buyer for developer infrastructure, but they have significant influence over evaluation and adoption. They often:

- Evaluate new tools during proof-of-concept projects.
- Recommend platforms to engineering leadership.
- Influence purchasing decisions through technical feedback.
- Drive bottom-up adoption when a tool demonstrably improves everyday workflows.
- Resist platforms that increase friction or reduce flexibility, even when mandated by leadership.

Successful platforms earn developer trust by solving real workflow problems rather than requiring developers to fundamentally change how they work.

## Common Questions

When evaluating a platform like Coder, developers often ask:

- Will this be faster than my current setup?
- Can I continue using my preferred IDE and development tools?
- How quickly can I create or rebuild a development environment?
- Can I customize my workspace while remaining within company standards?
- How does this integrate with Git, containers, Kubernetes, and cloud infrastructure?
- Can I use AI coding assistants and coding agents?
- What happens if my workspace stops or needs to be rebuilt?
- How does debugging work when development happens remotely?
- Can I share my environment with teammates to reproduce issues?
- Is this a true development environment or simply another form of VDI?

## Content They Trust

Developers tend to ignore high-level marketing content in favor of practical technical resources that demonstrate how a tool works. They are most influenced by:

- Product documentation with working examples.
- GitHub repositories and reference implementations.
- Technical blog posts that explain implementation details.
- API documentation.
- Architecture diagrams.
- Demo videos that show real workflows.
- Community discussions on GitHub, YouTube, Reddit, Hacker News, and Stack Overflow.
- Conference talks from practicing engineers.
- Recommendations from trusted peers and open source communities.

Developers are more likely to trust code, peer reviews, documentation, and hands-on experience than polished marketing claims. Demonstrating how a platform improves everyday workflows is far more persuasive than simply claiming increased productivity.
