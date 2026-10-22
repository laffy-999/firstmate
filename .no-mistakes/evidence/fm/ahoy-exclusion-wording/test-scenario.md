# Ahoy Skill Classification Test

## Change Under Test
The ahoy skill SKILL.md line 30 was changed from:
\`Captain quote: Run \`bin/fm-session-start.sh\` now...\`
to:
\`\`Captain quote: Run \`bin/fm-session-start.sh\` now...\`\`

This fixes markdown code span escaping so the example renders correctly.

## Classification Logic

### Deterministic Code (bin/fm-operational-input.sh line 168)
Uses exact string equality: \`[ "$message" = "$FM_LEGACY_SESSIONSTART" ]\`
- The exact verbatim payload matches -> classified as session-start (excluded)
- Any quoted/prefixed variant does NOT match -> not classified (captain message)

### Skill Instructions (SKILL.md lines 24, 30)
Line 24: "Exclude only the exact, verbatim legacy unmarked session-start payload..."
Line 30: "The legacy session-start exclusion applies only to the verbatim payload above; for example, \`\`Captain quote: Run...\`\` is a captain boundary."

## Test Verification
The markdown fix ensures the example clearly shows that:
1. "Captain quote: " prefix + the legacy payload = captain boundary (NOT excluded)
2. Only exact verbatim payload without prefix = excluded

The change clarifies the instruction text consumed by LLMs.
