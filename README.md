# Block Autosquash and Drop! Commits Action



A Github Action to prevent merging pull requests containing [autosquash](https://git-scm.com/docs/git-rebase#git-rebase---autosquash) commit messages.

## How it works

If any commit message in the pull request starts with `fixup!`, `squash!` and `drop!` the check status will be set to `error`.

>⚠️ GitHub's API only returns the first 250 commits of a PR so if you're working on a really large PR your fixup commits might not be detected.

## Usage

```yaml
on: pull_request

name: Pull Requests

jobs:
  message-check:
    name: Block Autosquash Commits

    runs-on: ubuntu-latest

    steps:
      - name: Block Autosquash Commits
        uses: skrobul/block-autosquash-commits-action@v2.1.1
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
```

You'll also need to add a [required status check](https://help.github.com/en/articles/enabling-required-status-checks) rule for your action to block merging if it detects any `fixup!` or `squash!` commits.

### Control Permissions

If your repository is using [control permissions](https://github.blog/changelog/2021-04-20-github-actions-control-permissions-for-github_token/) you'll need to set `pull-request: read` on either the workflow or the job.

