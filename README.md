# simple_ci_app
Simple app that utilizes github actions for CI and CD

## TOPIC / TASKS
* Notes GitHub components <a href="#github-comps">#</a>
* Writing workflows <a href="#write-workflows">#</a>
* Building and testing pull requests
* Deploying your application every time a release
* Adding a label whenever a new issue is opened

## NOTES GITHUB COMPS <span id="github-comps">#</span>
GitHub actions a triggered when an event occurs in your repo such as pull request being opened or issue being created.

- WORKFLOWS: This is a configurable automated proces that will run one or more jobs. Workflows are defined by a `YAML` file checked in your repo and will run automatic or manually when an event is triggered or defined schedule. All workflows are found in `./github/workflows` directory.

- EVENTS: This is a specific activity that triggers a workflow run.

- JOBS: A job is a set of steps in a workflow that run on the same runner. Example: A step to execute test and another to install dependencies. Each step depend on each other and run in sequencial order.

- ACTIONS: This is a custom app for GitHub action platform for perform frequently repeated tasks. Action can pull git repo from GitHub, set the correct toolchain for your build env ro setup the authentication to your cloud provider

- RUNNERS: This is a server that runs your workflow when triggered. Each runner can runs a job in sync. GitHub provides runners for all OS.
You can also [host your own runner](https://docs.github.com/en/actions/hosting-your-own-runners)

## WRITING WORKFLOWS <span id="write-workflows">#</span>
- uSING WORKFLOW TEMPLATES:
    GitHub provides reconfigured workflow templates that you can use as-is to create or customise your workflow. GitHub scans your repo to determine workflow you will need.

### PREREQUISIES:
- You have at least a basic knowledge of how to use GitHub. For quickstart on gituh 
    - [Quickstart for repos](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories)

    - [About Branches](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)

    - [About pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
- You have a repo on GitHub where you can add files
- You have access to GitHub actions. [more](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)

## STEP IN CREATING GITHUB ACTIONS
* Create `./github/workflows` directory the root of your repo
* Create a new files in the directory `<filename>.yml`, Replace `<filename>` with your filename. Example `github-action-demo.yml`

Note!!
```
For GitHub to discover any GitHub Actions workflows in your repository, you must save the workflow files in a directory called .github/workflows.

You can give the workflow file any name you like, but you must use .yml or .yaml as the file name extension. YAML is a markup language that's commonly used for configuration files.
```
* Paste the following code you your <filename>.yml
```yml
name: Simple CI Demo
run-name: ${{github.actor}} is testing out GitHub Actions 
on: [push]

jobs:
    Explore-GitHub-Actions:
        runs-on: ubuntu-latest
        steps:
            - run: echo "The job was automatically triggered by a ${{github.event_name}} event"
            - run: echo "This job is running on ${{runner.os}} server hosted by GitHub"
            - run: echo "The name of the branch is ${{github.ref}} and your repo is ${{github.repository}}"
            - name: Check out repository code
              uses: actions/checkout@v4
            - name: List files in the repository
              run: |
                ls ${{github.workspace}}
            - run: echo "This job's status is ${{job.status}}" 
```
* Commit your changes 
- Committing the workflow file to branch in your repo triggers the push event and runs the workflow
- To view the results of the workflow, visit your repo in GitHub and selete or click on the Actions tab in GitHub