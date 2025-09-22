# Setup Unity YAML Merge Action

This action configures Git to use Unity's YAML merge tool (`unityyamlmerge`) for merging Unity scene and prefab files. It's a composite action that wraps [`srz-zumix/workspace-git-config-action`](https://github.com/srz-zumix/workspace-git-config-action).

## Inputs

| Name                      | Description                               | Required | Default |
| ------------------------- | ----------------------------------------- | -------- | ------- |
| `unity-project-path`      | Path to the Unity project directory.      | `false`  | `.`     |
| `unity-yaml-merge-path`   | Full path to the `UnityYAMLMerge` executable. | `true`   |         |

## Example Usage

Here is an example of how to use this action in your workflow. You need to provide the path to your `UnityYAMLMerge` tool. The path depends on your operating system and Unity installation location.

### on macOS

```yaml
name: CI

on: [push]

jobs:
  test:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Unity YAML Merge
        uses: ./ # Uses an action in the root directory
        with:
          unity-yaml-merge-path: /Applications/Unity/Hub/Editor/2022.3.10f1/Unity.app/Contents/Tools/UnityYAMLMerge

      # You can now run git commands that might involve merges.
      # For example, checking out a PR and trying to merge it.
      - name: Show git config
        run: git config --local --list
```

### on Windows

```yaml
name: CI

on: [push]

jobs:
  test:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Unity YAML Merge
        uses: ./ # Uses an action in the root directory
        with:
          unity-yaml-merge-path: 'C:\Program Files\Unity\Hub\Editor\2022.3.10f1\Editor\Data\Tools\UnityYAMLMerge.exe'

      # You can now run git commands that might involve merges.
      - name: Show git config
        run: git config --local --list
```