# Test Design Guidelines

You help the user articulate WHAT they want before they build it. This is the "specify" step of specify-encode-fulfill.

## Core Principle

Tests are executable specifications. A specification answers: "In scenario X, what should happen?"

## Specification Format

Good: "When the user submits an empty form, display a validation error."
Good: "When the API returns 500, show a graceful error message."
Good: "When no records exist, display 'No results found'."

Bad: "It works correctly." (What does 'correctly' mean?)
Bad: "It handles errors." (Which errors? How?)
Bad: "It validates input." (What validation? What happens on failure?)

## Avoid .first and .last in Tests

Using `.first` or `.last` to retrieve records in tests is fragile because it depends on ordering, which can change unexpectedly. Instead, use explicit queries with `change` and `where`:

Bad:
```ruby
post repositories_path, params: { repo_full_name: "jasonswett/ductwork" }
repository = Repository.last
expect(repository.github_account).to eq(github_account_jasonswett)
```

Good:
```ruby
expect { post repositories_path, params: { repo_full_name: "jasonswett/ductwork" } }
  .to change { Repository.where(github_account: github_account_jasonswett).count }.by(1)
```

## Don't Assert Incidental Things

Only assert what matters. Don't assert things that are:
- Implied by other assertions (if checking response body, don't also check `be_successful` - if it wasn't successful, the body check would fail)
- Implementation details rather than behavior
- Just noise that makes the test longer without adding meaning

Bad:
```ruby
expect(response).to be_successful  # redundant noise
expect(response.body).not_to include("deleted_item")
```

Good:
```ruby
expect(response.body).not_to include("deleted_item")
```

If the response wasn't successful, the body assertion tells you something went wrong. The `be_successful` check adds nothing.
