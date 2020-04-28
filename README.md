# GitHub Prettier Action

[![CodeFactor](https://www.codefactor.io/repository/github/TimVanMourik/pretty-quick-gh-action/badge/master)](https://www.codefactor.io/repository/github/TimVanMourik/pretty-quick-gh-action/overview/master)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)
[![License MIT](https://img.shields.io/github/license/TimVanMourik/pretty-quick-gh-action)](https://github.com/TimVanMourik/pretty-quick-gh-action/blob/master/LICENSE)
[![Latest Release](https://img.shields.io/github/v/release/TimVanMourik/pretty-quick-gh-action)](https://github.com/TimVanMourik/pretty-quick-gh-action/releases)
[![Contributors](https://img.shields.io/github/contributors-anon/TimVanMourik/pretty-quick-gh-action)](https://github.com/TimVanMourik/pretty-quick-gh-action/graphs/contributors)
[![Issues](https://img.shields.io/github/issues/TimVanMourik/pretty-quick-gh-action)](https://github.com/TimVanMourik/pretty-quick-gh-action/issues)

A GitHub action for styling files with [prettier](https://prettier.io) by means of [pretty-quick](https://github.com/azz/pretty-quick).

## Usage

### Parameters

| Parameter        |      Required      |      Default      | Description                                                                                               |
| ---------------- | :----------------: | :---------------: | --------------------------------------------------------------------------------------------------------- |
| dry              |        :x:         |       False       | Runs the action in dry mode. Files wont get changed and the action fails if there are unprettified files. |
| prettier_version |        :x:         |       False       | Specific prettier version (by default use latest)                                                         |
| prettier_options |        :x:         | `--write **/*.js` | Prettier options (by default it applies to the whole repository)                                          |
| commit_options   |        :x:         |         -         | Custom git commit options                                                                                 |
| commit_message   |        :x:         | Prettified Code!  | Custom git commit message                                                                                 |
| file_pattern     |        :x:         |        \*         | Custom git add file pattern                                                                               |
| branch           | :white_check_mark: |         -         | Always set this to `${{ github.head_ref }}` in order to work both with pull requests and push events      |

### Example Config

```yaml
name: Continuous Integration

# This action works with pull requests and pushes
on:
  pull_request:
  push:
    branches:
      - master

jobs:
  prettier:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          # Make sure the actual branch is checked out when running on pull requests
          ref: ${{ github.head_ref }}

      - name: Prettify code
        uses: TimVanMourik/pretty-quick-gh-action@v1.0
        with:
          # Push back to the same branch that was checked out
          branch: ${{ github.head_ref }}
          # This part is also where you can pass other options, for example:
          prettier_options: --write **/*.{js,md}
```

More documentation for writing a workflow can be found [here](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions).

## Issues

Please report all bugs and feature request using the [GitHub issues function](https://github.com/TimVanMourik/pretty-quick-gh-action/issues/new). Thanks!
