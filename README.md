<h1>
  Gradle Check Version Action for GitHub <br>
  <a href="https://discord.gg/bSsv7XM"><img src="https://img.shields.io/badge/chat-discord-green?logo=discord&amp;style=flat" height="20"></a>
</h1>

Verifies that the version number (in a pull request) was bumped by comparing it
to the prevous version from the base branch.

## Usage

See [`action.yaml`](action.yaml)

##### Basic

```yaml
name: api
on:
  pull_request:
    paths:
      - "api"
      - "!README.md"
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: facutk/gradle-check-version@v1
        with: { path: "api" }
```

#### Full

```yaml
name: api
on:
  pull_request:
    paths:
      - "api"
      - "!README.md"
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - id: pkg
        uses: kriasoft/check-version@v1
        with:
          path: "api"
          format: "{name}_v{version}+build.{pr_number}.zip"

      - run: |
          echo "version: ${{ steps.pkg.outputs.version }}"
        #
        # Prints:
        #   version: 0.1.3
```

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE).
