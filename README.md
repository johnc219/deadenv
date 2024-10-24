# deadenv
Detect environment variables that might be unused

## Installation
1. install [rg](https://github.com/BurntSushi/ripgrep)
1. install [heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)
1. clone this repo
1. `chmod +x deadenv`
1. Optionally make it available in your `PATH`

## Usage
```bash
cd my_app
deadenv --heroku my_app_name
```

See `deadenv --help` for more

> [!TIP]
> The default `rg` input and filter options will be used. You can forward any
> `rg` options to customize what will be searched.

## Examples
Forward any `rg` options to customize the search
```bash
deadenv --heroku app_name -- --hidden --no-ignore
```

Process results using `jq`
```bash
deadenv --heroku app_name | jq '.[] | select(.matches == 0)'
```

Identify ENV vars that are only found in one or more glob patterns
```bash
deadenv --heroku app_name -t '.env*' -t 'app.json' -t 'spec/*/**' -- --hidden | jq '.[] | select(.matches_test_globs_only == true)'
```
