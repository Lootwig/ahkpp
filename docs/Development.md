# Development

This document covers the development process, from writing code to publishing a new version.

## Writing

1. Write your change on any branch other than `main`
1. Merge each change to `main` via a squash-commit PR

## Testing

-   Test all added commands
-   Perform the formatting tests
-   If the README was modified, confirm README appears as intended

### Automated tests

1. Open the Debug console panel (`Ctrl + Shift + Y`)
1. Run the tests (`debug test`)
    1. Select `Test Extension` in the Debug side bar
    1. Begin Debugging (`F5` or press the play button)

The tests should run automatically, and you should see passing output in the Debug console within a few seconds.

> Learn more about debugging at the [VS Code Debugging Guide](https://code.visualstudio.com/Docs/editor/debugging).

## Starting a release

1.  Update the changelog.
1.  Open a draft PR to merge to `main`. The title of the PR should be e.g. `v2.8.2`, lowercase 'v'. The PR description should contain the changelog entry.
1.  Fix any remaining issues with the code (but only make changes already logged in the changelog). Use the draft PR to easily detect issues.
1.  Bump the version in `package.json`. The message of the commit should be e.g. `v2.8.2`.
1.  Push the changes.
1.  Merge the PR. The body of the commit message should be the changelog entry.
1.  Checkout `main`
1.  Package the new version using `vsce package`.
1.  Install the new version:
    1. Select the newly-created `.vsix` file.
    1. Open the context menu (right-click).
    1. Select `Install Extension VSIX`.
    1. Reload the window.
1.  Perform final pre-release tests.
    -   If tests fail, there are two choices:
        1. Delay the release until the tests pass (preferred choice)
            > Changes can be made on the same release branch, same package version
        1. Create issues for the newly-introduced failures before releasing, then publish the release anyway

### Publishing

1. Tag the release
    1. Delete the release branch in local
    1. `git checkout main`
    1. `git tag v<major>.<minor>.<patch>`
    1. `git push origin v<major>.<minor>.<patch>`
    1. [Create a new release for this tag](https://github.com/mark-wiemer/vscode-autohotkey-plus-plus/tags)
        1. Release title: Same as in [Changelog.md](../Changelog.md)
        1. Description: Same as in changelog
        1. Attach binary
        1. Publish release
1. Publish the release through [Visual Studio Marketplace](https://marketplace.visualstudio.com/manage/publishers/mark-wiemer)
    1. Select the ellipsis `Actions` icon and select `Update`.
    1. Upload the `.vsix` release file packaged in a previous step.

The release is usually available within 5 minutes of uploading.