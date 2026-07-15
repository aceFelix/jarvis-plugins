---
name: everything-sdk
description: Search local files at extreme speed using Everything (voidtools). Requires Everything running with HTTP server enabled.
when_to_use: When the user asks to find/搜索/查找/search files on the local machine by name, path, or extension.
trigger_words: 找文件, 搜索文件, 查找, search files, find files, everything, es
---

# Everything SDK

Ultra-fast local file search via [Everything](https://www.voidtools.com/) engine.

## Prerequisites

Everything must be running with HTTP server enabled:
- Everything > Tools > Options > HTTP Server > Enable (default port 80)
- Or start: `everything.exe -startup`

## Usage

### Search by name

```bash
curl -s "http://localhost:80/?s=*keyword*&json=1"
```

Returns JSON: `{"results": [{"name": "...", "path": "...", "size": 123, "date_modified": "..."}]}`

### Common patterns

```bash
# All PDFs in a folder
curl -s "http://localhost:80/?s=D:\documents\*.pdf&json=1"

# Files modified today
curl -s "http://localhost:80/?s=*.py+dm:today&json=1"

# Largest 10 files
curl -s "http://localhost:80/?s=*&c=10&json=1&s=0"

# Specific extension anywhere
curl -s "http://localhost:80/?s=ext:mkv&json=1"

# Regex search (if enabled)
curl -s "http://localhost:80/?s=regex:.*report.*\.xlsx&json=1"
```

### CLI via es.exe (if installed)

```bash
es.exe "*.py" -n 20
es.exe /ad "project"          # folders only
es.exe /a-d "*.exe"           # files only  
es.exe -size -path "*.psd"    # show full path
```

## Tips

- Everything must be running (tray icon visible)
- If port 80 occupied, change in Everything HTTP server settings
- Search is near-instant even with millions of files
- `es.exe` must be in PATH or use full path: `"C:\Program Files\Everything\es.exe"`
