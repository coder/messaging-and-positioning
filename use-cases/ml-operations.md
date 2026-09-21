# ML Operations

## Summary

Coder gives ML engineers on-demand access to the GPUs and remote compute they need to train models safely and performantly, without relying on personal hardware or pulling sensitive training data onto laptops.

## Who This Is For

- **Data engineers and data scientists**, who need to build and train ML models against large volumes of data that require heavy processing power, and want their models to train faster.
- **DevSecOps and platform teams**, secondarily, who have to enforce data governance over training data without stalling data engineers' and scientists' progress. Governance and time to market are often in tension here.

## The Problem

Training models requires significant compute that strains local hardware, and it's rarely viable for every data engineer or scientist to have dedicated GPUs of their own. Intensive training sessions can degrade or effectively lock up a local machine for the duration of the job, keeping the engineer from doing anything else. Sensitive or proprietary training data pulled onto individual laptops introduces breach and privacy risk. Distributed teams often end up with inconsistent access to training data, since each engineer may compile their own local copies. And idle GPU and CPU capacity, if left running, can escalate cloud costs quickly. On top of all this, many ML platforms force engineers into notebook-only or terminal-only tooling, sacrificing the IDEs they'd otherwise prefer.

## Desired Outcome

ML engineers get on-demand access to powerful, shared GPU and CPU compute instead of needing dedicated personal hardware. Training runs remotely, so a local machine stays responsive during heavy jobs instead of being effectively taken out of commission. Training data stays inside a secure, centrally governed environment rather than landing on laptops, and distributed teams work from the same consistent, high-quality data instead of compiling their own local copies. Idle compute is scheduled down automatically to control cost, and engineers keep using the tools they already prefer, like VS Code or PyCharm, instead of being locked into a notebook-only workflow.

## How Coder Solves It

### On-Demand GPU and CPU Access

Moving development to the cloud gives engineers access to more powerful CPUs and GPUs than local hardware could provide, without requiring dedicated hardware per engineer. Because training happens in a remote workspace, engineers aren't blocked by local hardware constraints and can keep working while a processing-heavy job runs elsewhere. Autostart and autostop scheduling brings idle compute down automatically to keep spend under control.

### Keeping Sensitive Training Data Governed

Development happens next to the training data in a centralized cloud or on-premises environment, so engineers never need to pull sensitive or proprietary data down to their own machines. That data stays inside a secure environment protected by the organization's existing data governance policies and monitoring, and distributed teams work from the same consistent, reliable training data instead of compiling their own local copies.

### Familiar Tools, Not Notebook Lock-In

ML engineers keep using modern tools like VS Code and PyCharm rather than being restricted to the notebook-like tools or terminal access that most ML platforms force on them, while the actual training workload runs on powerful cloud resources behind the scenes.

## Products Involved

- **Coder Workspaces** — provisions the GPU- and CPU-backed environments engineers train against, and schedules that compute up and down as needed.

## Proof Points

- Palantir developers previously relied on high-end laptops paired with extra GPUs for machine learning projects before moving that work onto Coder-managed infrastructure ([Palantir success story](https://coder.com/success-stories/palantir)).
- Skydio reduced cloud computing costs for development environments by 90% by automating the shutdown of unused VMs and GPUs; its previous homegrown system provisioned GPUs manually with no automated deprovisioning, leaving them running, and billing, around the clock ([Skydio success story](https://coder.com/success-stories/skydio)).

## Known Limitations

Coder schedules and governs access to compute; it doesn't create additional GPU capacity on its own. Actual GPU availability still depends on the underlying cloud or on-premises infrastructure the organization provisions.

## Related Use Cases

- [Compute / Resource Optimization](./compute-resource-optimization.md)
- [Deploy AI Coding Agents](./deploy-ai-coding-agents.md)
- [Secure Development Environments](./secure-development-environments.md)

## Related Audiences

- [Data Scientist](../audiences/data-scientist.md)
- [ML Engineer](../audiences/ml-engineer.md)
