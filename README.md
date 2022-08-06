# `bash-action`


## Usage

> NodeJS is NOT Required

```yaml

jobs:
  pipeline:
    name: Node ${{ matrix.node-version }} on ${{ matrix.os }}
    runs-on: ${{ matrix.os }}

    strategy:
      fail-fast: false
      matrix:
        node-version: ['16.x']
        os: ['ubuntu-latest']
    name: Distributed Tasks
    steps:
      - uses: actions/checkout@v3

      - name: Run bash commands in parallel
        uses: sambacha/bash-action@v1
          id: tasks
        with:
          cmd1: echo $BASH_VERSION; date;
          cmd2: echo $BASH_VERSION; date;
```
