# Linters

Below is a list of linters supported by `slim-lint`, ordered alphabetically.

* [LineLength](#linelength)
* [RedundantDiv](#redundantdiv)
* [RuboCop](#rubocop)
* [TrailingWhitespace](#trailingwhitespace)

## LineLength

Option | Description
-------|-----------------------------------------------------------------
`max`  | Maximum number of columns a single line can have. (default `80`)

Wrap lines at 80 characters. You can configure this amount via the `max`
option on the linter, e.g. by adding the following to your `.slim-lint.yml`:

```yaml
linters:
  LineLength:
    max: 100
```

Long lines are harder to read and usually indicative of complexity.

## RedundantDiv

Reports explicit uses of `div` when it would otherwise be implicit.

**Bad: `div` is unnecessary when class/ID is specified**
```slim
div.button
```

**Good: `div` is required when no class/ID is specified**
```slim
div
```

**Good**
```slim
.button
```

Slim was designed to be concise, and not embracing this makes the tool less
useful.

## RuboCop

Option         | Description
---------------|--------------------------------------------
`ignored_cops` | Array of RuboCop cops to ignore.

This linter integrates with [RuboCop](https://github.com/bbatsov/rubocop) (a
static code analyzer and style enforcer) to check the actual Ruby code in your
templates. It will respect any RuboCop-specific configuration you have set in
`.rubocop.yml` files, but will explicitly ignore some checks (like
`Style/IndentationWidth`) since the extracted Ruby code sent to RuboCop is not
well-formatted.

```slim
- name = 'James Brown'
- unused_variable = 42

p Hello #{name}!
```

**Output from `slim-lint`**
```
example.slim:2 [W] Useless assignment to variable - unused_variable
```

You can customize which RuboCop warnings you want to ignore by modifying
the `ignored_cops` option (see [`config/default.yml`](/config/default.yml)
for the full list of ignored cops). Note that if you modify the list you'll
need to re-include all the items from the default configuration.

## TrailingWhitespace

Reports trailing whitespace (spaces or tabs) on any lines in a Slim document.