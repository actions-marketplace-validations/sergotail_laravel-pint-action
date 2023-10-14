# GitHub Action for Laravel Pint  

GitHub Action implementation of the [Laravel Pint](https://github.com/laravel/pint) Package. 

## Usage

Use with [GitHub Actions](https://github.com/features/actions)

_.github/workflows/pint.yml_

```
name: PHP Linting
on: pull_request
jobs:
  phplint:
    runs-on: ubuntu-latest
    steps:
        - uses: actions/checkout@v3

        - name: Get changed files
          id: changed-files
          uses: tj-actions/changed-files@v39

        - name: "laravel-pint"
          uses: sergotail/laravel-pint-action@1.0.1
          with:
            preset: laravel
            verboseMode: true
            testMode: true
            configPath: "vendor/my-company/coding-style/pint.json"
            pintVersion: 1.8.0
            onlyDirty: true
            onlyFiles: ${{ steps.changed-files.outputs.all_changed_files }}
          
```
ℹ️ Also you can specify the Pint version to be used by specifying a `pintVersion` in your configuration file.

If provided, a `pint.json` file in the root will be used for configuration during run of the Action.

This action **DOESN'T** commit changes automatically. If you want to achieve such behaviour you have to use it in combination with another action like [git-auto-commit Action](https://github.com/stefanzweifel/git-auto-commit-action) or [Create Pull Request Action](https://github.com/marketplace/actions/create-pull-request).

You can see Laravel Pint Action running on my [demo repository](https://github.com/aglipanci/laravel-pint-action-demo/pulls).
