# Git Hooks 🚀

## Difference between pre-commit and pre-receive

The `pre-commit` and `pre-receive` hooks in Git are both script files that can be executed before certain Git operations. However, they are triggered at different points in the Git workflow and serve different purposes:

1. Pre-commit hook:
    - Trigger: The `pre-commit` hook is triggered before creating a commit.
    - Purpose: It allows you to perform checks or validations on the proposed commit before it is actually created. You can use this hook to enforce coding standards, run tests, or perform any other checks that ensure the quality and integrity of the commit. If the pre-commit hook script exits with a non-zero status, the commit process is aborted.
    - Local scope: The pre-commit hook runs only on the local repository, affecting only the developer who initiated the commit.

2. Pre-receive hook:
    - Trigger: The `pre-receive` hook is triggered on the remote repository when receiving pushed commits.
    - Purpose: It allows you to enforce specific rules or checks on the incoming commits before they are accepted and applied to the repository. This hook is commonly used for enforcing branch policies, access controls, or any other custom rules that need to be validated before accepting the pushed changes.
    - Remote scope: The pre-receive hook runs on the remote repository, affecting all users who push changes to that repository. It ensures that certain criteria are met for the entire set of pushed commits.

In summary, the main difference between the `pre-commit` and `pre-receive` hooks is their timing and scope. The pre-commit hook runs locally and is triggered before a commit is created, allowing checks on individual commits. The pre-receive hook runs on the remote repository and is triggered before accepting pushed commits, allowing checks on a set of commits pushed by multiple users.

## How to enforce branch naming conventions ?

- you can use `pre-receive` hook in self-hosted git environments. It won't work in managed github service.

```bash
#!/bin/bash

while read oldrev newrev refname; do
    branch=$(basename "$refname")

    # Check if the branch name starts with one of the allowed prefixes
    if [[ $branch != feature/* && $branch != bugfix/* && $branch != hotfix/* ]]; then
        echo "Error: Branch names must start with 'feature/', 'bugfix/', or 'hotfix/'."
        exit 1
    fi
done

exit 0
```

## How to make sure only certain users push to master and release branches ?

## How to enforce commit message guidelines ?

## How to run code quality checks while pushing branch ?

## Enforcing merge or rebase policies ?

- You can enforce specific rules for merging or rebasing branches. For example, you can require that all merges are performed with the "--no-ff" (no fast-forward) flag to preserve branch history. Alternatively, you can enforce rebasing of feature branches onto the latest changes from the base branch before accepting the push.