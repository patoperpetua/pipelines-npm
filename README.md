# SINGLETON SD - PIPELINES - NPM TEMPLATE

This project contains templates for npm common jobs.

## AVAILABLE FILES

There are 2 files:

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

## HOW TO USE

To use it, you can include them as following:

```yaml
include:
  - project: 'singletonsd/pipelines/npm'
    file: '/src/.gitlab-ci-******.yml'
```

And also define the stages you want to use. It can be both or just one. Remember to include the one you want or main if you use both, like following:

```yaml
stages:
  - test_dynamic
  - test_static
```

## TODO

- [ ] Create docker image with gitlab linter.
- [ ] Use a variable to select docker image node version.

----------------------

© [Singleton SD](http://www.singletonsd.com), Italy, 2019.
