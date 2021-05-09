# Octopus Deploy Create Release Plugin

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) that enables you to create an Octopus deploy release for your pipelines

## Example

A basic configuration, assuming you already have the relevant Octopus API Key and Server environment variables set for [Octo CLI](https://octopus.com/docs/octopus-rest-api/octopus-cli)

```yml
steps:
  - command: echo 'Deploy preview created'
    plugins:
      - hu-danielgo/octopus-release#v0.0.1:
          # (optional) Names of env variables containing the API Key and Octopus Server URL
          # By default set to `OCTOPUS_CLI_API_KEY` and `OCTOPUS_CLI_SERVER`.
          octopus-api-key-env: OCTOPUS_CLI_API_KEY
          octopus-server-env: OCTOPUS_CLI_SERVER
          # See https://octopus.com/docs/octopus-rest-api/octopus-cli) for description of the below
          project: 'my-octopus-project' # required, can be name or ID
          packageVersion: '1.0.1' # required if auto package selection not enabled
          releaseNumber: '1.2.3' # optional (default: null)
          releaseNotesArtifactName: 'my_release_notes.md' # optional
```