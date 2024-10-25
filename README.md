Sample repo showing how to leverage [commitlint](https://commitlint.js.org/) to enforce [conventional commits](https://www.conventionalcommits.org/).

## Local Setup

After first cloning the repo first run this command to setup your local git repository.

```shell
npm i
```

If you do not currently have npm installed, recommend using [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating).

## Prompt

For help authoring compliant commit messages, optionally create your commit messages using `commitlint/prompt`.

```shell
npm run commit
```

You will be prompted the enter the relevant pieces of your commit messages, then a commit will be made using a message built by your responses to the prompts.

## CI Linting

A GitHub workflow enforces linting on push, where the Action will fail if pushed commits don't adhere to conventional commit formatting.

In the situation where you have a failed check on a PR, rebase and force push to fix.

Pull the latest updates for the branch locally:

```shell
git pull origin <branch_name>
```

Initiate a `rebase`, where `n` is the number of commits in history you need to be able to edit:

```shell
git rebase -i HEAD~n
```

This will open an editor window.  For each commit you need to edit, change the prefix from `pick` to `reword` and save the edits.

You will then get prompted with subsequent edit windows for each commit you marked as reword.  Update the commit messages to a format adherent to conventional commits.  Then force push your updates.

```shell
git push -f origin <branch_name>
```

The commits on the PR branch will be updated, the commitlint CI will re-run, and should pass if the messages have been updated properly.
