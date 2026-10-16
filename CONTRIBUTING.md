# Contributing to Claude Code Efficiency Guide

Thank you for helping make AI-assisted development more efficient, transparent,
and resource-conscious. This is a free, community-oriented documentation project.
Contributions of any size are welcome.

## Project principles

1. **Accuracy first.** Prefer verified, reproducible guidance to impressive claims.
2. **Efficiency without cutting corners.** Reduce unnecessary tokens, latency,
   resource usage, and API expenses without compromising safety or code quality.
3. **Practicality.** Show *when* and *how* to use a technique, ideally with an example.
4. **Clarity.** Write for developers with different experience levels.
5. **Transparency.** Disclose assumptions, model versions, trade-offs, and limitations.
6. **Independence.** Avoid promotional content and unverified provider claims.

## Ways to contribute

- Correct outdated Claude Code commands, flags, and feature descriptions.
- Submit new token- and context-efficiency techniques.
- Add concise real-world examples and reproducible benchmarks.
- Improve English, accessibility, structure, and navigation.
- Report broken links, unclear instructions, or unsafe recommendations.
- Propose translations (prefer a dedicated language file or folder).

## Before opening an issue

- Check existing issues and pull requests for duplicates.
- State the Claude Code version, model, operating system, and plan/API billing
  mode when the issue depends on them.
- Include a link to official documentation or a reproducible example when possible.
- Never post API keys, credentials, personal data, or private project code.

## Submitting a pull request

1. Fork the repository and create a descriptive branch (for example,
   `docs/improve-context-guide`).
2. Make focused changes; avoid unrelated reformatting.
3. Verify commands on the applicable Claude Code version, or clearly mark
   them as unverified/proposed.
4. Provide a short explanation of the problem, the change, and any evidence.
5. Update `CHANGELOG.md` under **Unreleased** for user-visible changes.
6. Open a pull request linked to any relevant issue.

### Pull request checklist

- [ ] My change is clear, practical, and scoped to this project.
- [ ] I checked for duplicate content and unnecessary verbosity.
- [ ] Commands, configuration keys, and links are accurate or labeled unverified.
- [ ] Claims about savings are supported by data or explicitly qualified.
- [ ] I did not include secrets, sensitive logs, or copyrighted material
      without permission.
- [ ] I updated `CHANGELOG.md` if the change is user-visible.

## Benchmarks and performance claims

Please include, where available:

| Field | Example |
| --- | --- |
| Claude Code version | Exact version used |
| Model | Exact model identifier |
| Setup | OS, tools, plugins, MCP configuration |
| Task | Concise description and input size |
| Baseline | Input/output/cache tokens or usage metrics |
| Optimized run | Same metrics under a comparable task |
| Quality check | Tests passed, output equivalence, review notes |
| Limitations | Variability, small samples, quota interpretation |

Do not present hypothetical or single-run improvements as guaranteed savings.
Token counts, API charges, and subscription usage quotas are different metrics.

## Editorial style

- Use clear international English and descriptive Markdown headings.
- Prefer short examples with comments explaining their purpose.
- Distinguish **official product behavior** from **recommendations** and
  **experimental techniques**.
- Explain trade-offs (for example, compression may omit important details).
- Avoid unnecessary superlatives or unsupported percentages.
- Link to primary sources, especially Anthropic documentation, when available.
- Preserve code blocks, paths, and commands exactly unless intentionally updating them.

## AI-assisted contributions

AI tools can help draft or review changes, but contributors remain responsible
for checking factual accuracy, licensing, and technical correctness. Do not
submit untested commands or fabricated benchmark results.

## License and attribution

By submitting a contribution, you agree to license your contribution under the
repository's **CC BY 4.0** license, unless clearly stated otherwise and agreed
with the maintainer. You retain copyright to your original contribution.
Please credit external sources properly and do not submit material you lack
rights to share.

For contributions containing executable code, clearly identify any third-party
license constraints in the pull request before inclusion. The maintainer may
choose a separate software license for future code files.

## Conduct and maintenance

Be respectful, constructive, and patient. Critique ideas and evidence, not
people. Spam, harassment, and promotional pull requests may be closed.
The project is maintained on a best-effort basis; acceptance and response times
are not guaranteed.

## Maintainer

**Antonio Maraucci** — Project creator and maintainer

- CEO, **Totaliweb** (web agency): https://www.totaliweb.com
- CEO, **Hostwebo** (managed WordPress hosting): https://www.hostwebo.com
- CEO, **Hostwebo** (managed WordPress hosting): https://www.hostwebo.com

This is an independent community resource, not an official Anthropic project.
