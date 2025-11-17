# Contributing to IETF Tools projects

:+1::tada: First off, thanks for taking the time to contribute! :tada::+1:

Before going any further, make sure you read the [code of conduct](CODE_OF_CONDUCT.md).

> [!NOTE]  
> This guide uses `PROJECT-NAME` as a placeholder in code / command examples. Replace it with the project name you're working on.

#### Table Of Contents

- [Workflow Overview](#workflow-overview)
- [Creating a Fork](#creating-a-fork)
- [Cloning a Fork](#cloning-a-fork)
  - [Using Git Command Line](#using-git-command-line)
  - [Using GitHub Desktop / GitKraken](#using-github-desktop--gitkraken)
  - [Using GitHub CLI](#using-github-cli)
- [Create a Local Branch](#create-a-local-branch)
- [Creating a Commit](#creating-a-commit)
  - [From your editor / GUI tool](#from-your-editor--gui-tool)
  - [From the command line](#from-the-command-line)
- [Push Commits](#push-commits)
- [Create a Pull Request](#create-a-pull-request)
  - [PR Checkout Tip](#pr-checkout-tip)
- [Sync your Fork](#sync-your-fork)
  - [Syncing with uncommitted changes](#syncing-with-uncommitted-changes)
- [Styleguides](#styleguides)
  - [Git Commit Messages](#git-commit-messages)
  - [Javascript](#javascript)
  - [Python](#python)
- [Release Procedure](#release-procedure)
  - [Auto Semver Deploy *(recommended)*](#auto-semver-deploy-recommended)
  - [Manual Release Deploy](#manual-release-deploy)
  - [NPM Packages](#npm-packages)
  - [Python Packages](#python-packages)
- [Blocked accounts](#blocked-accounts)

## Workflow Overview

Projects use the **Git Feature Workflow** model.

It consists of a **Main** branch which reflects the latest development state. New features / bug fixes are added to this branch until a new release is created, which creates a snapshot of the current branch state and performs deployment tasks.

A typical development workflow:

1. First, [create a fork](#creating-a-fork) of the repository and then [clone the fork](#cloning-a-fork) to your local machine.
2. [Create a new branch](#create-a-local-branch), based on the main branch, for the feature / fix you are to work on.
3. [Add one or more commits](#creating-a-commit) to this feature/fix branch.
4. [Push the commits](#push-commits) to the remote fork.
5. [Create a pull request (PR)](#create-a-pull-request) to request your feature branch from your fork to be merged to the source repository `main` branch.
6. The PR is reviewed by the lead developer / other developers, automated tests / checks are run to catch any errors and if accepted, the PR is merged with the `main` branch.
7. [Fast-forward (sync)](#sync-your-fork) your forked main branch to include the latest changes made by all developers.
8. Repeat this workflow from step 2.

![](https://github.com/ietf-tools/common/raw/main/assets/docs/workflow-diagram.jpg)

## Creating a Fork

As a general rule, work is never done directly on the project repository. You instead [create a fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) of the project. Creating a "fork" is producing a personal copy of the project. Forks act as a sort of bridge between the original repository and your personal copy.

1. Navigate to https://github.com/ietf-tools/PROJECT-NAME
2. Click the **Fork** button. *You may be prompted to select where the fork should be created, in which case you should select your personal GitHub account.*

![](https://github.com/ietf-tools/common/raw/main/assets/docs/fork-button.jpg)

Your personal fork contains all the branches / contents of the original repository as it was at the exact moment you created the fork. You are free to create new branches or modify existing ones on your personal fork, as it won't affect the original repository.

Note that forks live on GitHub and not locally on your personal machine. To get a copy locally, we need to clone the fork...

## Cloning a Fork

Right now, you have a fork of the project repository, but you don't have the files in that repository locally on your computer.

After forking the project repository, you should have landed on your personal forked copy. If that's not the case, make sure you are on the fork (e.g. `john-doe/PROJECT-NAME` and not the original repository `ietf-tools/PROJECT-NAME`).

Above the list of files, click the **Code** button. A clone dialog will appear.

![](https://github.com/ietf-tools/common/raw/main/assets/docs/code-button.png)

There are several ways to clone a repository, depending on your personal preferences. Let's go through them...

> [!IMPORTANT]  
> In all cases, you must have **git** already installed on your system.

- [Using Git Command Line](#using-git-command-line)
- [Using GitHub Desktop / GitKraken](#using-github-desktop--gitkraken)
- [Using GitHub CLI](#using-github-cli)

### Using Git Command Line

1. Copy the URL in the **Clone with HTTPS** dialog. 
2. In a terminal window, navigate to where you want to work. Subfolders will be created for each project you clone. **DO NOT** create empty folders for projects to be cloned. This is done automatically by git.
3. Type `git clone` and then paste the URL you just copied, e.g.:
```sh
git clone https://github.com/YOUR-USERNAME/PROJECT-NAME
```
4. Press **Enter**. Your local clone will be created in a subfolder named after the project.

### Using GitHub Desktop / GitKraken

There are several GUI tools which simplify your interaction with git:

- [GitHub Desktop](https://desktop.github.com/) *(macOS / Windows)*
- [GitKraken](https://www.gitkraken.com/) *(Linux / macOS / Windows)*
- [Sourcetree](https://www.sourcetreeapp.com/) *(macOS / Windows)*

If using **GitHub Desktop**, you can simply click **Open with GitHub Desktop** in the clone dialog.

For other tools, you must either manually browse to your forked repository or paste the HTTPS URL from the clone dialog.

### Using GitHub CLI

The GitHub CLI offers tight integration with GitHub.

1. Install the [GitHub CLI](https://cli.github.com/).
2. In a terminal window, navigate to where you want to work. Subfolders will be created for each project you clone. **DO NOT** create empty folders for projects to be cloned. This is done automatically by git.
3. Type `gh repo clone` followed by `YOUR-USERNAME/PROJECT-NAME` (replacing YOUR-USERNAME with your GitHub username and PROJECT-NAME with the project), e.g.:
```sh
gh repo clone john-doe/rfc2html
```
4. Press **Enter**. Your local clone will be created in a subfolder named after the project.

## Create a Local Branch

While you could *technically* work directly on the main branch, it is best practice to create a branch for the feature / fix you are working on. It also makes it much easier to fast-forward your forks main branch to the match the source repository.

1. From a terminal window, nagivate to the project directory you cloned earlier.
2. First, make sure you are on the `main` branch.:
```sh
git checkout main
```
3. Let's create a branch named `feature-1` based on the `main` branch:
```sh
git checkout -b feature-1
```
4. Press **Enter**. A new branch will be created, being an exact copy of the main branch.

You are now ready to work on your feature / fix in your favorite editor.

## Creating a Commit

Once you are ready to commit the changes you made to the project code, it's time to stage the modifications.

### From your editor / GUI tool

It's generally easier to use either your editor (assuming it has git capabilities) or to use a git GUI tool. This ensures you're not missing any new untracked files. Select the changes / new files you wish to include in the commit, enter a meaningful short description of the change (see [Git Commit Messages](#git-commit-messages) section) and create a commit.

### From the command line

If you wish to use the command line instead, you can view the current state of your local repository using the [git status](https://git-scm.com/docs/git-status) command:
```sh
git status
```

To stage a modification, use the [git add](https://git-scm.com/docs/git-add) command:
```sh
git add some-file.py
```

Finally, create the commit by running the [git commit](https://git-scm.com/docs/git-commit) command:
```sh
git commit
```
This will launch a text editor prompting you for a commit message. Enter a meaningful short description of the change (see [Git Commit Messages](#git-commit-messages) section) and save.

> [!TIP]  
> There are several command parameters you can use to quickly add all modifications or execute several actions at once. Refer to the documentation for each command above.

## Push Commits

You can now push your commits to your forked repository. This will add the commits you created locally to the feature/fix branch on the remote forked repository.

Look for the **Push** button in your editor / GUI tool.

If you prefer to use the command line, you would use the [git push](https://git-scm.com/docs/git-push) command:
```sh
git push origin feature-1
```

> [!TIP]  
> If the feature branch doesn't exist on the remote fork, it will automatically be created.

## Create a Pull Request

When your feature / fix is ready to be merged with the source repository `main` branch, it's time to create a **Pull Request (PR)**.

On GitHub, navigate to your branch (in your forked repository). A yellow banner will invite you to **Compare & pull request**. You can also click the **Contribute** dropdown to initiate a PR.

![](https://github.com/ietf-tools/common/raw/main/assets/docs/pr-buttons.png)

Make sure the base repository is set to `ietf-tools/PROJECT-NAME` with the branch `main` (this is the destination):

![](https://github.com/ietf-tools/common/raw/main/assets/docs/pr-form.png)

Enter a title and description of what your PR includes and click **Create pull request** when ready.

Your PR will then be reviewed by the lead developer / other developers. Automated tests will also run on your code to catch any potential errors.

Once approved and merged, your changes will appear in the `main` branch. It's now time to fast-forward your fork to the source repository. This ensures your fork main branch is in sync with the source main branch...

### PR Checkout Tip

It's possible to checkout the source code as it would be if the PR was merged with the target branch:

```sh
git checkout -B <NEW_BRANCH> refs/pull/<PR_NUMBER>/merge
```

- Replace `<NEW_BRANCH>` with a some name that won't conflict with your existing branches.
- Replace `<PR_NUMBER>` with the ID of the PR.

## Sync your Fork

Your fork `main` branch is now behind the source `main` branch. To fast-forward it to the latest changes, click the **Fetch upstream** button:

![](https://github.com/ietf-tools/common/raw/main/assets/docs/sync-branch.png)

Note that you also need to fast-forward your **local machine** `main` branch. This can again be done quickly from your editor / GUI tool. If you're using the command line, run these commands:

```sh
git checkout main
git merge --ff-only origin/main
```

> [!TIP]  
> While you could use the `git pull` command to achieve the same thing, this ensures that only a fast-forward operation will be executed and not a merge (which is most likely not what you want). You can read more about the different ways of pulling the latest changes via [git merge](https://git-scm.com/docs/git-merge), [git pull](https://git-scm.com/docs/git-pull) and [git rebase](https://git-scm.com/docs/git-rebase).

### Syncing with uncommitted changes

In some cases, you may need to get the latest changes while you're still working on your local branch.

Some tools like GitKraken automates this process and will even handle the stashing process if necessary.

If you prefer to use the command line:

1. You must first [git stash](https://git-scm.com/docs/git-stash) any uncommitted changes:
    ```sh
    git stash
    ```
    This will save the current state of your branch so that it can be re-applied later.

2. Run the [git rebase](https://git-scm.com/docs/git-rebase) command to fast-forward your branch to the latest commit from `main` and then apply all your new commits on top of it:
    ```sh
    git rebase main
    ```
    You can add the `-i` flag to the above command to trigger an interactive rebase session. Instead of blindly moving all of the commits to the new base, interactive rebasing gives you the opportunity to alter individual commits in the process.

3. Use the [git stash pop](https://git-scm.com/docs/git-stash) :musical_note: command to restore any changes you previously stashed:
    ```sh
    git stash pop
    ```

> [!WARNING]  
> Note that you should **never** rebase once you've pushed commits to the source repository. After a PR, **always** fast-forward your forked main branch to match the source one and create a new feature branch from it. Continuing directly from a previously merged branch will result in duplicated commits when you try to push or create a PR.

## Styleguides

### Git Commit Messages

* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* Limit the first line *(title)* to 72 characters or less
* Reference issues and pull requests liberally after the first line
* When only changing documentation, include `[ci skip]` in the commit message *(after the first line (title) when possible)*
* Start the commit message with one of the following keywords (see [Conventional Commits](https://www.conventionalcommits.org/) specification):
  * `chore`: Tool changes, configuration changes and changes to things that do not actually go into production
  * `ci:` Changes that affect the build system or external dependencies
  * `docs:` Documentation only changes
  * `feat:` A new feature
  * `fix:` A bug fix
  * `perf:` A code change that improves performance
  * `refactor:` A code change that neither fixes a bug nor adds a feature
  * `style:` Changes that do not affect the meaning of the code *(white-space, formatting, missing semi-colons, etc)*
  * `test:` Adding missing tests or correcting existing tests
* Optionally mention the scope (affected section / module of the project) of the change, in parentheses, between the type keyword and the colon.

#### Examples

- Commit message for a fix:
  ```
  fix: sanitize input value in module xyz
  ```
- Commit message for a feature with a scope:
  ```
  feat(meetings): add new agenda section to the meetings page
  ```
- Commit message for a documentation change with a skip build flag:
  ```
  docs: add usage information to the README
  
  [skip ci]
  ```

### Javascript

#### JS Coding Style

[StandardJS](https://standardjs.com/) is the style guide used for projects.

[![JavaScript Style Guide](https://cdn.rawgit.com/standard/standard/master/badge.svg)](https://github.com/standard/standard)

ESLint and EditorConfig configuration files are present in the project root. Most editors can automatically enforce these [rules](https://standardjs.com/rules.html) and even format your code accordingly as you type.

These rules apply whether the code is inside a `.js` file or as part of a `.vue` / `.html` file.

Refer to the [rules](https://standardjs.com/rules.html) for a complete list with examples. However, here are some of the major ones:

* No semi-colons! :no_entry_sign:
* Use 2 spaces for indentation
* Use single quotes for strings (except to avoid escaping)
* Use camelCase when naming variables and functions
* Always use `===` instead of `==` (unless you **specifically** need to check for `null || undefined`)
* No unused variables
* Keep `else` statements on the same line as their curly braces
* No trailing commas
* Files must end with a newline *(only for new .js / .vue files. See the Python directives below for other file types.)*

Finally, avoid using `var` to declare variables. You should instead use `const` and `let`. `var` unnecessarily pollutes the global scope and there's almost no use-case where it should be used.

#### JS Tests

For applications that require browser testing, the [Playwright](https://playwright.dev/) framework should be used.
These tests are to be located under the `playwright/` directory.

For standard testing, the [Vitest](https://vitest.dev/) framework should be used.

### Python

#### Python Coding Style

* Follow the coding style in the piece of code you are working on. Don't re-format code you're not working on to fit your preferred style. As a whole, the piece of code you're working on will be more readable if the style is consistent, even if it's not your style.

* For Python code, PEP 8 is the style guide. Please adhere to it, except when in conflict with the bullet above.

* Don't change whitespace in files you are working on, (except for in the code you're actually adding/changing, of course); and don't let your editor do end-of-line space stripping on saving. Gratuitous whitespace changes may give commit logs and diffs an appearance of there being a lot of changes, and your actual code change can be buried in all the whitespace-change noise.

* Now and then, code clean-up projects are run. During those, it can be the right thing to do whitespace clean-up, coding style alignment, moving code around in order to have it live in a more appropriate place, etc. The point in *those* cases is that when you do that kind of work, it is labelled as such, and actual code changes are not to be inserted in style and whitespace-change commits. If you are not in a clean-up project, don't move code around if you're not actually doing work on it.

* If you are modifying existing code, consider whether you're bending it out of shape in order to support your needs. If you're bending it too much out of shape, consider refactoring. Always try to leave code you change in a better shape than you found it.

#### Python Tests

* Reasonably comprehensive test suites should be written and committed to the project repository.
* Projects written in Python, should use Python's doctests or unittest framework.
* Please shoot for a test suite with at least 80% code coverage for new code, as measured by the built-in coverage tests for the project or standalone use of coverage.py for other Python projects. For non-Python projects, use the most appropriate test coverage measurement tool.
* Aim for 100% test suite template coverage for new templates.
* When a reported functional bug is being addressed, a test must be written or updated to fail while the bug is present and succeed when it has been fixed, and made part of the bugfix. This is not applicable for minor functional bugs, typos or template changes.

## Release Procedure

All projects follow a standard release procedure. There are 2 methods to create a release:

### Auto Semver Deploy *(recommended)*

1. Go the **Actions** tab.
2. Select the **Publish Python Package** workflow.
3. Click on the **Run workflow** button.
4. Check the **Create Production Release** checkbox and click **Run workflow**.
5. Wait for the workflow build to complete.
6. Follow the additional instructions depending on the project type below:
  - [NPM Packages](#npm-packages)
  - [Python Packages](#python-packages)

### Manual Release Deploy

1. Create a new GitHub Release by clicking the **Draft a new release** button on the project **Releases** page.
2. Create a new tag based on the **main** branch using a version respecting the [semantic versioning](https://semver.org/) specs. The tag should start with `v` (e.g. `v3.12.2`):

  ![](https://github.com/ietf-tools/common/raw/main/assets/docs/release-create-tag.png)

3. Enter the release title using the same name as the tag to be published. (e.g. `v3.12.2` in the above example)
4. In the description, insert `*pending*`. The contents will be replaced during the build process with the proper changelog.
  > *It's best to not leave this field empty as the default is to use the last commit message, which might contain a `[skip ci]` mention and prevent the release build from starting.*
5. Check the **This is a pre-release** box. This will mark the release as pre-release and prevent it to be displayed as the latest release until the build is completed. This flag will automatically be removed during the build process.
6. Finally, click **Publish release**.
7. Wait for the workflow build to complete.
8. Follow the additional instructions depending on the project type below:
  - [NPM Packages](#npm-packages)
  - [Python Packages](#python-packages)

### NPM Packages

*No additional steps needed. The package is published automatically to NPM during the release build.*

### Python Packages

*No additional steps needed. The package is published automatically to PyPI during the release build.*

## Blocked accounts

Any accounts that engaged in vandalism or bot-like behaviour in ietf-tools projects will be blocked. If your account is blocked and you want to unblock it, contact [support@ietf.org](mailto:support@ietf.org).
