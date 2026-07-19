---
name: list-sessions
description: 查询 opencode 当前所有 session 的基本信息
---

列出所有 session（title、directory、更新时间），自动清理子 agent 垃圾 session：

```bash
sqlite3 ~/.local/share/opencode/opencode.db "DELETE FROM session WHERE agent != 'build';" && \
sqlite3 -header -column ~/.local/share/opencode/opencode.db \
  "SELECT id, title, directory, datetime(time_created/1000, 'unixepoch', 'localtime') AS created, datetime(time_updated/1000, 'unixepoch', 'localtime') AS updated FROM session ORDER BY time_updated DESC;"
```

按标题或目录搜索 session：

```bash
sqlite3 -header -column ~/.local/share/opencode/opencode.db \
  "SELECT id, title, directory, datetime(time_created/1000, 'unixepoch', 'localtime') AS created FROM session WHERE title LIKE '%关键词%' OR directory LIKE '%关键词%' ORDER BY time_updated DESC;"
```

统计 session 数量：

```bash
sqlite3 ~/.local/share/opencode/opencode.db "SELECT COUNT(*) FROM session;"
```
