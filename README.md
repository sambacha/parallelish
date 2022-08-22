# `parallelish`

> parallel `păr′ə-lĕl` -- ish

Use parallel to run a job multiple times in parallel in a single pipeline.

Multiple runners must exist, or a single runner must be configured to run multiple jobs concurrently.

Parallel jobs are named sequentially from job_name 1/N to job_name N/N.

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
        uses: sambacha/parallelish@v1
          id: tasks
        with:
          cmd1: echo $BASH_VERSION; date;
          cmd2: echo $BASH_VERSION; date;
```

```yaml
test:
  stage: test
  parallel: 3
  script:
    - echo "Node index - ${CI_NODE_INDEX}. Total amount - ${CI_NODE_TOTAL}"
    - cmd1: time cargo nextest run --workspace --partition count:${CI_NODE_INDEX}/${CI_NODE_TOTAL}
    - cmd2: time cargo nextest run --workspace --partition count:${CI_NODE_INDEX}/${CI_NODE_TOTAL}
```
