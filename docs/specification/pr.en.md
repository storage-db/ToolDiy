# Specification

This website is built up by multiple contributors and its contents are based on Markdown. So for restrictive reasons, we have some specifications for writing.

## Pull Request Message Specification[^1]

For Pull Request, please follow the following requirements:

1. The title should be clear about the purpose of this PR (what **work** is done, what **problem** is fixed).
2. The content should briefly describe the changes. If you fix an issue, please add `fix #xxxx` in the content, where `xxxx` is the issue number.

For the title, such format is recommended:

```plain
<Edit type>(<file name>): <content> (<issue number>)
```

Edit type can be one of the following:

- `feat`: for adding new content.
- `fix`: for fixing existing content errors.
- `refactor`: for refactoring a page (larger changes).
- `revert`: for reverting previous changes.

Examples:

- `fix(sepecification/specification): edit code comment to make it more clear`
- `fix: plugins/xxx not in directory (#2)`
- `feat(software/mathpix): official website`
- `refactor(specification/template): tidy up page content`

[^1]: Edited from [OI-wiki: 如何参与](https://oi-wiki.org/intro/htc/#pull-request-%E4%BF%A1%E6%81%AF%E6%A0%BC%E5%BC%8F%E8%A7%84%E8%8C%83)
