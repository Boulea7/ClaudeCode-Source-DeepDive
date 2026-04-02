[简体中文](./comparison.md) | [English](./comparison.en.md)

# Short Comparison

Many tools can run parallel workers or multiple jobs.

Claude Code is more specific at this layer:

- interactive and headless sessions share one `query()` turn loop
- child-agent dispatch uses a formal tool path rather than prompt-only convention
- background tasks, remote tasks, shell work, and teammates share one task representation layer
- backgrounded main-session work still lives inside that same task framework
