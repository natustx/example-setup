---
name: writing-tests
description: Writes behavior-focused tests using Testing Trophy model with real dependencies. Use when writing tests, choosing test types, or avoiding anti-patterns like testing mocks.
metadata:
  source: https://github.com/rileyhilliard/claude-essentials/tree/main/plugins/ce/skills/writing-tests
---

# Writing Tests

**Core principle:** Test user-observable behavior with real dependencies. Tests should survive refactoring.

## Testing Trophy Model

| Priority | Type        | When                                            |
| -------- | ----------- | ----------------------------------------------- |
| 1st      | Integration | Default - multiple units with real dependencies |
| 2nd      | E2E         | Complete user workflows                         |
| 3rd      | Unit        | Pure functions only (no dependencies)           |

## Mocking Guidelines

**Default: Don't mock. Use real dependencies.**

**Only mock:**

- External HTTP/API calls
- Time/randomness
- Third-party services (payments, email)

**Never mock:**

- Internal modules
- Database queries (use test DB)
- Business logic
- Your own code calling your own code

## Test Type Decision

```
Complete user workflow? → E2E test
Pure function (no side effects)? → Unit test
Everything else → Integration test
```

## Assertion Strategy

| Context | Assert On             | Avoid                       |
| ------- | --------------------- | --------------------------- |
| UI      | Visible text, roles   | CSS classes, internal state |
| API     | Response body, status | Internal DB state           |
| Library | Return values         | Private methods             |

## Anti-Patterns

| Pattern                         | Fix                         |
| ------------------------------- | --------------------------- |
| Testing mock calls              | Test actual outcome         |
| Test-only methods in production | Move to test utilities      |
| `sleep(500)`                    | Use condition-based waiting |
| Asserting on internal state     | Assert on observable output |
| Incomplete mocks                | Mirror real API completely  |

## Quality Checklist

- [ ] Happy path covered
- [ ] Error conditions handled
- [ ] Real dependencies used (minimal mocking)
- [ ] Tests survive refactoring
- [ ] Test names describe behavior

## Language-Specific Patterns

- **JavaScript/Typescript/React**: See [references/typescript-react.md](references/typescript-react.md)
- **Python**: See [references/python.md](references/python.md)
- **Go**: See [references/go.md](references/go.md)

For flaky tests with timing issues, use the `condition-based-waiting` skill.
