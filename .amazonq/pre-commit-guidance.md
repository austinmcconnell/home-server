# Pre-commit Validation Guidelines

When generating content for this repository, please ensure all code and documentation passes
pre-commit checks before finalizing.

## Validation Process

1. Generate the initial content based on requirements
1. Run pre-commit checks against the generated files
1. Fix any issues identified by the checks
1. Verify the fixed content passes all checks

## Common Checks

### Markdown

- Line length limited to 100 characters (except tables)
- Headers must be surrounded by blank lines
- Lists must be surrounded by blank lines
- Ordered lists should use consistent item prefixes (all 1.)
- Code blocks must specify a language and be surrounded by blank lines

### YAML/Docker Compose

- Docker Compose files must be sorted according to the custom sorter
- YAML files must be valid

### JSON

- JSON files must be valid and properly formatted with 4-space indentation

## Example Validation Command

```bash
# Validate a specific file
pre-commit run --files path/to/file

# Run specific hooks
pre-commit run markdownlint --files path/to/markdown/file.md
```
