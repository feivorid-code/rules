# Repository Guidelines

## Project Structure & Module Organization

This repository stores network rule lists. The root contains only repository metadata and `README.md`; rule content lives under `quantumultx/`.

- `quantumultx/*.list`: Quantumult X rule lists grouped by service or topic, such as `applepush.list`, `homebrew.list`, `php.list`, and `zoom.list`.
- `README.md`: minimal project description.
- No application source, compiled assets, or generated build output is expected.

Keep new rule files in `quantumultx/` and name them with lowercase, descriptive service names, for example `github.list` or `docker.list`.

## Build, Test, and Development Commands

There is no build step for this repository. Use shell checks before committing:

```sh
rg -n "^[^#[:space:]]" quantumultx
```

Lists active rule lines for review.

```sh
rg -n "^\s*$" quantumultx/*.list
```

Finds blank lines; use them sparingly to separate logical groups.

```sh
git diff -- quantumultx
```

Review exact rule changes before committing.

## Coding Style & Naming Conventions

Use Quantumult X rule syntax consistently:

```text
HOST-SUFFIX,example.com,PolicyName
HOST,api.example.com,PolicyName
IP-CIDR,192.0.2.0/24,PolicyName,no-resolve
```

Start each list with a short comment header such as `#ApplePush`. Group related rules with comments. Keep policy names stable within a file, using clear PascalCase or existing names already present, such as `ApplePush` or `PHP`. Prefer specific rules over broad keyword rules unless the broad match is intentional and documented.

## Testing Guidelines

No automated test framework is configured. Validate changes by checking syntax manually and loading the edited list in Quantumult X when possible. For IP rules, confirm CIDR ranges from authoritative vendor documentation. For host rules, avoid duplicate entries and verify whether `HOST`, `HOST-SUFFIX`, or `HOST-KEYWORD` is the narrowest correct match.

## Commit & Pull Request Guidelines

Git history uses short messages such as `fix`, `add new rules`, and occasional Conventional Commit style like `fix: tune Apple push rules`. Prefer concise Conventional Commit messages going forward:

```text
fix: tune Apple push rules
feat: add Docker registry rules
docs: update contributor guide
```

Pull requests should describe the affected service, explain why rules changed, and mention any manual validation performed. Include links to vendor documentation for new IP ranges or broad host matches.

## Security & Configuration Tips

Do not commit private endpoints, credentials, tokens, or personal proxy node names. Review `.list` files for sensitive domains before publishing.
