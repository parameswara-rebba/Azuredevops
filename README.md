# Azuredevops

Notes and sample pipelines for Azure DevOps.

## Notes

- [Services overview](notes/services-overview.md) — Boards, Repos, Pipelines, Test Plans, Artifacts
- [YAML pipeline cheat sheet](notes/yaml-pipeline-cheat-sheet.md) — triggers, variables, stages, templates

## Sample pipelines

| File | What it shows |
|---|---|
| [basic-ci.yml](pipelines/basic-ci.yml) | Single-job build with a trigger and variables |
| [multi-stage.yml](pipelines/multi-stage.yml) | Build, then deploy to dev and prod with an approval gate |
| [docker-build-push.yml](pipelines/docker-build-push.yml) | Build a Docker image and push it to Azure Container Registry |

The pipelines are templates: replace the placeholder names (service connections,
registry, environments) with your own before running them.
