## GitHub actions quarto example

This is an example project that creates a website using GitHub actions with [Quarto](https://quarto.org). 

- The repo: [https://github.com/anielsen001/quarto-github-pages-actions-example](https://github.com/anielsen001/quarto-github-pages-actions-example)
- The webpage: [https://anielsen001.github.io/quarto-github-pages-actions-example](https://anielsen001.github.io/quarto-github-pages-actions-example)


## Create a quarto project

```bash
quarto create-project
```



## Python code example

An executable python code example can be found in `sources/python.qmd`

## Computation freeze

This example uses the [code computation freeze directive](https://quarto.org/docs/publishing/github-pages.html#freezing-computations).

## Configure the repository to use gh-pages
 
The following command step `quarto publish` won't complete unless this is set up first. 

## Manually perform `quarto publish`

https://quarto.org/docs/publishing/github-pages.html#publish-action

```bash
quarto publish gh-pages
```

This may take a long time to run. The documentation says that this will create a file called `_publish.yml` but that did not happen for me (quarto version 1.2.269).

Instead, manually create a `.github/workflows/publish.yml`

```bash
mkdir -p .github/workflows
touch .github/workflows/publish.yml
```

and put the following into `publish.yml` (copied directory from [quarto docs](https://quarto.org/docs/publishing/github-pages.html#publish-actions)
```yaml
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      - name: Render and Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```


## References

- [Quarto Documentation](https://quarto.org/docs/publishing/github-pages.html)