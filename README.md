# Code Freeze PR Blocker GitHub Action

This GitHub Action is designed to block pull requests (PRs) from being merged during a specified code freeze period. This ensures that no new code changes are introduced into the codebase during critical times, such as before a major release or during holidays.

## Features

- Automatically blocks PR merges during a specified date range.
- Customizable freeze period and bypass conditions.
- Provides clear messages to PR authors about the code freeze policy.

## Usage

To use this GitHub Action, add it to your repository's workflow file (e.g., `.github/workflows/block-prs.yml`).

### Example Workflow File

```yaml
name: Enforce Code Freeze

on:
  pull_request:
    types: [opened, edited, reopened]
  push:
    branches:
      - main

jobs:
  code-freeze-check:
    runs-on: ubuntu-latest
    steps:
      - name: Check Code Freeze Period
        run: |
          if [[ "$(date +%Y-%m-%d)" > "2024-11-22" && "$(date +%Y-%m-%d)" < "2024-12-01" ]]; then
            echo "Code freeze in effect. No changes allowed."
            exit 1
          fi
```

### Outputs

None.

## How It Works

1. The action checks if the current date falls within the specified freeze period.
2. If the date is within the freeze period, the action:
   - Fails the workflow.
   - Posts a comment on the PR, notifying the author about the code freeze.

## Customization

You can customize the action further by editing the script to include additional bypass rules, such as allowing PRs from certain users or for specific labels.

## Example Comment

If a PR is blocked, the action will post a comment like this:

> 🚫 Code Freeze Alert: Pull requests are not allowed to be merged between `2024-12-20` and `2025-01-05`. Please wait until the freeze period ends to merge this PR.

## Development

To modify this action, follow these steps:

1. Clone the repository.
2. Update the script in `.github/actions/block-prs`.
3. Test the changes locally or with a test repository.
4. Push updates to the main branch.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
