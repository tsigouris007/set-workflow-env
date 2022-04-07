# set-workflow-env
This action helps you set environment variables.
Will be extended later for more goodies.

## Usage
Before calling this step you should use the `actions/checkout` action with `fetch-depth: 0`. 
Then call this action:
```yaml
jobs:
  Jobname:
    runs-on: self-hosted
    steps:
      - name: Checkout action
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Set workflow environment 
        uses: skr-actions/set-workflow-env@master
        with:
          changed_files_filter: '\*.js$|\*.jsx$'
```
### Parameters
#### `changed_files_filter`
You can leave unspecified which defaults into null and does not do any filtering. Otherwise, you
can specify a custom grep regex filter to keep only the files you are interested in such as: 
`*.js$, *.erb$, *.py$`.

### Returns
After calling this action you will have available in your environment the following variables:

#### `CHANGED_FILES`
A flat space-delimited list of the changed files - works on both commit pushes and pull requests. Example:
```
file1.jsx file2.jsx file3.js
```

#### `PR_NO`
The pull request number. If the event is a pull request it fetches the number otherwise it is left null.

#### `COMMIT_SHA`
The commit sha. If the event is a pull request it fetches the pull request head sha otherwise the commit sha.
