# action-open-pr-in-official-unmanic-repo
A GitHub action that automatically opens a PR against an Unmanic plugin repository hosted on GitHub.

This action will create a new branch prefixed with `pr-`. The branch will be pushed to the remote repository specified by `dst_repo`.
After pushing the `pr-` branch, this action will then open a PR against the remote repository specified by `pr_repo`.
If the PR is already open, this action will simply be updating that PR with the latest changes.

All PRs opened by this action will follow a format:
- **TITLE:**    `[PLUGIN_ID] vPLUGIN_VERSION`
- **BODY:**     `PR automatically generated from plugin source workflow`

## Inputs

### `dst_repo` 

**Required** - The repository to push to. Should be a fork of the official Unmanic plugin repository.

### `pr_repo` 

**Optional** - The repository to open the PR against. Can be either a fork or the official Unmanic plugin repository [Default `Unmanic/unmanic-plugins`].

### `pr_repo_branch_name` 

**Optional** - The name of the branch to open the PR against [Default `official`].

### `github_token` 

**Required** - A personal access token (PAT) used to push the PR branch and open the PR against the `pr_repo`.

> [!IMPORTANT]
> This PAT requires the `workflow` scope. For this reason we cannot use the automatically provided `github.token` in this task.

## Example usages

Generate a PR to the official Unmanic plugin repo
```yaml
    - name: Generate PR for official repo
      uses: Josh5/action-open-pr-in-official-unmanic-repo@master
      with:
        dst_repo: Josh5/unmanic-plugins
        pr_repo: Unmanic/unmanic-plugins
        pr_repo_branch_name: official
        github_token: ${{ secrets.GH_TOKEN }}
```

Generate a PR to my own fork of the Unmanic plugin repo
```yaml
    - name: Generate PR for official repo
      uses: Josh5/action-open-pr-in-official-unmanic-repo@master
      with:
        dst_repo: Josh5/unmanic-plugins
        pr_repo: Josh5/unmanic-plugins
        pr_repo_branch_name: master
        github_token: ${{ secrets.GH_TOKEN }}
```
