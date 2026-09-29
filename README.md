# Maxym Gryn

Platform and SRE engineer in Calgary. Twenty years in software, the last six
owning production infrastructure for **HP Anyware** — a multi-cloud SaaS
platform on Azure, AWS and GCP serving 200 enterprise customers and ~300,000
sessions a day, supporting 30 engineers across 6 delivery teams and 20
microservices.

The work I care about is the kind that makes other engineers faster without
making them think about it: a release control plane that moved the org from
weekly to near-daily deploys and cut rollback from 60 minutes to 10, a
Terraform and GitHub Actions golden path that turned multi-day service setup
into a self-service action, mandatory SAST/SCA/image-scanning gates rolled
out across six teams without breaking a single release. Five years on-call,
ten Sev-1/Sev-2 incidents as incident commander.

## Running now

**[homelab](https://github.com/maxim-grin/homelab)** — a bare-metal Proxmox
platform run as a real environment, not a demo. Terraform provisions the VMs,
Ansible configures them, ArgoCD delivers applications to Kubernetes, and
HashiCorp Vault holds the secrets, resolved into manifests at sync time.
cert-manager issues Let's Encrypt certificates over ACME DNS-01 — with
separate Cloudflare tokens for the cluster and the LAN services, so either
can be revoked without touching the other.

Four CI jobs gate every pull request: pre-commit plus a full-history gitleaks
scan (the hook alone only sees staged changes, so in CI it would pass having
scanned nothing), conventional-commit checks, `terraform validate` and
tflint, and `kustomize build` / `helm template` output validated by
`kubeconform -strict`. Every action pinned to a commit SHA. ansible-lint at
production profile with no ignore file. Nothing in CI touches the cluster,
Proxmox or any secret — it only reads.

The README says what *isn't* there as carefully as what is.

## Also public

- **[cloud-report-portal](https://github.com/maxim-grin/cloud-report-portal)**
  — one secured document-generation service implemented four ways, idiomatic
  to Azure, AWS, GCP and OCI: Entra ID / Cognito / Identity Platform for auth,
  Functions / Lambda / Cloud Run for compute, object storage behind
  time-limited signed URLs, managed identities and private networking
  throughout. Includes a production-readiness pass and a per-cloud cost model.
- **[agent-sandbox](https://github.com/maxim-grin/agent-sandbox)** — Docker
  sandbox where an LLM agent clones, builds, tests and runs arbitrary repos
  under hard isolation: per-run networks and volumes, `cap_drop: ALL`,
  no-new-privileges, non-root execution, no Docker socket. Deterministic
  offline mock mode.
- **[shift-handoff](https://github.com/maxim-grin/shift-handoff)** —
  Kubernetes CronJob correlating overnight PagerDuty, Alertmanager,
  Kubernetes and Loki/CloudWatch data into one prioritized shift briefing.
  Degrades per collector rather than failing the run. Proof of concept.

## Reach me

Open to Senior Platform Engineer, SRE and Principal Engineer roles —
Calgary or remote.

[mgryn.cc](https://mgryn.cc) · [LinkedIn](https://linkedin.com/in/maximgrin)
· maxim.grin@gmail.com
