# DEVELOPING: fysigo-claude-plugin

The Fysigo Claude plugin, generated from fysigo-web's MCP catalog and companion skill. Never hand-edit `plugins/fysigo/`.

Regenerate from origin/main, never a stale checkout:

    S=$(mktemp -d); git -C <fysigo-web> archive origin/main src/lib/mcp/catalog.generated.json coach-skills/skills/fysigo-mcp | tar -x -C $S
    node scripts/generate.mjs --source $S --zip dist/fysigo.zip

`--check` exits 1 when the committed plugin is stale. Connector: https://app.fysigo.com/api/mcp/mcp. Submission to the Claude directory is done by the COO, not from here.

CI policy (Daniel, 2026-11-13): no PR workflows, no required checks, no new runners.
