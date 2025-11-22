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

Process improvement data is stored in the plugin's data directory:
- **Plugin install**: `~/.claude/plugins/marketplaces/process-improvement/data/`
- **Local testing**: `./data/` (relative to plugin root)
- **Legacy location**: `~/.claude/process-improvement/` (deprecated, see migration below)

The plugin automatically detects its installation location and uses the correct path.

## Migration from Legacy Installation

If you previously used this as a user skill at `~/.claude/process-improvement/`, migrate your data after installing the plugin:

```bash
# Backup first!
cp -r ~/.claude/process-improvement ~/.claude/process-improvement.backup

# Install plugin first (if not already done)
# /plugin marketplace add gserafini/process-improvement
# /plugin install process-improvement

# Find plugin installation directory
PLUGIN_DIR=$(find ~/.claude/plugins/marketplaces -type d -name "process-improvement" -maxdepth 2 | head -1)

# Migrate data to plugin directory
mkdir -p "$PLUGIN_DIR/data"
cp ~/.claude/process-improvement/*.{json,jsonl,md} "$PLUGIN_DIR/data/" 2>/dev/null || true
cp -r ~/.claude/process-improvement/sessions "$PLUGIN_DIR/data/" 2>/dev/null || true
cp -r ~/.claude/process-improvement/deferred-incidents "$PLUGIN_DIR/data/" 2>/dev/null || true
cp -r ~/.claude/process-improvement/fixes-registry "$PLUGIN_DIR/data/" 2>/dev/null || true

# Verify migration
ls -la "$PLUGIN_DIR/data"

# Optional: Remove legacy directory after confirming plugin works
# rm -rf ~/.claude/process-improvement
```

## Local Testing (Development)

To test the plugin locally before publishing:

```bash
# Clone or navigate to plugin directory
cd /path/to/process-improvement

# Add as local marketplace
/plugin marketplace add .

# Verify installation
/plugin list

# Test the skill
/improve week

# Verify data directory creation
ls -la ./data/
```

## Post-Install Verification

After installing from GitHub marketplace:

```bash
# Verify plugin files
PLUGIN_DIR=$(find ~/.claude/plugins/marketplaces -type d -name "process-improvement" -maxdepth 2 | head -1)
ls -la "$PLUGIN_DIR"

# Verify data directory structure
ls -la "$PLUGIN_DIR/data/"

# Should show:
# - incidents.jsonl
# - days-without-incident.json
# - sessions/
# - deferred-incidents/
# - fixes-registry/
# - experiments.md
# - patterns-detected.md
# - successful-fixes.md

# Test skill invocation
/improve month
```

## Testing Status

**Created**: 2025-11-21
**Status**: v1.0.1 - Path bugs fixed, ready for testing

**What changed in v1.0.1**:
- ✅ Fixed hardcoded paths - plugin now works with marketplace installs
- ✅ Added Phase 0 path discovery
- ✅ All file references use ${PLUGIN_DATA} variable
- ✅ Added migration instructions for legacy installations
- ✅ Added .gitkeep to fixes-registry/ directory

**Next Steps**:
1. Install plugin via `/plugin marketplace add gserafini/process-improvement`
2. Run `/improve month` to test
3. Verify file creation in `~/.claude/plugins/marketplaces/process-improvement/data/`
4. Complete full workflow test (all 5 phases)
5. Verify effectiveness tracking works

## Troubleshooting

### "File not found" errors

**Symptom**: Skill fails with `No such file or directory: ~/.claude/process-improvement/...`

**Cause**: You're running an old version (v1.0.0) with hardcoded paths

**Fix**: Update to v1.0.1+ which has dynamic path discovery:

```bash
cd /path/to/process-improvement
git pull
/plugin marketplace remove process-improvement
/plugin marketplace add .
```

### Plugin not showing in /plugin list

**Cause**: marketplace.json might have syntax errors

**Fix**: Validate JSON at jsonlint.com, check for trailing commas

### Data directory not created

**Cause**: Phase 0 path discovery didn't run

**Fix**: Verify you're invoking the skill (not just the slash command directly):

```bash
# Correct:
/improve month

# Also correct:
Skill(process-improvement:process-improvement-protocol)
```

## Version History

- **1.0.1** (2025-11-21): Path bug fixes
  - Fixed hardcoded paths that broke marketplace installs
  - Added Phase 0 dynamic path discovery
  - All file operations now use ${PLUGIN_DATA} variable
  - Added migration instructions for legacy users
  - Added .gitkeep to preserve fixes-registry/ directory
  - Added troubleshooting section
  - Ready for production use

- **1.0.0** (2025-11-21): Initial plugin creation ⚠️ DO NOT USE
  - Converted from user skill to plugin
  - Added plugin.json manifest
  - ❌ Critical bug: Hardcoded paths break on marketplace install
  - Use v1.0.1+ instead
