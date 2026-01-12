# lefthook

This repo contains a collection of reusable [lefthook](https://lefthook.dev) configuration files for various languages and tools.

## Usage

In order to use any of the hooks in this repo, please do the following:

1. Install [lefthook](https://lefthook.dev).
2. In the root directory of your git repo, use `lefthook install` to create a `lefthook.yml` file.
3. Edit the file to include the hooks from this repo that you want:

    ```yaml
    remotes:
      - git_url: <https://github.com/AjayKMehta/lefthook.git>
          configs:
            - hooks/pre-commit/<hook1>
            - hooks/pre-commit/<hook2>
            - hooks/pre-push/<hook1>
    ```

    > :bulb: All the hooks are located in `hooks/<hook-type>/<hook>`.

4. Install dependencies for any hooks of interest (see next section for details).
5. Run `lefthook install` to install these hooks in your repo. You can use `lefthook check-install` and `lefthook dump` to verify everything is installed and configured correctly.

## Available Hooks

### [commit-msg](https://git-scm.com/docs/githooks#_commit_msg)

- [run-commitlint.yml](hooks\commit-msg\run-commitlint.yml): Requires [commitlint](https://github.com/conventional-changelog/commitlint) to be installed.
- [run-typos.yml](hooks\commit-msg\run-typos.yml): Uses [typos](https://github.com/crate-ci/typos) to spellcheck commit messages.

### [pre-commit](https://git-scm.com/docs/githooks#_pre_commit)

- [analyze-csharp.yml](hooks/pre-commit/analyze-csharp.yml): This uses `dotnet format` to run analyzers on staged C# files.
- [format-csharp.yml](hooks/pre-commit/format-csharp.yml): This uses `dotnet format` to check formatting of staged C# files.
- [lint-actions.yml](hooks/pre-commit/lint-actions.yml): This requires [actionlint](https://github.com/rhysd/actionlint) to be installed.
- [lint-docker.yml](hooks/pre-commit/lint-docker.yml): This requires [hadolint](https://github.com/hadolint/hadolint) to be installed.
- [lint-markdown.yml](hooks/pre-commit/lint-markdown.yml): This requires [markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2) to be installed.
- [lint-toml.yml](hooks/pre-commit/lint-toml.yml): This requires [taplo](https://github.com/tamasfe/taplo) to be installed.
- [lint-yaml.yml](hooks/pre-commit/lint-yaml.yml): This requires [yamllint](https://yamllint.readthedocs.io/en/stable/index.html) to be installed.

### [pre-push](https://git-scm.com/docs/githooks#_pre_push)

- [detect-secrets.yml](hooks/pre-push/detect-secrets.yml): This requires [gitleaks](https://github.com/gitleaks/gitleaks) to be installed.
- [test-dotnet.yml](hooks/pre-push/test-dotnet.yml):
  - This ensures .NET code builds and all tests run successfully.
  - You can override the default build configuration (`Release`) by adding this to your repo's `lefthook-local.yml`:

    ```yaml
    templates:
      build_config: <New value>
    ```

  > [!NOTE]
  > Assumes that there is a solution file at repo root.
