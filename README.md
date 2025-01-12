# composer update workflow (reusable)

Run `composer update` and create pull request.

## Usage

### Workflow permissions

To use this workflow, you need to allow creating pull requests in the repository settings - Actions - General.

- Read and write permissions
- Allow GitHub Actions to create and approve pull requests

### Create Personal access tokens (classic)

Alternatively, you can create a personal access token. If the above settings do not work, please try this method.

Set the token in the repository's secrets as `ACTION_TOKEN`

`GITHUB_TOKEN` can't trigger other actions. If you want to run tests after pull request, you need a token.

### Create `.github/workflows/composer-update.yml`

```yaml
name: composer update

on:
  schedule:
    - cron: '0 0 * * *' #UTC

jobs:
  composer:
    uses: kawax/composer-workflow/.github/workflows/update.yml@v1
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

If you use `ACTION_TOKEN`.

```yaml
name: composer update

on:
  schedule:
    - cron: '0 0 * * *' #UTC

jobs:
  composer:
    uses: kawax/composer-workflow/.github/workflows/update.yml@v1
    secrets:
      token: ${{ secrets.ACTION_TOKEN }}
```

## Inputs
| name           | description                                  | default                                                 |
|----------------|----------------------------------------------|---------------------------------------------------------|
| php            | php version (same as setup-php)              | 'latest'                                                |
| extensions     | php extensions (same as setup-php)           | mbstring                                                |
| git-name       | git name                                     | `github-actions[bot]`                                   |
| git-email      | git email                                    | `41898282+github-actions[bot]@users.noreply.github.com` |
| composer-path  | working directory                            | `./`                                                    |
| branch         | git branch (Always works on a single branch) | composer-update                                         |
| title          | Pull request title                           | composer update                                         |
| commit-message | commit message                               | composer update                                         |

```yaml
jobs:
  composer:
    uses: kawax/composer-workflow/.github/workflows/update.yml@v1
    secrets:
      token: ${{ secrets.ACTION_TOKEN }}
    with:
      php: 8.4
      extensions: mbstring
      git-name: github-actions[bot]
      git-email: 41898282+github-actions[bot]@users.noreply.github.com
      composer-path: ./composer
      branch: composer-update
      title: composer update
      commit-message: composer update
```

## LICENCE
MIT
