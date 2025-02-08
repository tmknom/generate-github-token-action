# generate-github-token-action

Generate an installation access token using GitHub Apps for GitHub Actions.

<!-- actdocs start -->

## Description

This action generates an installation access token for a specified GitHub App,
enabling authentication in GitHub Actions workflows.
You can specify one or more repositories to define its access scope.

## Usage

```yaml
  steps:
    - name: Generate GitHub Token
      uses: tmknom/generate-github-token-action@v0
      with:
        app-id: <your-github-app-id>
        app-private-key: <your-github-app-private-key>
        repositories: foo-repo bar-repo
```

## Inputs

| Name | Description | Default | Required |
| :--- | :---------- | :------ | :------: |
| app-id | The ID of the GitHub App. | n/a | yes |
| app-private-key | The private key associated with the GitHub App. | n/a | no |
| app-private-key-file | The file path to the GitHub App's private key. | n/a | no |
| repositories | A space-separated list of repositories that the token grants access to. | n/a | no |

## Outputs

| Name | Description |
| :--- | :---------- |
| token | The installation access token for the specified GitHub App. |

<!-- actdocs end -->

## Permissions

N/A

## FAQ

N/A

## Related projects

- [revoke-github-token-action](https://github.com/tmknom/revoke-github-token-action): Revoke an installation access token using GitHub Apps for GitHub Actions.
- [private-generate-github-token-action](https://github.com/tmknom/private-generate-github-token-action): Generate an installation access token for personal use.

## Release notes

See [GitHub Releases][releases].

[releases]: https://github.com/tmknom/generate-github-token-action/releases
