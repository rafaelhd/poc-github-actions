# poc-github-actions

![title](/docs/github-actions.png)

This repository is a Github Actions POC with various examples regarding how to create workflows 🤖 

## Workflow YAML Basic Structure Explanation

```bash
name: Github action workflow name

on:
  push: # Run this workflow every time a new commit pushed to the repository
  pull_request:  # Run this workflow every time a new pull request is opened to the repository
  scheduled: # Run this workflow as a cron job
    - cron: "0 0 * * *"
  workflow_dispatch: # Run this workflow on demand (manually)

jobs: # All workflows need at list one job

  job-key: #First job
    name: Job Name
    runs-on: ubuntu-latest # Set the type of machine the workflow will run on
    steps: # Each job can be divided in many steps

      - name: Checkout code # Step name
        uses: actions/checkout@v2 # Action used on the step

      - name: Run Super-Linter # Another step name
        uses: github/super-linter@v3  # Action used on the step
        env:  # Environment variables used on the step
          DEFAULT_BRANCH: main
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Run specific commands # Another step name
        run: |
          ls -lha
          echo "This is a shell command"

```

## Examples

[![1 - Default Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/1-default-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/1-default-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to run some basic commands.

[![2 - Secret Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/2-secret-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/2-secret-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to run some basic commands using repository secrets.

[![3 - Python Script Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/3-python-script-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/3-python-script-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to execute a specific script [run.py](https://github.com/GuillaumeFalourd/poc-github-actions/blob/main/run.py) located on the repository.

[![4 - Remote Dispatch Action Initiator](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/4-dispatch-event-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/4-dispatch-event-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to dispatch an event to the [ritchie-formulas-scheduler-demo repository](https://github.com/GuillaumeFalourd/ritchie-formulas-scheduler-demo).

[![5 - Container Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/5-container-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/5-container-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) with a docker container where Ritchie CLI and Golang are installed, then check Ritchie CLI and Golang versions through commands.

[![6 - Docker Image Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/6-docker-image-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/6-docker-image-workflow.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) and a docker image `foundeo/minibox:latest`. It also specify an `entrypoint` (the command to run inside the container) and `args` (command line arguments to pass to the command specified in entrypoint). It is possible to omit the `entrypoint` if the container already species the entrypoint you want to use.

[![7 - Action workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/7-action-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/7-action-workflow.yml)

This workflow will run an Action each time a `PUSH` event occurs on the repository. This specific action runs a Ritchie CLI formula.

[![8 - Outputs workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/8-outputs-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/8-outputs-workflow.yml)

This workflow illustrates how to set outputs in a job to use them on another job. This specific workflow prints `Hello-World`.

[![9 - Artifacts workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/9-artifacts-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/9-artifacts-workflow.yml)

This workflow illustrates how to pass data between jobs in the same workflow. For more information, see the [actions/upload-artifact](https://github.com/actions/upload-artifact) and [download-artifact](https://github.com/actions/download-artifact) actions. The full math operation performed in this workflow example is `(3 + 7) x 9 = 90`.

[![10 - Environment workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/10-environment-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/10-environment-workflow.yml)

This workflow illustrates how to use `environment` variables from the whole workflow, a specific job, or a specific step.

[![11 - Input workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/11-input-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/11-input-workflow.yml)

This workflow illustrates how to use `input` variables on a `workflow_dispatch` event.

[![12 - Run Workflow](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/12-run-workflow.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/12-run-workflow.yml)

This workflow illustrates how to run a workflow once another specific one has been completed (with success or failure).

[![13 - Create Pull Request](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/13-create-pull-request.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/13-create-pull-request.yml)

This workflow uses [CRON](https://crontab.guru/#*_*_*_*_*) to automatically create a Pull Request committing updated files.

[![14 - Auto Merge](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/14-auto-merge.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/14-auto-merge.yml)

This workflow illustrates how to automatically merge a Pull Request with a specific label `automerge`.

[![15 - Push Dev](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/15-push-dev.yml/badge.svg)](https://github.com/GuillaumeFalourd/poc-github-actions/actions/workflows/15-push-dev.yml)

This workflow only run when a push is made to the `dev` branch.
Note that with this implementation, the workflow needs to be present on the specific branch as well (here `dev`).
