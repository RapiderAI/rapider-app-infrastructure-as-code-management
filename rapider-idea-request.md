<!-- Rapider Official App SOW & Specification | App #110: Infrastructure as Code Management (infrastructure-as-code-management) | Domain: DEV -->

# #110 Infrastructure as Code Management (`infrastructure-as-code-management`) — Scope of Work (SOW)

- **App Number & Name:** `#110 Infrastructure as Code Management`
- **Proposed App Key:** `infrastructure-as-code-management`
- **Domain / Suite & Model Prefix:** `DEV` (`Dev*`) — Category `11. Software Development & DevOps`
- **Representative Benchmark (`P1`):** `Terraform Cloud` (`HCP Terraform`)
- **Combined Feature Catalog:** [../combined-features/110-infrastructure-as-code-management-features.md](../combined-features/110-infrastructure-as-code-management-features.md)

---

## 1. Executive Outcome & Target Audience

**Infrastructure as Code Management (`infrastructure-as-code-management`)** provides platform engineering, DevOps, SRE, and FinOps teams with a centralized, multi-engine (`Terraform`, `OpenTofu`, `Pulumi`, `Bicep`) control plane inside the Rapider `DEV` suite. Instead of running unlogged `terraform apply` commands from developer laptops with local `.tfstate` files, static cloud keys, surprise cloud bills, and silent out-of-band console drift, organizations govern every cloud change through encrypted remote state locking, speculative Pull Request `plan` diffs, pre-apply `Decimal128` FinOps cost deltas, OPA/Sentinel Policy-as-Code guardrails, self-service No-Code module blueprints, and scheduled drift reconciliation.

*(Terminology Note: Following Rapider's Workspace Naming Convention, the tenant organization in user-facing UI is always **Workspace**, while isolated IaC state environments managed by `#110` are named **IaC Stacks** / `DevIacStack`.)*

- **SME & Startup Fast-Path:** A DevOps engineer registers a `DevIacStack` in `stack-drawer` connected to a Git repository and OIDC cloud identity, automatically gaining pessimistic state locking, visual `+ / ~ / -` PR plan previews, `preventDestroy` database locks, and one-click gated production `apply`—eliminating shared S3/DynamoDB bootstrap toil.
- **Enterprise Progressive Disclosure:** Multi-cloud platform teams unlock a curated `DevIacModule` Private Registry with No-Code self-service developer blueprints, directed cross-stack dependency graphs, `ADVISORY` / `SOFT_MANDATORY` / `HARD_MANDATORY` OPA Rego `DevIacPolicy` gates, `FinBudget`-linked monthly cost guardrails, 4-eyes Home `WorkItem` approvals for destructive/cost-spiking `PROD` runs, private VPC `AGENT_POOL` runners, and automated ephemeral TTL sandbox teardowns.
- **Measurable Business & Engineering Outcomes:**
  1. Eliminate **100% of concurrent state-corruption outages and static cloud access keys** via pessimistic `DevIacStateVersion` locking and dynamic OIDC workload identity federation.
  2. Cut wasted non-production cloud spend by **25%–45%** via pre-apply `Decimal128` monthly cost delta gates (e.g., catching accidental `+\$3,800.00/mo` GPU/NAT sizing before `apply`) and automated ephemeral TTL `destroy` schedules.
  3. Detect and reconcile **100% of unauthorized cloud console click-ops drift** within scheduled health-assessment windows.
- **Top 6 Global Benchmarks Synthesized (`P1`–`P6`):** `Terraform Cloud / HCP Terraform` (`P1` — Representative Product), `Spacelift` (`P2`), `env0` (`P3`), `Pulumi Cloud` (`P4`), `ServiceNow Cloud Provisioning & Governance` (`P5`), and `Oracle Cloud Resource Manager & MS Azure Deployment Environments` (`P6`).

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### In-Scope
- Managing `DevIacStack` units (`TERRAFORM`, `OPENTOFU`, `PULUMI`, `BICEP_ARM`), directed dependency graphs, `preventDestroy` locks, ephemeral `ttlExpiresAt` lifecycles, and envelope-encrypted `DevIacStateVersion` snapshots with pessimistic locking (`IAC-001`, `IAC-002`, `IAC-004`, `IAC-012`, `IAC-021`, `IAC-024`).
- Managing `DevIacVariableSet` inputs, write-only Secret Manager bindings, and dynamic OIDC cloud provider profiles (`AWS`, `GCP`, `Azure`, `OCI`) (`IAC-003`, `IAC-009`).
- Executing speculative PR `plan` and gated `apply`/`destroy` `DevIacRun` pipelines with structured `+ / ~ / - / +-` resource diffs, OPA/Sentinel `DevIacPolicy` checks, `Decimal128` FinOps cost deltas, and 4-eyes Home `WorkItem` approvals (`IAC-005`–`IAC-008`, `IAC-022`, `IAC-025`).
- Publishing versioned `DevIacModule` blueprints, No-Code self-service provisioning, `DevIacDriftAssessment` scheduled health/drift scans, unmanaged resource `import` assistance, and grounded AI blast-radius/Rego/drift assistants (`IAC-010`, `IAC-011`, `IAC-013`–`IAC-020`, `IAC-023`, `IAC-026`–`IAC-028`).

### Out-of-Scope
- Real-time 1-second host CPU/RAM/network metric scraping and APM trace ingestion (owned by `#083 Cloud Infrastructure Monitoring` and `#104 Application Error Tracking`).
- Static AST security scanning of general application code (Java/TS/Python) (owned by `#107 Code Quality & Static Analysis`; `#110` consumes `#107` HCL/IaC scan badges via pre-apply Run Tasks).
- General-purpose corporate accounting, vendor invoicing, and GL journal entries (owned by `FIN`; `#110` references `FinBudget` thresholds for FinOps cloud gates).
- Storing raw plaintext cloud credentials, TLS private keys, or database passwords in app tables (delegated strictly to Rapider Platform Secret Manager).

### Cross-Suite Ownership & Integration Contract

| Domain / App | Owns (Canonical System of Record) | Integration Contract with `#110` (`infrastructure-as-code-management`) |
| :--- | :--- | :--- |
| **`#110` (`infrastructure-as-code-management`)** | `DevIacStack`, `DevIacStateVersion`, `DevIacVariableSet`, `DevIacRun`, `DevIacModule`, `DevIacPolicy`, `DevIacDriftAssessment` | Orchestrates state locks, `plan`/`policy`/`cost`/`apply` lifecycles, and publishes `dev.iac.apply_completed.v1` and `dev.iac.drift_detected.v1`. |
| **`FIN` (`budgeting`)** | `FinBudget`, `FinLegalEntity` | `DevIacStack` optionally links `finBudgetId` (`FinBudget`) so `DevIacRun` flags monthly cost deltas exceeding allocated cloud budgets. |
| **`#107` (`code-quality-and-static-analysis`)** | `DevCodeFinding` (`IAC_MISCONFIG`), `DevAnalyzedRepo` | `#110` displays `#107` security ratings on `DevIacModule` versions and executes pre-apply static HCL misconfiguration Run Tasks (`IAC-022`). |
| **`#083` & `#104` & `OPS` (`assets`)** | Infra Monitors (`#083`), `DevErrorIssue` (`#104`), `OpsOperationsAsset` (`assets`) | `#110` emits `dev.iac.apply_completed.v1` to annotate `#083`/`#104` incident timelines and synchronize provisioned cloud resources with `OpsOperationsAsset`. |
| **`APM` (`planning` / `apm`)** | `ApmProject`, `ApmIssue` | Drift remediation, outdated module upgrades, and infra change requests link directly to canonical `ApmIssue` work items. |
| **Platform Core Services** | Identity/RBAC, Secret Manager, Files/Drive, Notebooks, Home `WorkItem`s, `projectChannelMessage` | Encrypted state snapshots & plan JSONs reside in Platform Files; OIDC/secrets in Secret Manager; `PROD` `apply`/`destroy`/soft-policy overrides use Home `WorkItem`s; AI runs on `projectChannelMessage`. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture (12 Pages)

Every visible sidebar section strictly enforces the **Minimum 3 Items Rule** (`Stacks & Execution` = 3 items, `Modules & Drift` = 3 items, `Policy & FinOps` = 3 items; detail and drawer routes set `displayOnMenu: false`).

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX Standards |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `dashboard` | Infrastructure Control Overview | `Stacks & Execution` | `true` (Order 1) | KPI cards (`countSWR`/`findSWR`) for Active IaC Stacks, Runs Awaiting Approval, Drifted Stacks, Managed Monthly Spend (`Decimal128`), and Expiring TTL Previews. |
| 2 | `stacks` | IaC Stacks & State | `Stacks & Execution` | `true` (Order 2) | Dual Table + `<rapider-kanban>` Health Board (`HEALTHY`, `LOCKED_RUNNING`, `AWAITING_APPROVAL`, `DRIFTED`, `FAILED`); `#activeFilterTagsBar` with `Clear all`; engine/cloud pills; clickable stack name (`stack-detail`). |
| 3 | `runs` | Plan & Apply Runs | `Stacks & Execution` | `true` (Order 3) | Real-time `DevIacRun` pipeline queue showing `+add / ~change / -destroy` counts, `Decimal128` `\$`/mo cost delta badge, policy check pill, and clickable run code (`run-detail`). |
| 4 | `modules` | Private Module Registry | `Modules & Drift` | `true` (Order 4) | Versioned `DevIacModule` catalog (`aws`, `gcp`, `azure`, `k8s`) displaying `#107` security rating, consumer stack count, input/output schema badge, and `Edit`/`Delete` governance. |
| 5 | `self-service` | No-Code Provisioning Catalog | `Modules & Drift` | `true` (Order 5) | Developer-friendly blueprint cards (e.g., `Cloud Run Public API (.run.app, ingress=all)`, `Preview Postgres Sandbox`) launching validated form-driven stack provisioning. |
| 6 | `drift` | Drift & Health Assessments | `Modules & Drift` | `true` (Order 6) | `DevIacDriftAssessment` queue highlighting out-of-band cloud attribute diffs, failed continuous check assertions, **Queue Reconcile Plan**, and **Create Import `ApmIssue`**. |
| 7 | `policies` | Policy-as-Code Guardrails | `Policy & FinOps` | `true` (Order 7) | `DevIacPolicy` OPA Rego / Sentinel policy set manager (`ADVISORY`, `SOFT_MANDATORY`, `HARD_MANDATORY`) with plan-JSON policy tester and violation counter. |
| 8 | `variable-sets` | Variable Sets & OIDC Auth | `Policy & FinOps` | `true` (Order 8) | Reusable `DevIacVariableSet` & dynamic OIDC cloud provider federation profiles (`AWS IAM Role`, `GCP Workload Identity`, `Azure Federated Cred`), masking all secret refs. |
| 9 | `finops-analytics` | Cloud Cost & TTL Analytics | `Policy & FinOps` | `true` (Order 9) | Portfolio `Decimal128` monthly run-rate breakdown vs. `FinBudget`, prevented cost-spike leaderboard, ephemeral TTL savings chart, and Save-to-Notebook export. |
| 10 | `stack-detail` | Stack State, Graph & Dependencies | *(Hidden)* | `false` | State serial history (`DevIacStateVersion`), lock/unlock badge, upstream/downstream stack dependency DAG, sanitized output table, TTL timer, and **Queue Plan** CTA. |
| 11 | `run-detail` | Run Plan Diff, Policy & Apply Gate | *(Hidden)* | `false` | Structured `+ / ~ / - / +-` resource attribute tree, `Decimal128` Infracost line-item breakdown, OPA policy results, **Approve & Apply** / **Override Soft Policy** (Home `WorkItem`), and AI Blast-Radius (`projectChannelMessage`). |
| 12 | `stack-drawer` | Create / Edit IaC Stack | *(Hidden)* | `false` | Sliding form drawer for `DevIacStack` setup (engine, Git path, tier, `preventDestroy`, TTL, `FinBudget` link); enforces `try/catch/finally`, SWR invalidation, and auto-close. |

**Mandatory Rapider UI Compliance across all 12 Pages:**
- Initial loads exclusively call `window.rapiderApi.findSWR` and `countSWR` with zero redundant `isDeleted` filter clauses; local in-memory arrays filter `item.isDeleted !== true` and update optimistically on edit/lock/approve/delete.
- Tables never render a standalone "View" button in `Actions`; primary identifiers (`stackName`, `runCode`, `moduleName`, `policyName`) navigate to detail views; `Edit` uses icon + text and `Delete` uses icon-only with `aria-label="Delete"`.
- Primary and destructive confirmation buttons (especially `Destroy` and `Delete`) enforce `#ffffff !important` text contrast and styled inline confirmation modals (`#rapiderConfirmOkBtn`); native `alert`/`confirm`/`prompt` are strictly banned.

---

## 4. Canonical Data Models (`Dev*` — 7 Models)

All models omit `projectId`, use backend-generated UUIDs (`00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in deterministic fixtures), enforce optimistic `version` checks, and store exact cloud cost figures as `Decimal128`.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`DevIacStack`** | `id` (UUID), `name` (String), `slug` (String), `engine` (`TERRAFORM` \| `OPENTOFU` \| `PULUMI` \| `BICEP_ARM`), `engineVersion` (String), `cloudProvider` (`AWS` \| `GCP` \| `AZURE` \| `OCI` \| `KUBERNETES`), `environmentTier` (`DEV` \| `STAGING` \| `PROD`), `executionMode` (`REMOTE_MANAGED` \| `AGENT_POOL`), `gitRepoRef` (String?), `workingDirectory` (String), `sourceModuleId` (UUID?), `autoApplyNonDestructive` (Boolean), `preventDestroy` (Boolean), `isLocked` (Boolean), `lockedByRunId` (UUID?), `driftStatus` (`CLEAN` \| `DRIFTED` \| `UNKNOWN`), `currentMonthlyCost` (`Decimal128`), `ttlExpiresAt` (DateTime?), `version` (Integer) | Optional `sourceModuleId` (`DevIacModule`), `upstreamStackIds` (`DevIacStack[]`), `finBudgetId` (`FinBudget`), `ownerUserId` (Platform Identity) | `slug` unique per Workspace; acyclic `upstreamStackIds` graph; for `PROD` tier, `preventDestroy` defaults `true` and `autoApplyNonDestructive` defaults `false`; `DESTROY` runs deterministically rejected while `preventDestroy = true`. |
| **`DevIacStateVersion`** | `id` (UUID), `stackId` (UUID), `producedByRunId` (UUID), `serialNumber` (Long), `lineageUuid` (UUID), `encryptedStateFileId` (UUID), `sha256Checksum` (String), `managedResourceCount` (Integer), `publicOutputs` (JSON), `sensitiveOutputKeys` (String[]), `createdAt` (DateTime) | Belongs to `DevIacStack` & `DevIacRun`; `encryptedStateFileId` refs Platform Files/Drive | **Strictly append-only immutable state ledger**; `serialNumber` strictly monotonic per `stackId`; raw `.tfstate` sensitive resource attributes are envelope-encrypted in Platform Files and never exposed in `publicOutputs`. |
| **`DevIacVariableSet`** | `id` (UUID), `name` (String), `scopeType` (`WORKSPACE_GLOBAL` \| `TIER_SCOPED` \| `STACK_SPECIFIC`), `oidcProviderConfig` (JSON?), `variables` (JSON[] — `{ key, category: 'HCL'\|'ENV', isSensitive: Boolean, plaintextValue?, secretManagerRefId? }`), `attachedStackIds` (UUID[]), `version` (Integer) | Referenced by `DevIacStack`; `secretManagerRefId` refs Platform Secret Manager | Whenever `isSensitive = true`, `plaintextValue` MUST be `null` (persisted exclusively in Platform Secret Manager; write-only in UI). |
| **`DevIacRun`** | `id` (UUID), `runCode` (String, e.g., `IAC-9204`), `stackId` (UUID), `runType` (`SPECULATIVE_PR_PLAN` \| `PLAN_AND_APPLY` \| `DESTROY` \| `REFRESH_DRIFT`), `commitSha` (String?), `pullRequestRef` (String?), `addCount` (Integer), `changeCount` (Integer), `replaceCount` (Integer), `destroyCount` (Integer), `priorMonthlyCost` (`Decimal128`), `proposedMonthlyCost` (`Decimal128`), `deltaMonthlyCost` (`Decimal128`), `policyOutcome` (`PASSED` \| `ADVISORY_WARN` \| `SOFT_FAILED` \| `HARD_BLOCKED`), `status` (`QUEUED` \| `PLANNING` \| `POLICY_COST_CHECK` \| `AWAITING_APPROVAL` \| `APPLYING` \| `APPLIED` \| `REJECTED` \| `ERRORED` \| `CANCELLED`), `planArtifactFileId` (UUID?), `homeWorkItemId` (UUID?), `version` (Integer) | Belongs to `DevIacStack`; optional `linkedApmIssueId` (`ApmIssue`), `homeWorkItemId` (Platform Home `WorkItem`), `threadChannelId` (`projectChannelMessage`) | `SPECULATIVE_PR_PLAN` can NEVER transition to `APPLYING`/`APPLIED`; `HARD_BLOCKED` runs can NEVER be overridden or applied; `PROD` `APPLY` / `DESTROY` / `SOFT_FAILED` overrides require an approved 4-eyes Home `WorkItem`. |
| **`DevIacModule`** | `id` (UUID), `namespace` (String), `name` (String), `provider` (String), `latestVersion` (String), `versions` (JSON[]), `inputSchemaJson` (JSON), `noCodeEnabled` (Boolean), `staticSecurityRating` (`A`..`E`), `status` (`PUBLISHED` \| `DEPRECATED` \| `REVOKED`), `consumerStackCount` (Integer), `version` (Integer) | Linked to `#107` `DevAnalyzedRepo` security rating; consumed by `DevIacStack` | Published semantic versions in `versions[]` are immutable; enabling `noCodeEnabled = true` requires `staticSecurityRating` of `A` or `B` and complete `inputSchemaJson` defaults/constraints. |
| **`DevIacPolicy`** | `id` (UUID), `name` (String), `engine` (`OPA_REGO` \| `SENTINEL_COMPAT`), `enforcementLevel` (`ADVISORY` \| `SOFT_MANDATORY` \| `HARD_MANDATORY`), `targetEnvironmentTiers` (String[]), `policySourceCode` (String), `maxMonthlyCostDelta` (`Decimal128`?), `isActive` (Boolean), `violationCount30d` (Integer), `version` (Integer) | Evaluated on `DevIacRun` | Active policies require syntax-valid Rego/rule validation before activation. |
| **`DevIacDriftAssessment`** | `id` (UUID), `stackId` (UUID), `assessedAt` (DateTime), `driftStatus` (`CLEAN` \| `DRIFTED` \| `CHECK_FAILED`), `driftedResourceCount` (Integer), `driftedResourcesDiff` (JSON[]), `failedAssertions` (JSON[]), `resolutionStatus` (`OPEN` \| `RECONCILE_QUEUED` \| `IMPORT_ISSUE_CREATED` \| `IGNORED`), `linkedApmIssueId` (UUID?), `version` (Integer) | Belongs to `DevIacStack`; `linkedApmIssueId` refs canonical `ApmIssue` | Sanitizes sensitive cloud attributes in `driftedResourcesDiff` before DB write. |

---

## 5. Core End-to-End User Journeys

1. **No-Code Self-Service Blueprint Provisioning (SME / App Developer Fast-Path):**
   - Backend engineer opens `#/self-service`, selects vetted module `gcp-cloud-run-public-api@2.1.0` (pre-configured per governance rules with direct `.run.app` URL and `ingress = all`), fills `serviceName = billing-webhook` and `environmentTier = STAGING`, and clicks **Provision Stack**.
   - `#110` creates `DevIacStack`, queues `DevIacRun` (`IAC-9204`), verifies OPA tags (`PASSED`) and FinOps delta (`+\$18.40/mo`), applies cleanly, and displays sanitized `.run.app` output URL on `#/stack-detail`.
2. **Production Destructive / Cost-Spike Plan -> Policy Check -> 4-Eyes Home `WorkItem` Gate:**
   - PR merge on `prod-postgres-cluster` queues `IAC-9210` showing `replaceCount = 1` (`+-` stateful instance replacement) and `deltaMonthlyCost = +\$1,250.00/mo` (`SOFT_MANDATORY` FinOps policy triggered).
   - Run pauses at `AWAITING_APPROVAL` and emits a shared Rapider Home `WorkItem` to the Cloud Infrastructure Lead.
   - Lead opens `#/run-detail`, reviews the AI Blast-Radius summary on `projectChannelMessage` highlighting the instance replacement downtime risk, rejects the run (`REJECTED`) with comment `"Use read-replica blue/green promotion instead of in-place replacement"`, preventing a production database outage.
3. **Out-of-Band Console Drift Detection & Reconciliation:**
   - Scheduled health assessment (`dev-iac-drift-assessment-wf`) detects someone manually opened port `22` on an AWS Security Group in the cloud console, marking `prod-vpc-network` `DRIFTED` (`#/drift`).
   - SRE clicks into `#/drift`, inspects the attribute diff (`ingress.cidr_blocks: [] -> ["0.0.0.0/0"]`), and clicks **Queue Reconcile Plan**—generating a gated `DevIacRun` that closes port `22` back to Git-defined state.
4. **Ephemeral PR Preview Sandbox Auto-Teardown (`TTL`):**
   - CI provisions preview stack `pr-512-preview` with `ttlExpiresAt = +24h`. Once 24 hours elapse (or PR `#512` closes), the TTL workflow automatically queues a guarded `DESTROY` run, reclaiming cloud resources and crediting savings on `#/finops-analytics`.
5. **List Search, Filter Tags, Click-Through & Back Restoration:**
   - On `#/stacks`, user filters `Tier: PROD` + `Drift: DRIFTED` and searches `"vpc"`. `#activeFilterTagsBar` displays dismissible chips and `Clear all`.
   - Clicking `prod-vpc-network` opens `#/stack-detail?id=...` cleanly; clicking `#btnGoBack` returns to `#/stacks` with all filter tags and `<rapider-kanban>` state preserved.

---

## 6. Consolidated Feature Priorities & Work Packages

### `P0` Foundation (MVP Release-Ready Core)
- **WP-P0-1: Stack Registry, Encrypted State Locking & OIDC Variable Sets (`IAC-001`–`IAC-003`, `IAC-016`, `IAC-021`):** `DevIacStack`, `DevIacStateVersion`, `DevIacVariableSet` schemas, pessimistic run locking, `preventDestroy` enforcement, Secret Manager integration, `#activeFilterTagsBar`, `#/dashboard`, `#/stacks`, `stack-drawer`, `#/stack-detail`, `#/variable-sets`.
- **WP-P0-2: Speculative Plan, OPA Policy, `Decimal128` Cost Delta & Gated Apply (`IAC-005`–`IAC-008`):** `DevIacRun` & `DevIacPolicy` engines, `+ / ~ / - / +-` diff viewer, `Decimal128` cost calculator, 4-eyes Home `WorkItem` approval gate, `#/runs`, `#/run-detail`, `#/policies`.
- **WP-P0-3: Private Module Registry, No-Code Catalog & Drift Detection (`IAC-010`, `IAC-011`, `IAC-014`, `IAC-015`):** `DevIacModule` & `DevIacDriftAssessment`, `#/modules`, `#/self-service`, `#/drift`, reconcile run trigger, and `ApmIssue` import handoff.

### `P1` Enterprise Cloud Governance & FinOps Scale
- **WP-P1-1: Stack Dependency DAGs, Agent Pools & Pre-Apply `#107` Run Tasks (`IAC-004`, `IAC-009`, `IAC-013`, `IAC-022`):** Cross-stack output triggers, private VPC `AGENT_POOL` routing, outdated module tracking, and `#107` HCL security webhook integration.
- **WP-P1-2: Ephemeral TTL Sandboxes, Continuous Assertions & FinOps/Asset Sync (`IAC-012`, `IAC-017`–`IAC-020`):** Automatic TTL `destroy` scheduler, post-apply health checks, `#/finops-analytics` (`FinBudget` comparison + Notebook export), and `OpsOperationsAsset` / `#083` / `#104` event sync.

### `P2` Adjacent Capabilities & Grounded AI Platform Assistant
- **WP-P2-1: Unmanaged Resource `import` Generator, Break-Glass Unlock & Tagging (`IAC-023`–`IAC-025`):** Read-only cloud discovery `import {}` generator, audited orphaned-lock release, and FinOps cost-center tag policies.
- **WP-P2-2: Grounded AI Blast-Radius, Rego Author & Drift Codifier (`IAC-026`–`IAC-028`):** Plain-English plan risk briefings, OPA Rego rule drafts, and HCL drift patches on `projectChannelMessage`.

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **Application Developer** | Provision approved No-Code `DevIacModule` blueprints in `DEV`/`STAGING`; view speculative PR `plan` diffs & non-sensitive stack outputs; extend ephemeral preview TTL within cap. | Cannot view raw `DevIacStateVersion` encrypted files, mutate `PROD` stacks directly, override `SOFT_MANDATORY` policies, or disable `preventDestroy`. |
| **DevOps / Infrastructure Engineer** | Create/edit `DevIacStack` & `DevIacVariableSet` (write-only secret refs); queue `PLAN_AND_APPLY` runs; publish `DevIacModule` versions; triage `DevIacDriftAssessment` items; invoke AI assistant. | Cannot self-approve own `PROD` `apply`/`destroy` or `SOFT_MANDATORY` override under 4-eyes policy; cannot read back sensitive variable values. |
| **Cloud / Platform Lead (Approver)** | All DevOps actions + author `DevIacPolicy` guardrails, approve/reject `PROD` `apply`/`destroy` & soft-policy Home `WorkItem`s, toggle `preventDestroy` (audited), and execute break-glass state unlock. | Cannot bypass `HARD_MANDATORY` policies during a run; cannot mutate append-only `DevIacStateVersion` snapshots. |
| **FinOps / Security Auditor** | Read-only access to `#/finops-analytics`, `DevIacPolicy` configurations, `DevIacRun` cost/policy audit trails, and `DevIacDriftAssessment` compliance posture. | Zero stack execution, state download, or credential mutation permissions. |
| **Scoped Runner / Agent Identity** | Pull single assigned `DevIacRun` bundle, mint short-lived OIDC token, upload new `DevIacStateVersion` while holding active `lockedByRunId` lease. | Scoped strictly to active run lease TTL; zero cross-stack read access. |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### Guarded Domain Commands
Every mutating command enforces RBAC, `idempotencyKey`, `correlationId`, and `expectedVersion`:
- `queueIacRun(stackId, runType, commitSha?, pullRequestRef?, expectedVersion, idempotencyKey)` -> Rejects `DESTROY` if `preventDestroy = true`; acquires pessimistic stack lock (for mutating runs) and dispatches plan worker.
- `recordPlanAndEvaluateGates(runId, planDiffSummary, costEstimateDecimal, planFileId, idempotencyKey)` -> Evaluates `DevIacPolicy` set + `#107` run task; transitions to `HARD_BLOCKED`, `AWAITING_APPROVAL` (emitting Home `WorkItem`), or `APPLYING` (if non-prod safe auto-apply).
- `decideIacRunApproval(runId, decision, overrideSoftPolicy, comment, expectedVersion, idempotencyKey)` -> Enforces 4-eyes non-self-approval (`initiatorUserId != actorUserId`), rejects any override if `policyOutcome == HARD_BLOCKED`, and dispatches `apply` worker.
- `commitStateVersion(stackId, runId, serialNumber, encryptedStateFileId, sha256Checksum, publicOutputs, idempotencyKey)` -> Verifies active `lockedByRunId == runId` and monotonic `serialNumber`, appends `DevIacStateVersion`, and releases stack lock.
- `forceUnlockStack(stackId, reasonComment, expectedVersion, idempotencyKey)` -> Audited Platform Lead break-glass release of orphaned runner locks.

### Kafka Domain Events (Published & Consumed)
- **Published:** `dev.iac.plan_completed.v1`, `dev.iac.policy_blocked.v1`, `dev.iac.approval_requested.v1`, `dev.iac.apply_completed.v1` (consumed by `#083`, `#104`, and `OPS` `OpsOperationsAsset`), `dev.iac.drift_detected.v1`, `dev.iac.ttl_expired.v1`.
- **Consumed:** `dev.git.pr_opened.v1` / `dev.git.pr_closed.v1` (queues speculative PR plan / triggers preview stack TTL `destroy`), `dev.code_quality.iac_scan_completed.v1` (updates `#107` pre-apply Run Task & `DevIacModule.staticSecurityRating`).

### `requiredWorkflows` in `app.manifest.json`
1. `dev-iac-plan-policy-cost-orchestrator-wf` (Executes isolated runner `plan`, computes `Decimal128` monthly cost delta, evaluates OPA/Sentinel policies, and creates Home `WorkItem`s for gated applies).
2. `dev-iac-state-commit-and-downstream-trigger-wf` (Seals encrypted `DevIacStateVersion`, emits asset/monitoring events, and queues speculative plans on dependent downstream stacks).
3. `dev-iac-drift-and-ttl-sweeper-wf` (Runs scheduled non-mutating `refresh-only` drift assessments and queues automated `DESTROY` runs on expired ephemeral non-prod stacks).
4. `dev-iac-ai-blast-radius-and-rego-wf` (Grounded AI plan blast-radius reviewer, OPA Rego drafter, and drift HCL patch proposer on `projectChannelMessage`—strictly barred from approving or executing `apply`/`destroy`).

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **Envelope-Encrypted State & Zero Plaintext Cloud Keys (CRITICAL):** Terraform/OpenTofu/Pulumi state files routinely contain sensitive resource attributes (e.g., initial DB passwords, TLS certs, webhook tokens). Raw state blobs are envelope-encrypted in Platform Files/Drive, never returned to browser clients, and `DevIacVariableSet` enforces write-only Platform Secret Manager references + dynamic OIDC short-lived tokens (`0` static long-lived AWS/GCP/Azure root keys stored in source or DB).
- **Accidental Data-Loss & Destructive Run Safeguards:** Production stacks enforce `preventDestroy = true` by default; `SPECULATIVE_PR_PLAN` runs execute with read-only credentials; any `DESTROY` or stateful `replaceCount > 0` in `PROD` requires explicit human 4-eyes confirmation via Home `WorkItem` and styled inline destructive confirmation modal (`#rapiderConfirmOkBtn` with `#ffffff !important` contrast).
- **FinOps Cost Accuracy:** Monthly cloud cost deltas and budget caps use `Decimal128` so multi-stack rollups never suffer float drift (e.g., exact `+\$1,250.00/mo`).
- **Accessibility & Responsive Parity:** WCAG 2.2 AA compliant across `390px` (on-call mobile run review), `768px`, and `1440px` (`light`/`dark` themes); `+ / ~ / - / +-` resource change icons pair symbols + labels with color; `findSWR` cached renders `< 150ms` p95.

---

## 10. Deterministic Acceptance Criteria

1. **Zero `projectId` & Platform UUIDs:** All 7 `Dev*` schemas contain zero `projectId` fields, generate backend UUIDs on creation, use `00000000-...` in seed fixtures, and label tenant vs. IaC unit cleanly as **Workspace** vs. **IaC Stack**.
2. **Pessimistic State Locking & Monotonic Serials:** Queuing a second mutating `DevIacRun` on a locked `DevIacStack` queues safely behind the active lock rather than running concurrently; attempting `commitStateVersion` with a stale `serialNumber` or mismatched `lockedByRunId` is deterministically rejected.
3. **Write-Only Secret & State Isolation:** Submitting a `DevIacVariableSet` variable with `isSensitive = true` stores the secret reference in Platform Secret Manager (`plaintextValue == null` in API read responses), and stack detail APIs expose only `publicOutputs`.
4. **`preventDestroy` & `HARD_MANDATORY` Unconditional Blocks:** Queuing `runType = DESTROY` on a stack with `preventDestroy = true` fails immediately with `409 PREVENT_DESTROY_ENABLED`; a run failing a `HARD_MANDATORY` `DevIacPolicy` transitions to `HARD_BLOCKED` and rejects all `decideIacRunApproval` attempts.
5. **Exact `Decimal128` Cost Gate & 4-Eyes Home `WorkItem`:** A `PROD` run with `deltaMonthlyCost = 1250.00` (`Decimal128`) breaching a `SOFT_MANDATORY` FinOps policy pauses in `AWAITING_APPROVAL`, emits a Rapider Home `WorkItem`, blocks self-approval, and proceeds to `APPLYING` only after authorized 4-eyes approval.
6. **Sidebar Minimum 3 Items Rule:** All 3 visible sidebar sections (`Stacks & Execution`, `Modules & Drift`, `Policy & FinOps`) each contain 3 visible items (`displayOnMenu: true`), while `stack-detail`, `run-detail`, and `stack-drawer` set `displayOnMenu: false`.
7. **SWR Clean Query & Optimistic Updates:** All pages load via `findSWR`/`countSWR` with zero `isDeleted` filter clauses; editing a policy, deprecating a module, or deleting a draft variable set updates local state and `<rapider-kanban>` optimistically, clears SWR cache, and rolls back on error.
8. **Table Actions, Contrast & Dialog Ban:** Zero tables render a "View" button in `Actions`; primary identifiers navigate to detail routes; `Edit` renders icon + text; `Delete` renders icon-only with `aria-label="Delete"`; primary/danger buttons enforce `#ffffff` text; zero `alert`/`confirm`/`prompt` calls exist.
9. **Active Filter Tags & Clear All:** Filtering `#/stacks` or `#/runs` renders `#activeFilterTagsBar` with HTML-escaped dismissible chips and `Clear all`, synchronously updating Table and `<rapider-kanban>` views.
10. **Drawer Auto-Close & `finally` Reset:** Saving or cancelling `stack-drawer` closes the drawer, broadcasts `RECORD_CREATED`/`RECORD_UPDATED`, and restores the Save button state inside `finally`.
11. **Click-Through Navigation & Back State Restoration:** Clicking `IAC-9204` on `#/runs` transitions cleanly to `#/run-detail?id=...` without `<base href>` 404 diversion, renders `+ / ~ / -` resource diffs, and `#btnGoBack` restores `#/runs` with active filters intact.
12. **Ephemeral TTL Auto-Destroy:** Expired non-production stacks (`ttlExpiresAt < now` and `preventDestroy = false`) deterministically enqueue a `DESTROY` run and record FinOps savings.
13. **Grounded AI Safety Boundary:** Requesting AI Blast-Radius analysis posts a resource/cost risk summary onto `projectChannelMessage` citing plan diff IDs and has zero permission to invoke `decideIacRunApproval` or `commitStateVersion`.
14. **Theme & Viewport Compliance:** Automated light/dark `validate_theme` checks and `390px`/`768px`/`1440px` layout validations pass cleanly.
