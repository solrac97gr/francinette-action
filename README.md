# Francinette GitHub Action

This GitHub Action runs [Francinette (paco)](https://github.com/xicodomingues/francinette), a testing framework for 42 School projects.

## Description

Francinette is a testing tool that works like a local moulinette to check your 42 projects. This action automatically installs Francinette and runs it on your repository code. It supports the following projects:

- libft
- ft_printf
- get_next_line
- minitalk
- pipex

## Usage

Add this to your GitHub workflow file (`.github/workflows/francinette.yml`):

```yaml
name: Francinette Tests

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  francinette:
    runs-on: ubuntu-latest
    name: Run Francinette
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
          
      - name: Run Francinette
        uses: solrac97gr/libft-action@v1
        with:
          strict: 'false'  # Set to 'true' for strict mode testing
          # project: 'libft'  # Optional: Specify a project or let Francinette detect it
          # tests: 'memset isalpha'  # Optional: Specify specific tests to run
```

## Inputs

The action accepts the following inputs:

| Input    | Description                                               | Required | Default |
|----------|-----------------------------------------------------------|----------|---------|
| project  | Project to test (e.g., 'libft', 'ft_printf')              | No       | ''      |
| strict   | Run in strict mode to test against memory leaks           | No       | 'false' |
| tests    | Specific tests to run (space separated)                   | No       | ''      |

## Examples

### Run with default settings (auto-detect project)

```yaml
- name: Run Francinette
  uses: solrac97gr/libft-action@v1
```

### Run in strict mode

```yaml
- name: Run Francinette with strict mode
  uses: solrac97gr/libft-action@v1
  with:
    strict: 'true'
```

### Run specific tests for libft

```yaml
- name: Run specific libft tests
  uses: solrac97gr/libft-action@v1
  with:
    project: 'libft'
    tests: 'memset isalpha memcpy'
```

## Note

This action requires Ubuntu as the runner OS. It doesn't currently support macOS runners.

## License

MIT
