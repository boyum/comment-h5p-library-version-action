# Comment H5P library version action

Comments whether or not the H5P library version was updated

## Usage

This action needs to be triggered by `pull_request`, something like this:

```yml
on:
  pull_request:
    types:
      - opened # PR opens
      - labeled # PR is labeled
      - unlabeled # A label is removed from PR
      - synchronize # A commit is added - i.e. the PR's code is changed

jobs:
  check-h5p-library-version:
    name: Check H5P if library version is updated

    runs-on: ubuntu-latest

    steps:
      - name: Check library version
        uses: boyum/comment-h5p-library-version-action@v1
```

### Options

| Name                          | Description                                                                                                                                                                                                                                                     | Default value                                                                                                                                                                                                          | Required |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| `cancel-label`                | Name of the label that blocks messages from being sent.                                                                                                                                                                                                         | `non-functional`                                                                                                                                                                                                       | false    |
| `working-directory`           | The directory where the library.json file is located, relative to the Git project.                                                                                                                                                                              | `.`                                                                                                                                                                                                                    | false    |
| `version-changed-message`     | Message shown when the version number was changed. These special words will be replaced:<br>- `%OLD_VERSION%`: The project's version in the main branch<br>- `%NEW_VERSION%`: The project's version in the current PR                                           | :tada: The library version was updated from **%OLD_VERSION%** to **%NEW_VERSION%**.                                                                                                                                    | false    |
| `version-not-changed-message` | Message shown when the version number was changed. These special words will be replaced:<br>- `%OLD_VERSION%` — The project's version in the main branch<br> `%NEW_VERSION%` — The project's version in the current PR<br>- `%CANCEL_LABEL%` — The cancel label | :warning: The library version was not updated.<br>Add the label `%CANCEL_LABEL%` if this PR does not require a change of version numbers.<br><br>**Current version:** %NEW_VERSION%<br>**Main version:** %OLD_VERSION% | false    |
| `project-id`                  | An unique identifier used to distinguish between H5P projects in a monorepo. Only required in repositories with more than one H5P project.                                                                                                                      | `1`                                                                                                                                                                                                                    | false    |

## Development

### Releasing

#### Create release

Each release has its own Git _tag_. Do these steps to create a new release:

1. Create the tag: `git tag <version>`
1. Push the tag to origin: `git push origin <version>`

#### Update release

Because the release is now tagged to a specific commit, if you want to update the release, the tag has to be destroyed and re-created:

1. Delete the tag: `git push origin --delete <version>`
1. Delete the local tag: `git tag -d <version>`
1. Create the tag again: `git tag <version>`
1. Push the tag to origin: `git push origin <version>`
