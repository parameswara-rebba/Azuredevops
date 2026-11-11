# YAML pipeline cheat sheet

## Triggers

```yaml
trigger:            # CI: run on push
  branches:
    include: [main, release/*]
  paths:
    exclude: [docs/*]

pr:                 # run on pull requests targeting these branches
  branches:
    include: [main]

schedules:
- cron: "0 2 * * *" # 02:00 UTC every day
  displayName: Nightly build
  branches:
    include: [main]
  always: true
```

Use `trigger: none` to turn CI triggers off.

## Agent pool

```yaml
pool:
  vmImage: ubuntu-latest   # Microsoft-hosted
# pool:
#   name: MySelfHostedPool # self-hosted
```

## Variables

```yaml
variables:
  buildConfiguration: Release
  # or, list form with a variable group:
  # - group: my-variable-group
  # - name: buildConfiguration
  #   value: Release

steps:
- script: echo $(buildConfiguration)
```

| Syntax | When it is evaluated |
|---|---|
| `$(var)` | Macro, just before a task runs |
| `${{ variables.var }}` | Template expression, at compile time |
| `$[variables.var]` | Runtime expression, used in conditions |

Common predefined variables: `$(Build.BuildId)`, `$(Build.SourceBranchName)`,
`$(Build.SourcesDirectory)`, `$(Build.ArtifactStagingDirectory)`, `$(System.DefaultWorkingDirectory)`.

## Stages, jobs, steps

```yaml
stages:
- stage: Build
  jobs:
  - job: BuildJob
    steps:
    - script: echo building
- stage: Deploy
  dependsOn: Build
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
  jobs:
  - deployment: DeployJob
    environment: prod
    strategy:
      runOnce:
        deploy:
          steps:
          - script: echo deploying
```

## Artifacts

```yaml
- publish: $(Build.ArtifactStagingDirectory)
  artifact: drop

- download: current
  artifact: drop
```

## Templates

```yaml
# templates/build-steps.yml
parameters:
- name: configuration
  type: string
  default: Release
steps:
- script: echo Building ${{ parameters.configuration }}
```

```yaml
# azure-pipelines.yml
steps:
- template: templates/build-steps.yml
  parameters:
    configuration: Debug
```
