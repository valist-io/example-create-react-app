# Create React App Example

This example demonstrates how to publish your Create React App on Valist.

> *IMPORTANT* You must add `"homepage": "."` to your `package.json` for the static build paths to work correctly.

## Publish with the Valist GitHub Action

See the [GitHub Action Quick Start](https://docs.valist.io/github-action/github-action-quick-start) for more info.

```yaml
on:
  release:
    types: [published]
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/setup-node@v2
        with:
          node-version: '16'
      - uses: actions/checkout@v2
      - run: |
          npm install
          npm run build
      - uses: valist-io/valist-github-action@dev
        with:
          private-key: ${{ secrets.PRIVATE_KEY }}
          account: <your-account-name-here>
          project: <your-project-name-here>
          release: ${{ github.ref_name }}
          path: './build'
```

## Publish with the Valist CLI

Create a `valist.yml` file in the root of your project.

```yaml
account: <your-account-name-here>
project: <your-project-name-here>
release: <your-release-name-here>
path: ./build
```

See the [CLI Quick Start](https://docs.valist.io/cli/cli-quick-start) for more info.

```bash
$ npm run build
$ valist publish <your-account-name-here>/<your-project-name-here> ./build
```
