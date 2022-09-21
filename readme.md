# Github Action for dotnet-format
Run [dotnet-format](https://github.com/dotnet/format) as part of your workflow to auto fix violations as part of your pull request workflow.

## Usage
Running on `pull_request`
```yaml
name: "[CI]Build, Test and Lint"

on: pull_request
jobs:
  dotnet-format:
    runs-on: ubuntu-latest
    steps:
        -   uses: actions/checkout@v2
        -   name: dotnet-format
            uses: tegrasystems/dotnet-format@v1
            with:
                project: PROJECT_PATH
                project-name: PROJECT_NAME
                nuget-sources: <source>
                export-output: 'true'
```

## Parameters
### Inputs

| Name | Description | Type |
| --- | ----------- | ----- |
| project | Path to `.csproj` or `.sln` file | string |
| project-name | Name of the project, will be displayed as name of job  | string |
| nuget-sources | (optional) NuGet Sources to restore (Limited to 1 NuGet source) | string |
| export-output | (optional) Whether the changes should be in the output (Default: true) | boolean |

### Outputs
| Name | Description | Type |
| --- | ----------- | ----- |
| has-changes | `true` if any files were found to have fixes applied. Will be a string of `true` or `false` | string |
| changes | (optional) if `has-changes` is `true`, every change made by [dotnet-format](https://github.com/dotnet/format) will be returned as [git-diff](https://git-scm.com/docs/git-diff) | string |

## License
The scripts and documentation in this project are released under the [MIT License](https://github.com/xt0rted/dotnet-format/blob/main/LICENSE)

