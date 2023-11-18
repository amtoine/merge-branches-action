# merge-branches-action
A GitHub action to merge branches together in a CI.

## Examples
- a simple workflow to merge the `main` branch into a `nightly` branch whenever there is a new
commit pushed to the `main` branch from a closed PR. This action will push and show the worktree.
```yml
name: 🌃 Sync main to nightly

on:
  pull_request:
    types: [closed]
    branches: [main]

permissions:
  contents: write

jobs:
  sync_on_merge:
    runs-on: ubuntu-latest
    if: github.event.pull_request.merged == true
    steps:
      - uses: actions/checkout@v3
        with:
          # Fetches all history for all tags and branches
          fetch-depth: 0
      - uses: amtoine/merge-branches-action@0.1.0
        with:
          do_push: true
          log_worktree: true
```
