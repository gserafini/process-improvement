# Process Improvement Protocol Plugin

Systematic intervention system for detecting frustration, analyzing root causes, implementing fixes, and tracking effectiveness over time.

## Installation

This plugin has been created and registered in Claude Code. To activate it:

**YOU MUST RESTART CLAUDE CODE** for the plugin to be loaded.

Once restarted, the skill will be available as:
- **Skill tool**: `Skill(process-improvement:process-improvement-protocol)`
- **Slash command**: `/improve [week|month|year|all]`

## Plugin Structure

```
process-improvement/
├── .claude-plugin/
│   └── plugin.json              # Plugin metadata
├── skills/
│   └── process-improvement-protocol/
│       └── SKILL.md             # Main skill documentation
├── commands/
│   └── improve.md               # /improve slash command
└── data/                        # Runtime data (copied from ~/.claude/process-improvement/)
    ├── incidents.jsonl          # Incident tracking
    ├── days-without-incident.json
    ├── sessions/                # Resume contexts
    ├── deferred-incidents/      # Saved for later
    ├── fixes-registry/          # Fix documentation
    ├── successful-fixes.md
    ├── patterns-detected.md
    └── experiments.md
```

## Registration

Plugin registered in `~/.claude/plugins/installed_plugins.json` as:
```json
"process-improvement@local": {
  "version": "1.0.0",
  "installedAt": "2025-11-21T23:00:00.000Z",
  "lastUpdated": "2025-11-21T23:00:00.000Z",
  "installPath": "/Users/gserafini/.claude/plugins/marketplaces/process-improvement/",
  "isLocal": true
}
```

## Usage

After restarting Claude Code:

### Via Slash Command (Recommended)
```
/improve month    # Analyze last 30 days (default)
/improve week     # Analyze last 7 days
/improve year     # Analyze last 365 days
/improve all      # Analyze entire history
```

### Via Skill Tool
```
Skill(process-improvement:process-improvement-protocol)
```

### Auto-Detection
The skill can also be triggered automatically when frustration phrases are detected in user messages:
- "Stop"
- "I keep asking"
- "Did you actually"
- "You didn't test"
- etc.

## Data Storage

Process improvement data is stored in both locations:
- **Runtime data**: `~/.claude/plugins/marketplaces/process-improvement/data/`
- **Original location**: `~/.claude/process-improvement/` (legacy, can be removed after confirming plugin works)

## Testing Status

**Created**: 2025-11-21
**Status**: Plugin structure complete, awaiting Claude Code restart for testing

**Next Steps**:
1. Restart Claude Code
2. Run `/improve month` to test
3. Verify skill is discoverable via `Skill` tool
4. Complete full workflow test (all 5 phases)
5. Verify file creation (sessions/, incidents.jsonl updates)

## Version History

- **1.0.0** (2025-11-21): Initial plugin creation
  - Converted from user skill to plugin
  - Added plugin.json manifest
  - Registered in installed_plugins.json
  - Copied all data files to plugin structure
