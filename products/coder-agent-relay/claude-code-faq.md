# Agent Relay for Claude FAQ

## Understanding the Integration

**Who is Anthropic and what is Claude Code?**
Anthropic is an AI safety and research company that builds Claude. Claude Code is Anthropic's agentic coding product. You can start Claude Code cloud sessions from supported Anthropic surfaces and route them to Anthropic-hosted compute or a customer-operated, self-hosted environment like Coder workspaces.

**Who is Coder?**
Coder is the self-hosted, cloud-agnostic infrastructure layer that governs how AI development runs inside the enterprise. It standardizes development environments, gives platform and security teams centralized control over AI model access and usage, and lets both human developers and autonomous agents work in the same governed environment, on infrastructure the customer already owns.

**How would you summarize the architecture in one sentence?**
Anthropic orchestrates and performs inference, Coder provides the self-hosted execution environment, and Agent Relay connects the two.

**Why are Anthropic and Coder integrating?**
Anthropic enables organizations to route Claude Code cloud sessions to self-hosted environments that customers create and operate on their own infrastructure. Coder provides the development-environment control plane and workspace lifecycle to provision those environments on demand. Together, this integration lets developers retain the Claude Code cloud experience while session execution occurs inside ephemeral Coder workspaces in the customer's network.

**What customer problem does this solve?**
Cloud-hosted coding agents need access to source code, dependencies, internal services, development tooling, and other enterprise resources to do useful work. Many organizations cannot provide that access inside vendor-managed execution environments. Coder gives Claude Code agents self-hosted development environments inside the customer's infrastructure while preserving the Claude Code cloud agent experience developers already use.

**Who is this solution designed for?**
The integration is designed for organizations that want to adopt cloud-hosted AI coding agents while retaining control over the infrastructure where those agents execute. This is particularly relevant to financial services, government, defense, healthcare, critical infrastructure, and large enterprises with strict security, compliance, or data sovereignty requirements.

## The Integration

**What does the integration provide?**
Claude Code provides the cloud agent experience, orchestration, and inference developers already use, while Coder provides self-hosted execution environments on customer-controlled infrastructure. Coder Agent Relay brokers the connection between the two and manages the lifecycle of the Coder workspaces where Claude Code agents execute.

**How is responsibility divided between Anthropic and Coder?**
Anthropic provides the Claude Code developer experience, cloud-session orchestration, environment queue, runner software, session protocol, and AI inference. The customer creates and operates the self-hosted environment and compute. Coder provides the self-hosted execution layer, including declarative workspace provisioning, networking, governance, and secure development environments. Agent Relay connects Claude Code cloud sessions to Coder workspaces and manages the lifecycle of those environments.

**What runs inside the customer's infrastructure?**
Coder runs inside customer-controlled infrastructure, including the Coder control plane, Agent Relay, and the workspaces where Claude Code agents execute. Claude Code's agent orchestration and AI inference remain cloud-hosted. The Anthropic self-hosted runner inside each Coder workspace communicates directly with the corresponding Claude Code cloud session.

**Is Claude Code fully self-hosted through this integration?**
No. The agent execution environment is self-hosted, not Claude Code itself. Claude Code's agent orchestration and AI inference remain cloud-hosted, while the environment where the agent accesses code, runs commands, uses development tools, and performs its work runs on customer-controlled infrastructure through Coder.

## Technical Architecture

**How does the technical integration work?**
Customers create Coder workspace templates using Terraform that install the Anthropic self-hosted runner when provisioned. When Agent Relay detects a new Claude Code cloud agent session, it claims the session and provisions or assigns it to a Coder workspace. The Anthropic self-hosted runner then communicates directly with the Claude Code cloud session, while Agent Relay coordinates the workspace lifecycle based on Claude Code request state and the status of the runner running inside the workspace.

**What is Coder Agent Relay?**
Coder Agent Relay is a broker that connects cloud-hosted AI agent sessions with self-hosted execution environments on Coder. For Claude Code, it monitors pending requests, validates and claims eligible sessions, triggers the Coder control plane to create the corresponding workspace, and coordinates its lifecycle. Once the Anthropic self-hosted runner connects, agent communication happens directly between the worker and Claude Code.

**Does Agent Relay proxy communication between Claude Code and the workspace?**
No. Agent Relay brokers the initial association between a Claude Code cloud session and a Coder workspace. Once that association is established, the Anthropic self-hosted runner inside the workspace communicates directly with Claude Code. Agent Relay continues to manage the workspace lifecycle but does not sit in the agent's communication path.

**How are Coder workspaces provisioned for Claude Code sessions?**
Customers configure a Claude pool in Agent Relay and map it to a Coder organization and Terraform-based workspace template. When Agent Relay claims a session work order, it validates the Anthropic-attested account identity, matches the account email to an active member of the mapped Coder organization, and asks the Coder control plane to create a workspace from that template for that user. Coder handles the actual provisioning and deprovisioning, while Agent Relay coordinates those lifecycle actions based on the state of the Claude Code session and runner.

**What happens when a Claude Code agent session ends?**
The Anthropic self-hosted runner serves the session and exits when its work is complete. It reports runner state through Coder agent metadata, and Agent Relay's reaper detects completion and deletes the ephemeral workspace.

**Where does the Claude Code agent actually execute?**
The Claude Code agent executes inside a Coder workspace running on customer-controlled infrastructure. That workspace provides the agent with its development environment and access to the code, tools, dependencies, networks, and other resources made available by the customer.

**How is a Claude Code session routed to a Coder workspace?**
Customers create a named environment in Claude admin settings, then configure Agent Relay with that environment's credentials and map it to a Coder organization and workspace template. Developers select the environment for a Claude Code cloud session. Agent Relay polls Anthropic for a spawn hint, receives a short-lived single-use work order for the session, resolves the session owner, and creates the corresponding Coder workspace. The Anthropic self-hosted runner starts in that workspace and serves the session.

**Does Coder need to keep Anthropic self-hosted runners running all the time?**
No. The initial Agent Relay architecture is designed to scale to zero. Anthropic environments remain available even when no Coder workspaces are running. When a new request arrives, Agent Relay claims it and triggers creation of an ephemeral workspace for that session, which is deleted after the runner finishes. Pre-built warm capacity is being considered as a future optimization to reduce startup latency.

**Does each Claude Code agent get its own Coder workspace?**
Yes. Agent Relay creates an ephemeral Coder workspace for each Claude Code agent session. The workspace serves that session until the Anthropic self-hosted runner exits, after which Agent Relay triggers its deletion through the Coder control plane.

**Where does agent orchestration happen?**
Agent orchestration remains in Claude Code. Coder does not replace Claude Code's cloud-hosted orchestration plane. Agent Relay connects sessions created and orchestrated by Claude Code with the self-hosted Coder workspaces where their execution occurs.

**Where does AI inference happen?**
AI inference remains in Anthropic's cloud. Coder does not perform or proxy AI inference in this integration. The distinction is between cloud-hosted orchestration and inference in Anthropic and self-hosted agent execution in Coder.

**Does Coder AI Gateway participate in Anthropic inference?**
No. Coder AI Gateway is not part of the inference path for this integration. Claude Code continues to handle AI inference through its own service while Coder provides the self-hosted environment where the agent executes.

**What data stays inside the customer's infrastructure?**
Agent execution occurs inside the customer's Coder deployment, allowing organizations to retain control over the infrastructure where their development environments, source repositories, credentials, internal services, and development tooling reside. Because the Anthropic self-hosted runner communicates with Anthropic and inference occurs through Anthropic, some information must cross the customer boundary. Specific data flows should be evaluated against Anthropic's architecture and security documentation rather than assuming that all data remains inside the customer's environment.

## Positioning & Competitive Differentiation

**What makes Coder different?**
Coder is self-hosted AI development infrastructure trusted by some of the world's most security-conscious organizations and regulated industries. It provides a consistent execution architecture for developers and AI agents across customer-controlled public cloud, private cloud, and on-premises infrastructure.

Unlike vendor-specific execution environments, Coder is infrastructure-, cloud-, model-, tool-, and agent-agnostic. Organizations can standardize how development environments are provisioned, connected, and governed while allowing developers to use the AI coding tools that best fit their needs. Agent Relay extends that architecture to cloud-hosted agents by connecting their sessions to self-hosted Coder execution environments.

**What does Coder add beyond a self-hosted runner?**
A runner provides compute for an agent. Coder provides complete development environments with declarative provisioning, enterprise networking, identity and access controls, governance, observability, lifecycle management, and access to the tools and resources developers and agents need to perform real software development. Agent Relay makes those environments available to supported cloud-hosted agents such as Claude Code.

**Why does the execution environment matter?**
Coding agents need real development environments with source code, dependencies, development tools, credentials, and access to internal systems. For many enterprises, those environments need to run on infrastructure they control. Coder lets organizations give Claude Code agents the environments they need while retaining control over where execution occurs and what enterprise resources those environments can access.

**How does this help with data sovereignty?**
The integration gives organizations control over the infrastructure where Claude Code agents execute and where development resources such as repositories, credentials, tools, and internal services reside. Claude Code's orchestration and inference remain cloud-hosted, so this should not be positioned as preventing all data from leaving the customer's environment.

**When is the Claude Code integration the right fit?**
The Claude Code integration is the right fit when a customer wants the Claude Code cloud agent experience but requires agent execution to occur on infrastructure they own or control. It is particularly relevant when customers need agents to work inside existing enterprise networks, access internal development resources, or operate within infrastructure governed by their platform and security teams.

## Product & Roadmap

**Does this replace Claude Code?**
No. Claude Code's developer experience, agent orchestration, and inference remain cloud-hosted. The integration changes where Claude Code agents execute by allowing those workloads to run inside self-hosted Coder workspaces on customer-controlled infrastructure.

**Is this available today?**
The Claude Code integration uses Coder Agent Relay to connect Claude Code cloud agent sessions with self-hosted Coder workspaces. Agent Relay is currently in Preview with select regulated enterprise customers.

**Is Agent Relay specific to Claude Code?**
No. Agent Relay is Coder infrastructure for connecting supported cloud-hosted AI agents with self-hosted execution environments on Coder. Agent Relay's underlying architecture can support other cloud-hosted agent providers as they enable self-hosted execution environments.

**Can organizations use agent harnesses other than Claude Code on Coder?**
Yes. Coder is agent- and model-agnostic. Organizations can run Coder's native harness, Coder Agents, and other popular agent harnesses directly inside Coder workspaces. Agent Relay extends that model to supported cloud-hosted agents, allowing their cloud-hosted orchestration to use self-hosted Coder environments for execution.

**How is the Claude Code integration different from running another agent inside a Coder workspace?**
Many agent harnesses can already be installed and run directly inside a Coder workspace. The Claude Code integration is different because Claude Code's agent orchestration remains cloud-hosted. Agent Relay provides the integration layer that automatically connects those cloud sessions to Coder workspaces and manages the execution environment throughout the session lifecycle.

**Does this change Coder's investment in Coder Agents?**
No. Coder Agents remains Coder's native agent experience for running completely self-hosted agent orchestration. Agent Relay addresses a different use case: giving customers a way to connect supported cloud-hosted agents to self-hosted Coder execution environments. Coder's broader strategy is to support both native Coder experiences and the AI tools developers choose.

**When should a customer use Claude Code with Agent Relay versus Coder Agents?**
Claude Code with Agent Relay is a strong fit when an organization wants the Claude Code cloud agent experience while requiring self-hosted execution environments. Coder Agents is Coder's native agent experience and is designed to run completely within Coder's self-hosted architecture. Customers can also use both depending on developer preferences and organizational requirements.

**Can a customer use Claude Code, Coder Agents, and other agents at the same time?**
Yes. Coder is designed to provide a common infrastructure layer for developers and AI agents rather than require organizations to standardize on a single agent harness. Customers can support multiple agent experiences while using Coder to standardize the development environments and infrastructure where those agents execute.

**Will Coder work with cloud agent providers beyond Anthropic?**
Yes. Coder is designed to remain agent-agnostic, and Agent Relay provides an architecture for connecting cloud-hosted agents to self-hosted Coder environments. Support for additional providers will depend on their ability to support self-hosted execution and specific product integrations.

## Frequently Misunderstood Concepts

**Does Coder replace Claude Code?**
No. Claude Code provides the developer experience, agent workflows, cloud-hosted orchestration, and inference. Coder provides the self-hosted execution environments where Claude Code agents perform their work.

**Does Agent Relay move Claude Code's control plane into Coder?**
No. Claude Code's control plane and agent orchestration remain cloud-hosted. Agent Relay connects cloud sessions to Coder workspaces but does not replicate or self-host Claude Code's control plane.

**Does Coder become the AI model provider?**
No. Coder does not provide or proxy the AI inference used by Claude Code as part of this integration. Inference remains the responsibility of Anthropic.

**Is Coder just another self-hosted runner?**
No. Coder provides complete development environments rather than standalone execution workers. Those environments can be declaratively provisioned with the development tools, networking, access controls, infrastructure, and enterprise resources required by both developers and AI agents.

**Does Agent Relay sit between the agent and Claude Code for the entire session?**
No. Agent Relay brokers the session and workspace association and manages the execution environment's lifecycle. Once connected, the Anthropic self-hosted runner inside the workspace communicates directly with the Claude Code cloud session.

**Is this only for regulated industries?**
No. Regulated industries are an important use case because their infrastructure and data requirements are often the most stringent, but the architecture benefits any organization that wants to use cloud-hosted AI agents while retaining control over their execution environments.
