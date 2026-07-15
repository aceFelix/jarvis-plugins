# J.A.R.V.I.S Plugin Marketplace

J.A.R.V.I.S 官方插件市场 —— 安装 J.A.R.V.I.S 后即可使用，无需额外配置。

## 前置条件

- 已安装 [J.A.R.V.I.S](https://github.com/aceFelix/J.A.R.V.I.S) 个人 AI 助手
- Jarvis 运行正常（`jarvis` 或 `python -m agent.main`）

## 使用方式

在 Jarvis 对话中输入斜杠命令：

```bash
# 搜索插件
/plugin search weather

# 安装插件
/plugin install weather

# 查看已安装
/plugin

# 卸载插件
/plugin uninstall weather
```

安装后输入 `/reset` 生效（无需退出 Jarvis）。Jarvis 模型也可以自动调用 `MarketSearch` 工具搜索插件。

## 插件列表

| 插件 | 说明 | 版本 |
|------|------|------|
| `weather` | 天气查询（wttr.in + Open-Meteo，免费免 Key） | 1.0.0 |
| `everything-sdk` | Everything 引擎高速本地文件搜索 | 1.0.0 |
| `speech-sense` | 语音感知 —— 增强语音对话体验 | 1.0.0 |

## 插件结构

```
jarvis-plugins/
  marketplace.json              # 市场清单
  plugins/
    <plugin-name>/
      plugin.json               # 插件清单（name, version, skills, mcp_servers）
      skills/                   # SKILL.md 技能文件（注入系统提示词）
      .mcp.json                 # MCP server 配置（可选）
```

## 贡献插件

欢迎提交 PR 将自己的技能包加入市场。

1. Fork 本仓库
2. 在 `plugins/` 下创建 `<your-plugin>/` 目录，包含 `plugin.json` 和 `skills/`
3. 在 `marketplace.json` 的 `plugins` 数组中添加条目：

```json
{
  "name": "your-plugin",
  "description": "一句话描述",
  "version": "1.0.0",
  "author": "your-name",
  "source": {
    "type": "github-subdir",
    "repo": "aceFelix/jarvis-plugins",
    "subdir": "plugins/your-plugin",
    "ref": "master"
  }
}
```

4. 提交 PR

### plugin.json 格式

```json
{
  "name": "your-plugin",
  "description": "插件描述",
  "version": "1.0.0",
  "author": "your-name",
  "skills": ["skill-dir-name"],
  "mcp_servers": ["mcp-server-name"]
}
```

### SKILL.md 格式

标准 YAML frontmatter + Markdown 正文：

```markdown
---
name: skill-name
description: 一句话描述
when_to_use: 何时使用此技能
trigger_words: 触发词1, 触发词2
---

# Skill Title

技能提示词正文，会被注入到 Jarvis 的系统提示词中。
```

### .mcp.json 格式

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "@scope/package"]
    }
  }
}
```

## FAQ

**Q: 安装插件后需要重启吗？**
A: 输入 `/reset` 即可，不必退出 Jarvis。

**Q: 如何知道我安装了哪些插件？**
A: 输入 `/plugin` 查看已安装列表。

**Q: 插件更新后如何同步？**
A: 先 `/plugin uninstall <name>` 再 `/plugin install <name>` 即可获取最新版本。
