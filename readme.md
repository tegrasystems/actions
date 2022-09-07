# Github Actions for dotnet projects

## Table of contents
- [Github Actions for dotnet projects](#github-actions-for-dotnet-projects)
  - [Table of contents](#table-of-contents)
  - [Github Action for publishing dotnet projects](#github-action-for-publishing-dotnet-projects)
    - [Usage](#usage)
    - [Parameters](#parameters)
      - [Inputs](#inputs)
      - [Outputs](#outputs)
    - [Limitations](#limitations)
  - [Github Action for dotnet-format](#github-action-for-dotnet-format)
    - [Usage](#usage-1)
    - [Parameters](#parameters-1)
      - [Inputs](#inputs-1)
      - [Outputs](#outputs-1)
  - [License](#license)

## Github Action for publishing dotnet projects
Automatically deploy dotnet projects using [msbuild](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild?view=vs-2022) as part of your Github Actions workflow.

### Usage
Running on `pull_request` type `closed`
```yaml
name: "[CD]Deploy"

on:
  pull_request:
    branches: [ "Release" ]
    types: [ "closed" ]

jobs:
    Release:
    uses: tegrasystems/actions/.github/workflows/dotnet-publish.yml@master
    with:
      project-path: PATH_TO_PROJECT
      publishprofile: PATH_TO_PUBLISHPROFILE
      password: PASSWORD
      configuration: CONFIGURATION
```

### Parameters
#### Inputs

| Name | Description | Type |
| --- | ----------- | ----- |
| project-path | Path to `.csproj` to deploy | string |
| publishprofile | Path to `.pubxml` of the project to deploy | string |
| password | Password needed for `publishprofile`  | string |
| configuration | (optional) Name of configuration  | string |
| additional-arguments | (optional) Additional switches to use in msbuild command, see [msbuild documentation](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild-command-line-reference?view=vs-2022#switches) for more information | string |

#### Outputs
Currently there is no outputs

### Limitations
At this moment it is not possible to run this Github Action without using a publishprofile, for more information about making publishprofile see [Microsoft documentation](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/visual-studio-publish-profiles?view=aspnetcore-6.0)





## Github Action for dotnet-format
Run [dotnet-format](https://github.com/dotnet/format) as part of your workflow to auto fix violations as part of your pull request workflow.

### Usage
Running on `pull_request`
```yaml
name: "[CI]Build, Test and Lint"

on: pull_request
jobs:
  dotnet-format:
    uses: tegrasystems/actions/.github/workflows/dotnet-format.yml@master
    with:
        project: PROJECT_PATH
        project-name: PROJECT_NAME
```

### Parameters
#### Inputs

| Name | Description | Type |
| --- | ----------- | ----- |
| project | Path to `.csproj` or `.sln` file | string |
| project-name | Name of the project, will be displayed as name of job  | string |

#### Outputs
| Name | Description | Type |
| --- | ----------- | ----- |
| has-changes | `true` if any files were found to have fixes applied. Will be a string of `true` or `false` | string |
| changes | (optional) if `has-changes` is `true`, every change made by [dotnet-format](https://github.com/dotnet/format) will be returned as [git-diff](https://git-scm.com/docs/git-diff) | string |

## License
The scripts and documentation in this project are released under the [MIT License](https://github.com/xt0rted/dotnet-format/blob/main/LICENSE)

