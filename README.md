# generate-github-token-action

Generate a GitHub App installation access token in GitHub Actions.

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

This action does not require additional `GITHUB_TOKEN` permissions in the workflow file.
However, make sure your GitHub App has the necessary permissions configured.

## Why

GitHub Actions provides a built-in `GITHUB_TOKEN` for workflows,
but it has limited permissions and cannot be used outside the workflow.

Personal Access Tokens (PATs) offer broader access,
but they are tied to individual users, making them harder to manage and less secure in team environments.
Additionally, PATs do not expire automatically, posing security risks if not revoked manually.

GitHub Apps use **Installation Access Tokens**, which provide several key advantages:

- **Access beyond the repository where the workflow runs**:
  `GITHUB_TOKEN` is restricted to its own repository, but installation tokens allow access to other repositories as needed.
- **Short-lived tokens**:
  Unlike PATs, which remain valid until manually revoked, installation tokens expire automatically after a short period, reducing exposure in case of compromise.
- **Scoped repository access control**:
  A GitHub App’s permissions define the maximum set of accessible repositories,
  but installation tokens enable additional security by allowing you to specify only the required repositories at runtime.

This action automates the creation of **Installation Access Tokens** within GitHub Actions,
ensuring secure and seamless authentication.

## FAQ

### When do I need a GitHub App installation access token?

You need a GitHub App installation access token in the following cases:

- **Accessing permissions unavailable to `GITHUB_TOKEN`**: Some permissions (e.g., `workflows`) require a GitHub App token.
- **Approving pull requests created with `GITHUB_TOKEN`**: The creator of a pull request cannot approve it due to GitHub’s restrictions.
- **Creating pull requests in workflows that trigger `pull_request` events**: `GITHUB_TOKEN` does not trigger `pull_request` workflows when creating pull requests.

### Can I use this token to access multiple repositories?

Yes.
Provide a space-separated list of repositories in the `repositories` input.
The generated token grants access to all specified repositories.

### How long is the generated token valid?

GitHub installation access tokens expire after **one hour**.
Ensure your workflow regenerates the token as needed.

### How do I revoke an installation access token?

Installation access tokens expire automatically after one hour.
To revoke a token immediately, use [tmknom/revoke-github-token-action](https://github.com/tmknom/revoke-github-token-action).

### Do I need to configure `permissions` in my workflow?

No.
This action generates an installation access token with the required repository permissions,
so no additional `permissions` settings are needed in the workflow file.

### Can I provide the private key as a file path?

Yes.
You can provide the private key either as a string (`app-private-key`) or as a file path (`app-private-key-file`).
Using a file path is useful for managing secrets in the runner environment.

### Does this action protect sensitive data?

Yes.
This action automatically masks credentials to prevent exposure in logs.

### How do I configure GitHub App permissions?

To set up the required permissions for your GitHub App:

1. Go to `GitHub > Settings > Developer settings > GitHub Apps` and select your app.
2. Under `Permissions`, configure access levels for the required resources.
3. Save your changes and install the GitHub App on the necessary repositories or organizations.

For details, refer to [GitHub Documentation](https://docs.github.com/en/developers/apps/managing-github-apps#configuring-permissions-for-your-github-app).

> [!NOTE]
>
> Installation permissions may differ from the app's configured permissions.
> If the app requests additional permissions after installation, an administrator must approve them.

## Related Projects

- [revoke-github-token-action](https://github.com/tmknom/revoke-github-token-action): Revokes a GitHub App installation access token for GitHub Actions.
- [private-generate-github-token-action](https://github.com/tmknom/private-generate-github-token-action): Generates an installation access token for private use.

## Release Notes

See [GitHub Releases][releases].

[releases]: https://github.com/tmknom/generate-github-token-action/releases

## Administration

<details>
<summary>Click to expand repository administrator guide</summary>

This section provides guidance for repository administrators on configuration settings that are managed outside the codebase.

### Repository Secrets

The following secrets are stored in Repository Secrets for use in the [test workflow](/.github/workflows/test.yml):

- `TESTING_APP_ID`: The ID of the GitHub App `Testing for tmknom`.
- `TESTING_APP_PRIVATE_KEY`: The private key of the GitHub App `Testing for tmknom`.

These secrets authenticate the GitHub App.

> [!NOTE]
>
> `Testing for tmknom` is a GitHub App used exclusively for testing workflows.
> For more details, see the [internal-docs](https://github.com/tmknom/internal-docs) repository (private).

### Repository Variables

The following variables are stored in Repository Variables for use in the [test workflow](/.github/workflows/test.yml):

- `TESTING_REPOSITORY`: The private repository accessed by the test workflow.
- `TESTING_REPOSITORY_FIRST_COMMIT`: The hash of the initial commit in this repository.
- `TESTING_APP_PRIVATE_KEY_FINGERPRINT`: The fingerprint of the private key for the GitHub App `Testing for tmknom`.

These values are not sensitive.
Since Repository Secrets cannot be accessed after being set,
non-sensitive values are stored as Repository Variables for easier management.

</details>
