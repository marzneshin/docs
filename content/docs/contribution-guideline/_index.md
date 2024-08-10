---
title: Contribution Guideline
weight: 4
---

This series of documents is dedicated to people who want to understand
the codebase, architecture, and the contribution guideline.

### Reporting issues

Include the following information in your post:

- Describe what you expected to happen.
- Describe what actually happened. Include server logs or any error that browser shows.
- If possible, post your xray json config file and what you have set in env (by censoring critical information).
- Also tell the version of Marzneshin, Xray and docker (if you use docker) you are using.

{{< callout type="warning" >}}

Please refrain from opening issues solely to **ask a question**. Instead, use one of the following methods:

- Ask in our Telegram group: [@marzneshins](https://t.me/marzneshins)
- Use our [GitHub Discussions](https://github.com/marzneshin/marzneshin/discussions) long-term discussions or more complex questions.

{{< /callout >}}

### Submitting a Pull Request

If there is not an open issue for what you want to submit, prefer opening one for discussion before working on a PR. You
can work on any issue that doesn't have an open PR linked to it or a maintainer assigned to it. These show up in the
sidebar. No need to ask if you can work on an issue that interests you.

{{< callout type="warning" >}}

Your PR name must follow the angular [commit conventions](https://www.conventionalcommits.org) `action(scope): desc`.
Otherwise your PR will be marked as broken and does not pass CI pipeline.

{{< /callout >}}

#### CI

There are several actions quality checking your code. Make sure you pass all criteria's, especially **Sonar**.

#### Branches

Make sure to create a branch off your master branch, and then submit a PR to our master branch.

The naming convetion for branches is `action/scope` plus the the number of issue if
there is one related. E.g. `feat/users-filter-admin`, `fix/nodes-settings-tab-123`.
