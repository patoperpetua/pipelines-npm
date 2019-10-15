# SINGLETON SD - PIPELINES - NPM TEMPLATE

This project contains templates for npm common jobs.

> The **main repository** is hosted in [gitlab.com/singletonsd/pipelines/npm](https://gitlab.com/singletonsd/pipelines/npm.git) but it is automaticaly mirrored to [github.com/singletonsd](https://github.com/singletonsd/pipelines-npm.git), [github.com/patoperpetua](https://github.com/patoperpetua/pipelines-npm.git) and to [gitlab.com/patoperpetua](https://gitlab.com/patoperpetua/pipelines-npm.git). If you are in the Github page it may occur that is not updated to the last version.

## AVAILABLE FILES

There are 3 files:

- **common:** contains common jobs for any npm project/library. There are 2 jobs:
  - **install:** executes npm install.
  - **build:** executes npm run build-all.

- **test-dynamic:** contains jobs for run test script in each node environment. To enable these jobs, you need to setup variables to true. There is one variable to run all test (it finishes with **ALL**):
  - **TEST_DYNAMIC_EXECUTE_ALL**: "true"
  - **TEST_DYNAMIC_EXECUTE_4**: "true"
  - **TEST_DYNAMIC_EXECUTE_6**: "true"
  - **TEST_DYNAMIC_EXECUTE_7**: "true"
  - **TEST_DYNAMIC_EXECUTE_8**: "true"
  - **TEST_DYNAMIC_EXECUTE_10**: "true"
  - **TEST_DYNAMIC_EXECUTE_12**: "true"

- **test-static:** contains jobs for run static scripts.
  - The scripts are:
    - **linting:** run npm lint script.
    - **audit:** run npm audit script to check for vulneravilities.
    - **check:** run npm-check script to check for new versions of dependencies.
  - Available variables: (to run all, declare the one finished with **ALL**)
    - **TEST_STATIC_ALL**: "true"
    - **TEST_STATIC_LINT**: "true"
    - **TEST_STATIC_AUDIT**: "true"
    - **TEST_STATIC_CHECK**: "true"

## HOW TO

### USE

If you want to skip reading, you can copy and paste [this main example file](https://gitlab.com/singletonsd/pipelines/npm/raw/master/examples/.gitlab-ci-example-main.yml) or [this common example file](https://gitlab.com/singletonsd/pipelines/npm/raw/master/examples/.gitlab-ci-example-common.yml) and setup the variables.

To use it, you can include them as following (using repository aproach):

```yaml
include:
  # The main files contains includes all files
  - project: 'singletonsd/pipelines/npm'
    file: '/src/.gitlab-ci-main.yml'

  # Or you can include each file by your self.
  - project: 'singletonsd/pipelines/npm'
    file: '/src/.gitlab-ci-common.yml'
  - project: 'singletonsd/pipelines/npm'
    file: '/src/.gitlab-ci-test-dynamic.yml'
  - project: 'singletonsd/pipelines/npm'
    file: '/src/.gitlab-ci-static.yml'
```

Or using remote approach over gitlab repo:

```yaml
include:
  - remote: 'https://gitlab.com/singletonsd/pipelines/npm/raw/master/src/.gitlab-ci-main.yml'
  - remote: 'https://gitlab.com/singletonsd/pipelines/npm/raw/master/src/.gitlab-ci-common.yml'
  - remote: 'https://gitlab.com/singletonsd/pipelines/npm/raw/master/src/.gitlab-ci-test-dynamic.yml'
  - remote: 'https://gitlab.com/singletonsd/pipelines/npm/raw/master/src/.gitlab-ci-test-static.yml'
```

Or using remote approach over gilab pages:

```yaml
include:
  - remote: 'https://singletonsd.gitlab.io/pipelines/npm/latest/.gitlab-ci-main.yml'
  - remote: 'https://singletonsd.gitlab.io/pipelines/npm/latest/.gitlab-ci-common.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/npm/latest/.gitlab-ci-test-dynamic.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/npm/latest/.gitlab-ci-test-static.yml'
```

Master branch is setup as latest folder. To use an specific version, put the version name before the file name like:

```yaml
include:
  - remote: 'https://singletonsd.gitlab.io/pipelines/npm/1.0.0/.gitlab-ci-main.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/npm/develop/.gitlab-ci-test-dynamic.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/npm/feature-new/.gitlab-ci-test-static.yml'
```

And also define the stages you want to use. It can be both or just one. Remember to include the one you want or main if you use both, like following:

```yaml
stages:
  - install
  - test_static
  - build
  - test_dynamic
```

### TEST

You can test your .gitlab-ci.yml files by executing the following:

```bash
curl -s https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_test_standalone.sh | bash /dev/stdin
```

That script contains the following options:

```bash
-h | --help: display help.
-o | --only: the name of the file or folder to test.
```

Also you can download the script by:

```bash
curl -o gitlab-ci_lint_test_standalone.sh -L https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_test_standalone.sh
```

## GIT HOOK

You can setup gitlab lint tester to be run before a commit. To do that just execute the following script under your git repository:

```bash
curl -s https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_hook_installer.sh | bash /dev/stdin
```

## DOCUMENTATION

- [Gitlab CI - Includes](https://docs.gitlab.com/ee/ci/yaml/)

## TODO

- [X] Create docker image with gitlab linter.
- [X] Use a variable to select docker image node version.
- [X] Create a script to test locally.
- [X] Add example files.
- [X] Use ci-cd template.
- [ ] User variables to define allow_failure.

----------------------

© [Singleton SD](http://www.singletonsd.com), Italy, 2019.
