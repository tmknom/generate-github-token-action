# generate-github-token-action

Generate an installation access token using GitHub Apps for GitHub Actions.

<!-- actdocs start -->

## Description

This action generates a specified GitHub Apps installation access token.
The token is used to authenticate requests for repository access.
You can provide a space-separated list of repositories to grant access.

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
| app-id | GitHub App ID. | n/a | yes |
| app-private-key | GitHub App private key. | n/a | no |
| app-private-key-file | The file path to the GitHub App's private key. | n/a | no |
| repositories | A space-separated list of repositories to install the GitHub App on. | n/a | no |

## Outputs

| Name | Description |
| :--- | :---------- |
| token | GitHub installation access token |

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
