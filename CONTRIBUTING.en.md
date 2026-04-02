[简体中文](./CONTRIBUTING.md) | [English](./CONTRIBUTING.en.md)

# Contributing

Thanks for helping improve this repository.

This is a research-oriented documentation repository centered on source reading. The two main goals for contributions are:

- keep source-backed claims accurate
- keep human-facing docs clear, restrained, and easy to verify

## Before You Contribute

- Source-related claims must come from these two places only:
  - `https://github.com/ChinaSiro/claude-code-sourcemap`
  - the local mirror: `_upstream/claude-code-sourcemap/`
- Re-read source before making claims. Do not inherit older wording without verification.
- When evidence is partial, narrow the wording. Do not turn code clues into product facts.

## Writing Rules

- Keep Chinese docs friendly, restrained, and easy to read.
- Keep English mirrors natural and accurate. Avoid machine-translated phrasing.
- Keep human-facing docs aligned across Chinese and English.
- `PROMPTS/` explains assembly mechanisms and should not dump large raw prompts.
- Names such as `Buddy`, `KAIROS`, `voice`, `bridge`, and `remote isolation` must stay conservative.
- `feature()`, GrowthBook, and env gates only show that conditional paths exist. They do not prove public rollout.
- Prefer direct declarative wording over contrast-heavy turns such as “not X, but Y”.

## Directory Scope

- Contributions are welcome in:
  - root human-facing docs
  - `MODULES/`
  - `PROMPTS/`
  - `FEATURE-FLAGS/`
  - `COMPARISONS/`
  - `SIMPLE/`
  - `DEEP/`
  - `EXAMPLES/`
  - `ASSETS/`
- Avoid editing by default:
  - `AI-AGENT/`
- Do not commit:
  - `TASK_GOAL.md`
  - `agents.md`
  - `_upstream/`

## Before Opening A PR

- confirm that navigation links and Chinese/English mirrors stay aligned
- confirm that source paths still point to `_upstream/claude-code-sourcemap/restored-src/src/...`
- run `git diff --check`
- if the change is documentation-only, tests can be skipped, but say so explicitly in the delivery note:
  - `本轮没有跑测试，原因是文档改写`

## Pull Request Notes

- Keep the title direct and scoped.
- In the PR description, it helps to say:
  - which pages changed
  - whether any source claims were tightened
  - whether English mirrors or navigation were updated
  - which minimal checks were run
