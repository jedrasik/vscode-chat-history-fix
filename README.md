# VS Code Chat History Fix

**Lost your VS Code chat history?** This tool can restore it! 🔧

## Quick Fix (Recommended)

**Close VS Code completely**, then run:

```bash
python3 fix_chat_session_index_v3.py
```

That's it! Reopen VS Code and your chat sessions should be back.

---

## What Happened?

Your chat sessions aren't actually lost - they just became invisible due to a corrupted index in VS Code's database. The session files still exist on disk, but VS Code doesn't know to load them.

**This tool rebuilds the index so VS Code can find your sessions again.**

---

## Which Script to Use?

### Option 1: Automatic Fix (Easiest) ⭐

**`fix_chat_session_index_v3.py`** - Finds and fixes all corrupted workspaces automatically.

```bash
# See what would be fixed (safe preview)
python3 fix_chat_session_index_v3.py --dry-run

# Fix everything (asks for confirmation)
python3 fix_chat_session_index_v3.py

# Fix everything automatically (no prompts)
python3 fix_chat_session_index_v3.py --yes
```

### Option 2: Manual Selection

**`fix_chat_session_index_v2.py`** - Choose which workspace to fix.

```bash
# List your workspaces
python3 fix_chat_session_index_v2.py

# Fix a specific workspace
python3 fix_chat_session_index_v2.py <workspace_id>
```

---

## Important Notes

### ⚠️ Close VS Code First!

Always close VS Code **completely** before running these scripts. Otherwise, VS Code might overwrite your fixes.

### ✅ Safe to Use

- Creates automatic backups before making changes
- Only modifies the index, never deletes your session data
- Can preview changes with `--dry-run` mode

### 📋 Requirements

- Python 3.6 or newer
- No installation needed - uses only Python standard library

---

## How It Works

1. **Scans** your VS Code workspace storage for session files
2. **Detects** sessions that exist on disk but are missing from the index
3. **Rebuilds** the index to include all your sessions
4. **Backs up** the database before making any changes

---

## Example Output

```
🔍 Scanning VS Code workspaces...
   Found 3 workspace(s) with chat sessions

🔧 Found 1 workspace(s) needing repair:

1. Workspace: 68afb7ebecb251d147a02dcf70c41df7
   Folder: /home/user/my-project
   Sessions on disk: 13
   Sessions in index: 1
   ⚠️  Missing from index: 12

📊 Total issues:
   Sessions to restore: 12

✨ REPAIR COMPLETE
   Workspaces repaired: 1
   Total sessions restored: 12
```

---

## Troubleshooting

**Script says "No workspaces found"**
- Make sure you've used VS Code Chat before
- Check that `~/.config/Code/User/workspaceStorage/` exists

**Sessions still not showing**
- Ensure you closed VS Code before running the script
- Try reloading VS Code window (Ctrl+Shift+P → "Reload Window")
- Check the backup was created successfully

**Want to undo the fix?**
- Find the backup file: `state.vscdb.backup.TIMESTAMP`
- Copy it back to `state.vscdb`

---

## Report the Bug

This is a VS Code core issue, not an extension bug. Help get it fixed permanently:

1. See `VSCODE_CORE_BUG_REPORT.md` for details
2. File at: https://github.com/microsoft/vscode/issues

---

## License

MIT

---

**Need help?** Open an issue with details about your problem.
