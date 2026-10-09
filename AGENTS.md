# Agent guide

This repository is a starter editor plugin for Awake. A plugin depends only on
`com.awakekt.awake.editor:contract`; never add an editor's own artifacts. Keep game runtime out of
the plugin. The `awake-editor-plugin-authoring` skill has the rules.

## Agent skill bundles

`.agents/skills.lock.toml` pins the game-authoring skills from
[awake-game-agent-skills](https://github.com/awakekt/awake-game-agent-skills). Claude Code installs
them at session start (`.claude/settings.json` runs `hooks/sync-agent-skills.sh`). To install by
hand:

```bash
git clone https://github.com/awakekt/awake-agent-skills .agents/vendor/awake-agent-skills-bootstrap
python3 .agents/vendor/awake-agent-skills-bootstrap/scripts/install_consumer.py --project .
```

It needs Python 3.11 or newer; on Windows, where `python3` is often the Microsoft Store placeholder,
run it with `py -3`.

Never edit the deployed copies under `.agents/` or `.claude/`.
