# Comment H5P library version action
Comments whether or not the H5P library version was updated

## Usage

This action needs to be triggered by pull_request, something like this:

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

| Name | Description | Default value | Required |
|---|---|---|---|
| `cancel-label` | Name of the label that blocks messages from being sent. | `non-functional` | false |
