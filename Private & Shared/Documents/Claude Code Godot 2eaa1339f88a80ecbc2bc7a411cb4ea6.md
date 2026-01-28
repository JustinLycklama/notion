# Claude Code Godot

~/.claude.json

Add this at the bottom

```jsx
,
  "mcpServers": {
    "godot": {
      "type": "stdio",
      "command": "node",
      "args": ["C:\\Users\\Justin\\Development\\Godot\\godot-mcp\\build\\index.js"],
      "env": {
        "DEBUG": "true",
        "GODOT_PATH": "C:\\Program Files (x86)\\GoDot\\Godot_v4.2.1-stable_win64.exe",
        READ_ONLY: "true"
      }
    }
  }

```

Switched models, this works:

```jsx
"mcpServers": {
    "godot-mcp": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@satelliteoflove/godot-mcp"],
      "env": {
        "GODOT_PATH": "C:\\Program Files (x86)\\GoDot\\Godot_v4.2.1-stable_win64.exe"
      }
    }
  }
```