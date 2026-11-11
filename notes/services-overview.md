# Azure DevOps services overview

| Service | Purpose |
|---|---|
| **Azure Boards** | Work tracking: epics, features, user stories, tasks, bugs, sprints, Kanban boards |
| **Azure Repos** | Git repositories with branch policies and pull requests |
| **Azure Pipelines** | CI/CD: build, test and deploy to any platform or cloud |
| **Azure Test Plans** | Manual and exploratory testing |
| **Azure Artifacts** | Package feeds for NuGet, npm, Maven, Python and universal packages |

## Hierarchy

```text
Organization
└── Project
    ├── Boards
    ├── Repos
    ├── Pipelines
    ├── Test Plans
    └── Artifacts
```

## Pipeline concepts

- **Agent**: the machine that runs a job. Microsoft-hosted (fresh VM per job) or self-hosted.
- **Agent pool**: a group of agents a pipeline can target.
- **Stage → Job → Step**: a pipeline has stages, a stage has jobs, a job has steps (scripts or tasks).
- **Service connection**: stored credentials for an external system such as an Azure subscription,
  a container registry or a Kubernetes cluster.
- **Environment**: a deployment target (dev, prod) that can require approvals and checks.
- **Variable group**: a shared set of variables, optionally linked to Azure Key Vault.
- **Artifact**: files produced by one job or stage and used by a later one.

## Branch policies worth enabling on `main`

- Require a minimum number of reviewers
- Require a successful build before a pull request can complete
- Require linked work items
- Require all comments to be resolved
