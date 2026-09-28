# Agent Relay for Cursor FAQ

## Understanding the Partnership

**Who is Cursor?**
Cursor is an AI coding platform helping developers and engineering teams build software with AI. Cursor's product is designed for complex codebases, supports frontier models from leading providers, and gives teams tools to configure model access, MCP controls, and system-level agent rules.

**Who is Coder?**
Coder is the self-hosted, cloud-agnostic infrastructure layer that governs how AI development runs inside the enterprise. It standardizes development environments, gives platform and security teams centralized control over AI model access and usage, and lets both human developers and autonomous agents work in the same governed environment, on infrastructure the customer already owns.

**How would you summarize the architecture in one sentence?**
Cursor orchestrates and performs inference, Coder provides the self-hosted execution environment, and Agent Relay connects the two.

**Why is Cursor partnering with Coder?**
Cursor has built one of the industry's most compelling AI coding experiences, but many enterprises need greater control over where AI agents execute and what resources they can access. Together, Cursor and Coder give organizations a way to use Cursor's cloud agent experience while running agent workloads inside self-hosted Coder environments on infrastructure they own and govern.

**What customer problem does this solve?**
Cloud-hosted coding agents need access to source code, dependencies, internal services, development tooling, and other enterprise resources to do useful work. Many organizations cannot provide that access inside vendor-managed execution environments. Coder gives Cursor agents self-hosted development environments inside the customer's infrastructure while preserving the Cursor cloud agent experience developers already use.

**Who is this solution designed for?**
The joint solution is designed for organizations that want to adopt cloud-hosted AI coding agents while retaining control over the infrastructure where those agents execute. This is particularly relevant to financial services, government, defense, healthcare, critical infrastructure, and large enterprises with strict security, compliance, or data sovereignty requirements.

## The Joint Solution

**What does the partnership provide?**
Cursor provides the cloud agent experience, orchestration, and inference developers already use, while Coder provides self-hosted execution environments on customer-controlled infrastructure. Coder Agent Relay brokers the connection between the two and manages the lifecycle of the Coder workspaces where Cursor agents execute.

**How is responsibility divided between Cursor and Coder?**
Cursor provides the developer experience, cloud-hosted agent orchestration, and AI inference. Coder provides the self-hosted execution layer, including declarative workspace provisioning, networking, governance, and secure development environments. Agent Relay connects Cursor cloud sessions to Coder workspaces and manages the lifecycle of those environments.

**What runs inside the customer's infrastructure?**
Coder runs inside customer-controlled infrastructure, including the Coder control plane, Agent Relay, and the workspaces where Cursor agents execute. Cursor's agent orchestration and AI inference remain cloud-hosted. The Cursor worker inside each Coder workspace communicates directly with the corresponding Cursor cloud session.

**Is Cursor fully self-hosted through this integration?**
No. The agent execution environment is self-hosted, not Cursor itself. Cursor's agent orchestration and AI inference remain cloud-hosted, while the environment where the agent accesses code, runs commands, uses development tools, and performs its work runs on customer-controlled infrastructure through Coder.

## Technical Architecture

**How does the technical integration work?**
Customers create Coder workspace templates using Terraform that install the Cursor worker when provisioned. When Agent Relay detects a new Cursor cloud agent session, it claims the session and provisions or assigns it to a Coder workspace. The Cursor worker then communicates directly with the Cursor cloud session, while Agent Relay coordinates the workspace lifecycle based on Cursor request state and the status of the worker running inside the workspace.

**What is Coder Agent Relay?**
Coder Agent Relay is a broker that connects cloud-hosted AI agent sessions with self-hosted execution environments on Coder. For Cursor, it monitors pending requests, validates and claims eligible sessions, triggers the Coder control plane to create the corresponding workspace, and coordinates its lifecycle. Once the Cursor worker connects, agent communication happens directly between the worker and Cursor.

**Does Agent Relay proxy communication between Cursor and the workspace?**
No. Agent Relay brokers the initial association between a Cursor cloud session and a Coder workspace. Once that association is established, the Cursor worker inside the workspace communicates directly with Cursor. Agent Relay continues to manage the workspace lifecycle but does not sit in the agent's communication path.

**How are Coder workspaces provisioned for Cursor Agents?**
Customers configure a Cursor pool in Agent Relay and map it to a Coder organization and Terraform-based workspace template. When Agent Relay detects and claims an eligible Cursor request, it asks the Coder control plane to create a workspace from that template for the requesting user. Coder handles the actual provisioning and deprovisioning, while Agent Relay coordinates those lifecycle actions based on the state of the Cursor session and worker.

**What happens when a Cursor agent session ends?**
The Cursor worker remains available for follow-up messages during a configurable idle period. When that period expires, the worker exits and reports its completed status through the Coder workspace. Agent Relay's reaper detects the completed worker and triggers the Coder control plane to delete the workspace.

**Where does the Cursor agent actually execute?**
The Cursor agent executes inside a Coder workspace running on customer-controlled infrastructure. That workspace provides the agent with its development environment and access to the code, tools, dependencies, networks, and other resources made available by the customer.

**How does Cursor know which Coder workspace should handle a session?**
Customers configure Cursor worker pools in Agent Relay and map each pool to a Coder organization and workspace template. Developers select the appropriate pool in Cursor, and Agent Relay monitors that pool for pending requests. When it claims a request, it creates a unique worker ID and triggers the corresponding Coder workspace, allowing Cursor to route the session to the worker running inside it.

**Does Coder need to keep Cursor workers running all the time?**
No. The initial Agent Relay architecture is designed to scale to zero. Cursor pools remain available even when no Coder workspaces are running. When a new request arrives, Agent Relay claims it and triggers creation of an ephemeral workspace for that session, which is deleted after the worker finishes. Startup latency is an active area of investment as the architecture matures.

**Does each Cursor agent get its own Coder workspace?**
Yes. Agent Relay creates an ephemeral Coder workspace for each Cursor agent session. The workspace serves that session until the Cursor worker exits, after which Agent Relay triggers its deletion through the Coder control plane.

**Where does agent orchestration happen?**
Agent orchestration remains in Cursor. Coder does not replace Cursor's cloud-hosted orchestration plane. Agent Relay connects sessions created and orchestrated by Cursor with the self-hosted Coder workspaces where their execution occurs.

**Where does AI inference happen?**
AI inference remains in Cursor. Coder does not perform or proxy AI inference as part of this integration. The distinction is between cloud-hosted orchestration and inference in Cursor and self-hosted agent execution in Coder.

**Does Coder AI Gateway participate in Cursor inference?**
No. Coder AI Gateway is not part of the inference path for this integration. Cursor continues to handle AI inference through its own service while Coder provides the self-hosted environment where the agent executes.

**What data stays inside the customer's infrastructure?**
Agent execution occurs inside the customer's Coder deployment, allowing organizations to retain control over the infrastructure where their development environments, source repositories, credentials, internal services, and development tooling reside. Because the Cursor worker communicates with Cursor and inference occurs through Cursor, some information must cross the customer boundary. Specific data flows should be evaluated against Cursor's architecture and security documentation rather than assuming that all data remains inside the customer's environment.

## Positioning & Competitive Differentiation

**What makes Coder different?**
Coder is self-hosted AI development infrastructure trusted by some of the world's most security-conscious organizations and regulated industries. It provides a consistent execution architecture for developers and AI agents across customer-controlled public cloud, private cloud, and on-premises infrastructure.

Unlike vendor-specific execution environments, Coder is infrastructure-, cloud-, model-, tool-, and agent-agnostic. Organizations can standardize how development environments are provisioned, connected, and governed while allowing developers to use the AI coding tools that best fit their needs. Agent Relay extends that architecture to cloud-hosted agents by connecting their sessions to self-hosted Coder execution environments.

**What does Coder add beyond a self-hosted runner?**
A runner provides compute for an agent. Coder provides complete development environments with declarative provisioning, enterprise networking, identity and access controls, governance, observability, lifecycle management, and access to the tools and resources developers and agents need to perform real software development. Agent Relay makes those environments available to supported cloud-hosted agents such as Cursor.

**Why does the execution environment matter?**
Coding agents need real development environments with source code, dependencies, development tools, credentials, and access to internal systems. For many enterprises, those environments need to run on infrastructure they control. Coder lets organizations give Cursor agents the environments they need while retaining control over where execution occurs and what enterprise resources those environments can access.

**How does this help with data sovereignty?**
The integration gives organizations control over the infrastructure where Cursor agents execute and where development resources such as repositories, credentials, tools, and internal services reside. Cursor's orchestration and inference remain cloud-hosted, so this should not be positioned as preventing all data from leaving the customer's environment.

**When is the Cursor integration the right fit?**
The Cursor integration is the right fit when a customer wants the Cursor cloud agent experience but requires agent execution to occur on infrastructure they own or control. It is particularly relevant when customers need agents to work inside existing enterprise networks, access internal development resources, or operate within infrastructure governed by their platform and security teams.

## Product & Roadmap

**Does this replace Cursor Cloud?**
No. Cursor's developer experience, agent orchestration, and inference remain cloud-hosted. The integration changes where Cursor agents execute by allowing those workloads to run inside self-hosted Coder workspaces on customer-controlled infrastructure.

**Is this available today?**
The Cursor integration uses Coder Agent Relay to connect Cursor cloud agent sessions with self-hosted Coder workspaces. Agent Relay is currently in Preview with select regulated enterprise customers.

**Is Agent Relay specific to Cursor?**
No. Agent Relay is Coder infrastructure for connecting supported cloud-hosted AI agents with self-hosted execution environments on Coder. Cursor is Coder's first integration partner for Agent Relay, and the underlying architecture is provider-agnostic by design.

**Can organizations use agent harnesses other than Cursor on Coder?**
Yes. Coder is agent- and model-agnostic. Organizations can run Coder's native harness, Coder Agents, and other popular agent harnesses directly inside Coder workspaces. Agent Relay extends that model to supported cloud-hosted agents, allowing their cloud-hosted orchestration to use self-hosted Coder environments for execution.

**How is the Cursor integration different from running another agent inside a Coder workspace?**
Many agent harnesses can already be installed and run directly inside a Coder workspace. The Cursor integration is different because Cursor's agent orchestration remains cloud-hosted. Agent Relay provides the integration layer that automatically connects those cloud sessions to Coder workspaces and manages the execution environment throughout the session lifecycle.

**Does this change Coder's investment in Coder Agents?**
No. Coder Agents remains Coder's native agent experience for running completely self-hosted agent orchestration. Agent Relay addresses a different use case: giving customers a way to connect supported cloud-hosted agents to self-hosted Coder execution environments. Coder's broader strategy is to support both native Coder experiences and the AI tools developers choose.

**When should a customer use Cursor with Agent Relay versus Coder Agents?**
Cursor with Agent Relay is a strong fit when an organization wants the Cursor cloud agent experience while requiring self-hosted execution environments. Coder Agents is Coder's native agent experience and is designed to run completely within Coder's self-hosted architecture. Customers can also use both depending on developer preferences and organizational requirements.

**Can a customer use Cursor, Coder Agents, and other agents at the same time?**
Yes. Coder is designed to provide a common infrastructure layer for developers and AI agents rather than require organizations to standardize on a single agent harness. Customers can support multiple agent experiences while using Coder to standardize the development environments and infrastructure where those agents execute.

**Will Coder work with cloud agent providers beyond Cursor?**
Agent Relay's architecture is provider-agnostic by design and not built exclusively for Cursor. We aren't able to comment on specific unannounced partnerships or roadmap timing.

## Frequently Misunderstood Concepts

**Does Coder replace Cursor?**
No. Cursor provides the developer experience, agent workflows, cloud-hosted orchestration, and inference. Coder provides the self-hosted execution environments where Cursor agents perform their work.

**Does Agent Relay move Cursor's control plane into Coder?**
No. Cursor's control plane and agent orchestration remain cloud-hosted. Agent Relay connects cloud sessions to Coder workspaces but does not replicate or self-host Cursor's control plane.

**Does Coder become the AI model provider?**
No. Coder does not provide or proxy the AI inference used by Cursor as part of this integration. Inference remains the responsibility of Cursor.

**Is Coder just another self-hosted runner?**
No. Coder provides complete development environments rather than standalone execution workers. Those environments can be declaratively provisioned with the development tools, networking, access controls, infrastructure, and enterprise resources required by both developers and AI agents.

**Does Agent Relay sit between the agent and Cursor for the entire session?**
No. Agent Relay brokers the session and workspace association and manages the execution environment's lifecycle. Once connected, the Cursor worker inside the workspace communicates directly with the Cursor cloud session.

**Is this only for regulated industries?**
No. Regulated industries are an important use case because their infrastructure and data requirements are often the most stringent, but the architecture benefits any organization that wants to use cloud-hosted AI agents while retaining control over their execution environments.
