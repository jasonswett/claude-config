# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## ⚠️ CRITICAL WORKFLOW REQUIREMENTS

**NEVER commit without explicit user approval.** Always ask permission before making any commits.
Push after every commit only after user approval.

## Workflow

Commits should be atomic.
Don't mix jobs.
Don't mix bugfixes with refactors.
Don't mix bugfixes with behavior changes.
Don't mix refactors with behavior changes.

Commit messages should be a single short sentence with a period at the end.

Unless otherwise specified, favor making changes on feature branches rather than the main branch.

### Debugging

The first step of debugging is to determine an EXPLANATION of why the bug is occurring.
Don't just make guesses and then try to apply the guesses.
Come up with hypotheses and then see if you can find any way to disprove them.

### Naming

Always be consistent about naming. Use predictable names.
Bad: `repositories.each { |repo| repo.destroy }`
Good: `repositories.each { |repository| repository.destroy }`
Also good: `repositories.each { |r| r.destroy }`
Bad: `admin_user.each { |user| user.destroy }`
Good: `admin_user.each { |admin_user| admin_user.destroy }`
Also good: `admin_user.each { |u| u.destroy }`

Another consistency example:

Bad: `data-terminal-output-delay-value="<%= DOM_RENDER_DELAY_IN_MILLISECONDS %>">`
Good: `data-terminal-output-dom-render-delay-value="<%= DOM_RENDER_DELAY_IN_MILLISECONDS %>"`

## Testing

When writing tests, consult the Professional Rails Testing reference in memory/professional-rails-testing/ for guidance on approach and style.

## Git Usage

Always commit using full sentences with a period at the end.

When merging, always use --squash.

Never include the "Generated with Claude" message.
