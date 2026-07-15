# J.A.R.V.I.S Plugin Marketplace

J.A.R.V.I.S 插件市场（单仓库模式）— 所有插件在一个仓库的子目录中。

## 目录结构

```
jarvis-plugins/
  marketplace.json              # 市场清单（列出所有可用插件）
  plugins/                      # 所有插件（每个子目录 = 一个插件）
    weather/
      plugin.json               # 插件清单
      skills/weather/SKILL.md   # 技能文件（可选）
      .mcp.json                 # MCP 配置（可选）
    everything-sdk/
      ...
    speech-sense/
      ...
```

## 添加新插件

1. 在 `plugins/` 下创建新目录 `<plugin-name>/`
2. 创建 `plugin.json` + 可选的 `skills/` 和 `.mcp.json`
3. 在 `marketplace.json` 的 `plugins` 数组中添加条目，`source.type` 设为 `"github-subdir"`

## 使用方式

在 Jarvis 中执行：

```
/plugin search <关键词>          # 搜索插件
/plugin install <名称>           # 安装插件
/plugin                          # 列出已安装
/plugin uninstall <名称>         # 卸载插件
```

## 插件数量

目前 1 个插件（weather），计划中的 2 个（everything-sdk, speech-sense）。
