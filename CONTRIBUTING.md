# Contributing to Iris Species Prediction

We welcome fixes and suggestions for the Iris analysis, report, and documentation. Please follow the project's `CODE_OF_CONDUCT.md` when interacting with other contributors.

## Report a bug or suggest an improvement

Search the [existing issues](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-40-Iris-species-prediction/issues) first. If someone has already raised the same topic, add any new information to that issue. Otherwise, open an issue with a short, specific title.

- For a bug, include the command or steps that reproduce it, the expected and actual results, and any relevant error message or environment details. Remove private information before posting.
- For an improvement, explain what you would change and why it would help. Let the team know in the issue if you plan to work on it.

## Make and check a change

Group members should start from the latest `main` and create a separate, descriptive branch in the shared repository for each change. For example, a branch to fix a report caption could be created like this.

```bash
git switch main
git pull --ff-only origin main
git switch -c fix-report-caption
```

Keep the change focused on its issue. Check the output before committing, stage the intended files, and use a commit message that describes the change. Push to your branch and use a pull request to bring the changes into `main`.

For a documentation-only change, preview the Markdown and check any edited links or commands. For changes to the analysis or report, follow the report publishing steps below.

## Develop in the Docker container

Install [Positron](https://positron.posit.co/download.html) and follow the [README installation steps](README.md#installation) to set up Docker, check your SSH public key and Git configuration, and pull the project image. Positron includes Remote SSH.

1. In a terminal on your computer, run `docker compose up -d` from the repository root. Run `docker compose ps` and confirm that `analysis-env` is running.
2. In Positron, open the Command Palette (`Cmd+Shift+P` on macOS or `Ctrl+Shift+P` on Windows and Linux). Run **Remote SSH: Show Remote Menu**, choose **Connect to Host**, and enter `root@localhost:2222`. If prompted for the remote platform, select **Linux**. The first connection may take a few minutes while Positron sets up its remote server.
3. In the new window, check that the status bar shows `SSH: localhost:2222`. Choose **File → Open Folder** and open `/workspace`. Changes made there are saved to your local checkout.
4. Run **Python: Select Interpreter** and choose `/opt/venv/bin/python`. If the interpreter is missing from the list, choose **Enter interpreter path...** and enter `/opt/venv/bin/python`. In the Python Console, run `import sys; print(sys.executable)` and confirm that it prints `/opt/venv/bin/python`.
5. In the Positron Terminal, run `git config --get user.name` and `git config --get user.email`. Compose mounts your computer's `~/.gitconfig` into the container. If either value is missing, follow the Git configuration steps in the README on your computer and check again.

When you finish, close the remote Positron window and run `docker compose down` from the repository root on your computer.

### Troubleshoot the SSH connection

- **Connection refused or port already in use.** Run `docker compose ps` to check that `analysis-env` is running. If port `2222` is in use, free it or change the host port in your local Compose configuration and connect to that port.
- **SSH asks for a password.** Check that `~/.ssh/id_ed25519.pub` exists as a file and that your SSH client uses its matching private key. If Docker created an empty directory at the public key or `.gitconfig` path, stop the container, remove that empty directory, and follow the README setup steps before starting again.
- **Host key changed after replacing the container.** Once you have confirmed that you replaced the local container, run `ssh-keygen -R '[localhost]:2222'` on your computer and reconnect.
- **SSH rejects the mounted public key on Linux.** See the [course guide for Linux hosts](https://ubc-mds.github.io/DSCI_522_dsci-workflows_students/assignments/milestone2.html#positron-ssh).
- **GitHub authentication fails when pushing from the container.** Push from your computer's terminal using your existing GitHub credentials. The two terminals share the same checkout.

## Add or update a Python dependency

Start from an up-to-date `main` on a separate branch. In the Positron Terminal at `/workspace`, run `uv add 'PACKAGE==VERSION'`, replacing `PACKAGE` and `VERSION` with the dependency name and exact version. Review the changes to `pyproject.toml` and `uv.lock`, then commit both files together. Push the branch from your computer and set its upstream if this is the first push (`git push -u origin <branch-name>`).

A push that changes `uv.lock` triggers GitHub Actions to build and publish an updated Docker image for `linux/amd64` and `linux/arm64`. The workflow commits the new `sha-` image tag to `docker-compose.yml` on your branch. Once the workflow succeeds, run these commands from the repository root on your computer:

```bash
git pull --ff-only
docker compose pull
docker compose up -d
```

Reconnect Positron and test the change with the updated image before requesting review. After the PR merges and the publishing workflow succeeds on `main`, teammates should pull `main` and run `docker compose pull` again. Run `docker compose up -d` to use the new image for the next development session.

## Republish the report

From the repository root on your computer, re-render the report inside the container:

```bash
docker compose run --rm analysis-env uv run quarto render analysis/iris-species-prediction.qmd --to html
```

Once rendering succeeds, copy the self-contained HTML report to the file served by GitHub Pages:

```bash
cp analysis/iris-species-prediction.html docs/index.html
```

Open `docs/index.html` and check the updated sections, tables, and figures. Commit `analysis/iris-species-prediction.html` and `docs/index.html` with the relevant source changes, then push your branch and open a pull request. After the PR merges and GitHub Pages deploys, check that the [published report](README.md#published-report) shows the update. If rendering fails with a resource deadlock on macOS, follow the [README troubleshooting steps](README.md#troubleshooting-on-macos).

## Open a pull request and request review

1. Open a pull request from your branch into `main`. Explain what changed, why, and how you checked it. If merging fully resolves an issue, add a closing reference such as `Closes #123` using the actual issue number.
2. Request review from at least one teammate. Reviewers should check that the change addresses the issue and that affected analysis or documentation still works. Leave specific, constructive feedback if something needs attention.
3. Discuss feedback in the pull request and push any revisions to the same branch. Once a teammate has reviewed the final changes and approved the pull request, a team member can merge it.

## Generative AI policy

You may use generative AI tools to brainstorm, understand concepts, debug problems, or help draft code and documentation, subject to any instructions for the specific assessment. Check the correctness and licensing of AI-assisted material, test changes that affect the analysis, and be ready to explain everything you submit. Keep confidential, personal, and sensitive information out of AI tools.

Team members are responsible for opening issues and pull requests, pushing changes, reviewing each other's work, and making final decisions about merging. Write issues, pull request descriptions, and review comments in your own words. You may use AI to help with translation or grammar.

Follow the [DSCI 522 generative AI policy](https://ubc-mds.github.io/DSCI_522_dsci-workflows_students/#use-of-generative-ai) for the full course requirements. Contributors must disclose any AI use in the pull request description, and the team summarizes it in the README’s AI use statement.
