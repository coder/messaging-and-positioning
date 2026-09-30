# Coder Workspaces FAQ

## Developer Experience

**Do developers have to change IDEs?**
No. Developers can use VS Code desktop or in the browser, JetBrains IDEs, Cursor, Devin Desktop (formerly Windsurf), Zed, or any SSH-capable editor, plus a web terminal and port forwarding. See [Access workspaces](https://coder.com/docs/user-guides/workspace-access).

**How fast do workspaces start?**
It depends on the template. Simple templates start quickly, and prebuilt workspaces (Premium) keep a pool of ready workspaces for each preset so developers can claim one without waiting for a full build. See [Prebuilt workspaces](https://coder.com/docs/admin/templates/extending-templates/prebuilt-workspaces).

**Can developers bring their dotfiles and existing dev container configurations?**
Yes. Coder can apply a developer's dotfiles repository to a workspace, and existing `devcontainer.json` configurations can be reused on Linux workspaces. The Dev Containers integration isn't supported in Windows or macOS workspaces. See [Dotfiles](https://coder.com/docs/user-guides/workspace-dotfiles) and [Dev Containers](https://coder.com/docs/admin/integrations/devcontainers).

## Infrastructure and Deployment

**What can a workspace run on?**
Anything Terraform can provision, including VMs, Kubernetes pods, and Docker containers on Linux, Windows, or macOS, and on x86-64 or ARM. See [Templates](https://coder.com/docs/admin/templates).

**Where can Coder be installed?**
On Kubernetes, which is recommended for production, and on OpenShift, Rancher, Docker, RPM-based Linux, or VMs on AWS, Azure, or GCP. Coder is also listed on the AWS and GCP marketplaces. See [Install Coder](https://coder.com/docs/install/server).

**Can Coder run fully air-gapped?**
Yes. All Coder features are supported in air-gapped and offline deployments, using a Terraform provider mirror and offline license checks. Telemetry and update checks can be disabled. See [Air-gapped deployments](https://coder.com/docs/install/prepare/airgap).

**How many users can Coder support?**
Coder publishes validated reference architectures for 1,000, 2,000, 3,000, and 10,000 users on Kubernetes. The 10,000-user architecture is sized for 6,000 concurrently running workspaces. These are sizing guidelines, not guarantees. See [Scale Coder](https://coder.com/docs/install/plan/sizing).

**Does Coder support globally distributed teams?**
Yes. Workspace proxies (Premium) relay workspace traffic for teams in other regions to reduce latency. High availability (Premium) runs multiple control plane replicas within one region. See [Workspace proxies](https://coder.com/docs/admin/networking/workspace-proxies) and [High availability](https://coder.com/docs/admin/networking/high-availability).

## Security and Governance

**Which identity and Git providers does Coder work with?**
Users sign in with OIDC providers such as Okta, Keycloak, PingFederate, or Azure AD, or with GitHub. SCIM provisioning and IdP group sync are Premium. Workspaces authenticate to Git providers including GitHub, GitLab, Bitbucket, and Azure DevOps through external authentication. See [Users](https://coder.com/docs/admin/users) and [External authentication](https://coder.com/docs/admin/external-auth).

**Does Coder send data back to Coder?**
Deployment telemetry is on by default and can be disabled. Telemetry doesn't collect user email addresses, apart from the administrator's. See [Telemetry](https://coder.com/docs/admin/setup/telemetry).

**Can we audit what happens in workspaces?**
Yes. Audit logs and connection logs (Premium) record user and workspace actions and workspace connections, and audit logs can be exported to log management and SIEM tools such as Splunk. See [Audit logs](https://coder.com/docs/admin/security/audit-logs).

## Cost and Packaging

**How do we control compute cost?**
Autostart and autostop schedules stop idle workspaces. Premium adds quotas, dormancy, automatic cleanup, and required autostop, and template usage insights show where compute goes. See [Workspace scheduling](https://coder.com/docs/admin/templates/managing-templates/schedule) and [Quotas](https://coder.com/docs/admin/users/quotas).

**What does Premium add over Community?**
Community is free and open source. Premium adds enterprise controls such as audit logs, groups and custom roles, multiple organizations, SCIM and IdP sync, template permissions, quotas, prebuilt workspaces, workspace proxies, high availability, external provisioners, and AI Governance. See [Packaging](../../company/packaging.md) and [coder.com/pricing](https://coder.com/pricing).

**How can an organization evaluate Coder?**
The free Community edition installs in under 10 minutes with the [quickstart](https://coder.com/docs/get-started). A free, unlimited 30-day Premium trial is available at [coder.com/trial](https://coder.com/trial).
