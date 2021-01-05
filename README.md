# mkdocs-include-markdown-plugin

Mkdocs Markdown includer plugin.

## Status

[![PyPI][pypi-version-badge-link]][pypi-link]
[![Tests][tests-image]][tests-link]
[![Coverage status][coverage-image]][coverage-link]

## Installation

```bash
pip install mkdocs-include-markdown-plugin
```

## Documentation

### Setup

Enable the plugin in your `mkdocs.yml`:

```yaml
plugins:
  - include-markdown
```

### Directives

This plugin provides two directives, one to include markdown files and another
to include files of any type. Paths of included files can be absolute or
relative to the path of the file that includes them:

#### **`include-markdown`**

Includes markdown file content, optionally using two delimiters to filter the
content to include.

- **start**: Delimiter that marks the beginning of the content to include.
- **end**: Delimiter that marks the end of the content to include.
- **rewrite_relative_urls** (*true*): When this option is enabled (default),
 Markdown links and images in the content that are specified by a relative URL
 are rewritten to work correctly in their new location. Possible values are
 `true` and `false`.
- **comments** (*true*): When this option is enabled (default), the content to
 include is wrapped by `<!-- BEGIN INCLUDE -->` and `<!-- END INCLUDE -->`
 comments which help to identify that the content has been included. Possible
 values are `true` and `false`.
- **preserve_includer_indent** (*false*): When this option is enabled, every
 line of the content to include is indented with the same number of spaces
 used to indent the includer `{% %}` template. Possible values are `true` and
 `false`.

> Note that the **start** and **end** strings may contain usual (Python-style)
escape sequences like `\n`, which is handy if you need to match on a multi-line
start or end trigger.

##### Examples

```jinja
{%
   include-markdown "../README.md"
   start="<!--intro-start-->"
   end="<!--intro-end-->"
%}
```

```jinja
{%
   include-markdown "docs/includes/header.md"
   start="<!--\n\ttable-start\n-->"
   end="<!--\n\ttable-end\n-->"
   rewrite_relative_urls=false
   comments=false
%}
```

#### **`include`**

Includes the content of a file.

- **start**: Delimiter that marks the beginning of the content to include.
- **end**: Delimiter that marks the end of the content to include.
- **preserve_includer_indent** (*false*): When this option is enabled, every
 line of the content to include is indented with the same number of spaces
 used to indent the includer `{% %}` template. Possible values are `true` and
 `false`.

> Note that the **start** and **end** strings may contain usual (Python-style)
escape sequences like `\n`, which is handy if you need to match on a multi-line
start or end trigger.

##### Examples

```jinja
~~~yaml
{% include "../examples/github-minimal.yml" %}
~~~
```

```jinja
    {%
      include "../examples/github-minimal.yml"
      start="~~~yaml"
      end="~~~"
      preserve_includer_indent=true
    %}
```

## Acknowledgment

- Joe Rickerby and contributors for
 [giving me the permissions][cibuildwheel-470] to separate this plugin from the
 documentation of [cibuildwheel][cibuildwheel-repo-link].

[pypi-link]: https://pypi.org/project/mkdocs-include-markdown-plugin
[pypi-version-badge-link]: https://img.shields.io/pypi/v/mkdocs-include-markdown-plugin
[tests-image]: https://img.shields.io/github/workflow/status/mondeja/mkdocs-include-markdown-plugin/CI?logo=github
[tests-link]: https://github.com/mondeja/mkdocs-include-markdown-plugin/actions?query=workflow%3ACI
[coverage-image]: https://img.shields.io/coveralls/github/mondeja/mkdocs-include-markdown-plugin?logo=coveralls
[coverage-link]: https://coveralls.io/github/mondeja/mkdocs-include-markdown-plugin

[cibuildwheel-470]: https://github.com/joerick/cibuildwheel/issues/470
[cibuildwheel-repo-link]: https://github.com/joerick/cibuildwheel
