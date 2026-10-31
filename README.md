# ROC 与校准曲线证据约束型自检 Skill

这是一个可安装的 Agent Skill，用于降低多模态 AI 解读 ROC 曲线和校准曲线时的信息遗漏、数值误读、统计概念混淆、验证集混淆、过度推断和前后矛盾。

它是纯指令型插件，不执行代码，不联网，也不需要 API Key。安装后，支持 Agent Skills 的智能体可以自动发现并调用它；不支持 Skill 的平台可以使用仓库中的跨平台 Prompt。

## 一键下载

打开仓库页面，选择 **Code → Download ZIP**：

https://github.com/RANQQQQQ/ai_literacy_skill

下载的整个 ZIP 就是安装包。不要只下载 `SKILL.md`，否则 ROC 和校准曲线的专用规则不会随包安装。

## 包结构

```text
ai_literacy_skill/
├── plugin.json                         # Agent Plugins 可移植清单
├── .codex-plugin/plugin.json           # Codex 兼容清单
├── .claude-plugin/plugin.json          # Claude Code 兼容清单
├── skills/
│   └── audit-roc-calibration-figures/
│       ├── SKILL.md
│       └── references/
│           ├── roc.md
│           └── calibration.md
└── prompts/
    └── 跨平台自检Prompt.md
```

## 安装方式

### 支持“从仓库安装插件”的智能体

在插件或 Skill 设置中选择 **Add from repository / 从仓库添加**，输入：

```text
https://github.com/RANQQQQQ/ai_literacy_skill
```

安装后新建对话，再上传图像并要求使用 `audit-roc-calibration-figures`。

### 支持 ZIP 上传的智能体

1. 从 GitHub 下载整个仓库 ZIP；
2. 在插件、Skills 或扩展页面选择上传 ZIP；
3. 如果平台要求先解压，请选择解压后包含 `plugin.json` 的顶层文件夹；
4. 安装后新建对话。

### 只支持 Agent Skills 文件夹的平台

解压 ZIP，将下面这个完整文件夹复制到该平台的 Skills 目录：

```text
skills/audit-roc-calibration-figures/
```

必须同时保留 `SKILL.md` 和 `references/`。

### 不支持 Skill 或插件的平台

打开 [`prompts/跨平台自检Prompt.md`](prompts/%E8%B7%A8%E5%B9%B3%E5%8F%B0%E8%87%AA%E6%A3%80Prompt.md)，复制全文作为首条提示词，然后上传图像。这种方式能复用规则，但不属于真正安装。

## 使用示例

上传包含 ROC 曲线或校准曲线的图片后输入：

```text
请使用 audit-roc-calibration-figures，对这张图进行证据约束型觃读和自检。
只依据我提供的材料回答；无法辨认或无法确定的信息不要猜测。
```

可以同时提供图注、正文摘录或原始统计输出。Skill 会区分图像事实、合理解释和当前材料无法确定的信息。

## 核心流程

```text
图表类型判断
→ 信息完整性清点
→ 关键数值原样转录
→ 调用 ROC / 校准专用规则
→ 证据分级
→ 结论权限检查
→ 前后一致性复核
→ 修正后输出
```

- **A：直接事实**——图中或用户材料明确显示；
- **B：合理解释**——由图形关系和统计规则支持；
- **C：无法确定**——需要图注、正文、数据、代码或额外检验。

## 能力边界

- 专用规则目前只覆盖 ROC 曲线和校准曲线；其他图表只能做通用信息清点。
- Skill 能降低常见误读风险，但不能保证回答必然正确。
- AI 自检不等于独立事实验证。正式引用前仍应核对论文正文、原始数据或统计代码。
- 精确数值应优先以作者的原始统计输出为准，而不是从低分辨率图片估读。

## 版本

当前版本：`0.1.0`


