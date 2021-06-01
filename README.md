# Octopus Deploy Create Release Plugin

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) that enables you to create an Octopus deploy release for your pipelines

## Example

A basic configuration, assuming you already have the relevant Octopus API Key and Server environment variables set for [Octo CLI](https://octopus.com/docs/octopus-rest-api/octopus-cli)

```yml
steps:
  - command: echo 'Deploy preview created'
    plugins:
      - hu-danielgo/octopus-release#v0.1.3:
          # (optional) Names of env variables containing the API Key and Octopus Server URL
          # By default set to `OCTOPUS_CLI_API_KEY` and `OCTOPUS_CLI_SERVER`.
          octopus-api-key-env: OCTOPUS_CLI_API_KEY
          octopus-server-env: OCTOPUS_CLI_SERVER

          # See https://octopus.com/docs/octopus-rest-api/octopus-cli) for description of the below
          project: 'my-octopus-project' # required, can be name or ID
          packageVersion: '1.0.1' # required if auto package selection not enabled
          releaseNumber: '1.2.3' # optional (default: null)
          releaseNotesArtifactName: 'my_release_notes.md' # optional Buildkite artifact path
          releaseChannel: Channels-26 # optional Octopus Channel name or ID

          # (optional) Specifying these will additionally pack and push a package to the Octopus Package Repo
          packageId: "MyPackage" # the ID of the package to push
          packageInclude: "package*" # File pattern for files to include in package.
          # To include multiple patterns, seperate them with a space. e.g.:
          # packageInclude: "package* yarn*"
```