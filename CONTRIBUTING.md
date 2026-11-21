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

For a change that affects the analysis or report, run these commands from the repository root on macOS with uv and Quarto installed.

```bash
uv sync --locked
QUARTO_PYTHON="$(pwd)/.venv/bin/python3" quarto render analysis/iris-species-prediction.qmd --to html
```

Open the rendered HTML and check that the sections, tables, and plots affected by your change still look right. For a documentation-only change, preview the Markdown and check edited links or commands.

## Open a pull request and request review

1. Open a pull request from your branch into `main`. Explain what changed, why, and how you checked it. If merging fully resolves an issue, add a closing reference such as `Closes #123` using the actual issue number.
2. Request review from at least one teammate. Reviewers should check that the change addresses the issue and that affected analysis or documentation still works. Leave specific, constructive feedback if something needs attention.
3. Discuss feedback in the pull request and push any revisions to the same branch. Once a teammate has reviewed the final changes and approved the pull request, a team member can merge it.

## Generative AI policy

You may use generative AI tools to brainstorm, understand concepts, debug problems, or help draft code and documentation, subject to any instructions for the specific assessment. Check the correctness and licensing of AI-assisted material, test changes that affect the analysis, and be ready to explain everything you submit. Keep confidential, personal, and sensitive information out of AI tools.

Team members are responsible for opening issues and pull requests, pushing changes, reviewing each other's work, and making final decisions about merging. Write issues, pull request descriptions, and review comments in your own words. You may use AI to help with translation or grammar.

Follow the [DSCI 522 generative AI policy](https://ubc-mds.github.io/DSCI_522_dsci-workflows_students/#use-of-generative-ai) for the full course requirements. Contributors must disclose any AI use in the pull request description, and the team summarizes it in the README’s AI use statement.
