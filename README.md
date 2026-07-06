# ecom-image-to-prompt

[零基础使用指南](./docs/BEGINNER_GUIDE.zh-CN.md) · [English](./README.en.md) · [下载 v0.1.0 Skill ZIP](./dist/ecom-image-to-prompt-v0.1.0.zip) · [SHA-256](./dist/SHA256SUMS)

一个面向 Codex 的电商图片反推 Skill：上传成品电商参考图或纯商品素材，直接得到完整中文拆版规格、正向 Prompt 与 Negative Prompt。

它解决的不是“把画面描述成一段摄影提示词”，而是先锁定商品身份、版式骨架、可见文字和转化任务，再生成可以执行的电商视觉 Prompt。

## 零基础先看这里

你可以把它理解成一位“电商视觉拆解师”：

```text
上传图片 → 判断图片类型 → 锁定商品 → 拆解版式和文字 → 输出正向 Prompt + Negative Prompt → 交给生图模型
```

你不需要会写代码。第一次使用前，建议阅读 [《从一张图片到 Prompt：零基础使用指南》](./docs/BEGINNER_GUIDE.zh-CN.md)，里面包含完整链路图、母婴海报示例、安装步骤和常见问题。

## 适合什么任务

- 拆解并复刻电商主图、促销海报或商品详情图
- 从卖点信息图、对比图、步骤图、场景图、信任背书图反推 Prompt
- 根据白底商品图或包装素材规划一张新的竖版详情图
- 分析多张素材：第一张做版式参考，后续图片锁定商品、包装、Logo 或证明材料

普通的无图 PDP 策划不应触发本 Skill，可继续使用其他电商策划 Skill。

## 核心能力

- **双模式自动识别**：区分成品创意 `reference_creative` 与纯商品素材 `product_asset`
- **商品身份锁**：锁定数量、包装形态、色块、Logo、角度、比例和不可修改项
- **版式级反推**：输出画幅、区域占比、元素位置、层级、遮挡、留白和阅读路径
- **逐项文字清单**：只转录清晰可见或用户提供的文字；模糊文字标记“不可辨识”
- **严格证据规则**：不编造价格、功效、认证、销量、股票代码、评价或证明材料
- **防漂移 Negative Prompt**：阻止生活方式摄影替代、包装重设计、错误数量、礼盒替换、随机文字和额外商品
- **无需外部视觉 API**：直接使用 Codex 当前会话的图片理解能力

## 两种输入模式

| 模式 | 典型输入 | 行为 |
|---|---|---|
| `reference_creative` | 已有标题、价格、人物、商品、图标和证明栏的成品图 | 保持原画幅，高保真拆解并复刻信息层级 |
| `product_asset` | 白底商品图、透明商品素材、包装图或 Logo | 默认规划 `1024×1536` 竖版详情图；缺少卖点时保留待确认占位符 |

## 安装

### 方法一：让 Codex 安装

在 Codex 中输入：

```text
请使用 $skill-installer 安装这个 Skill：
https://github.com/willson-wen/ecom-image-to-prompt/tree/main/skills/ecom-image-to-prompt
```

### 方法二：手动安装

```bash
git clone https://github.com/willson-wen/ecom-image-to-prompt.git
mkdir -p ~/.codex/skills
cp -R ecom-image-to-prompt/skills/ecom-image-to-prompt ~/.codex/skills/
```

### 方法三：使用 ZIP

下载 [ecom-image-to-prompt-v0.1.0.zip](./dist/ecom-image-to-prompt-v0.1.0.zip)，解压后将 `ecom-image-to-prompt` 文件夹放到：

```text
~/.codex/skills/ecom-image-to-prompt
```

安装完成后重启 Codex，使新 Skill 生效。

ZIP 完整性可通过 `dist/SHA256SUMS` 校验。

## 怎么使用

### 1. 反推成品电商图

上传一张电商主图或详情图，然后输入：

```text
使用 $ecom-image-to-prompt 分析我上传的图片，输出完整拆版规格、正向 Prompt 和 Negative Prompt。
```

也可以自然地说：

```text
帮我拆这张电商图，锁定商品包装、版式和全部清晰文字，并给我可复刻的中文 Prompt。
```

### 2. 从纯商品素材规划详情图

上传白底商品图，然后输入：

```text
使用 $ecom-image-to-prompt，把这张商品素材规划成一张电商详情图。不要编造功效、价格和认证，缺少信息用待确认占位符。
```

### 3. 多图输入

默认规则：第一张图片是版式参考，后续图片是商品、包装、Logo 或证明素材。若顺序不同，请在请求中明确说明。

```text
图1是版式参考，图2是准确商品包装，图3是品牌 Logo。请使用 $ecom-image-to-prompt 进行复刻拆解。
```

## 固定输出

每次按以下顺序返回：

1. 识别模式与图片类型
2. 电商任务诊断
3. 商品身份锁
4. 版式蓝图
5. 文字清单
6. 证据与假设
7. 最终中文正向 Prompt
8. Negative Prompt
9. 生成提醒

证据会被标记为 `Visible`、`User-provided`、`Inferred`、`Default` 或 `Needs confirmation`，方便区分看得见的事实与合理推断。

## 重要边界

- 本 Skill 只分析图片并输出 Prompt，不自动生成图片。
- 无图片时只会请求上传，不会虚构 Prompt。
- 图片模糊、文字过小或商品被遮挡时，会明确标记不确定性。
- 生图模型仍可能写错密集中文或包装小字，生成后需要逐项校对。
- 第一版不调用 OpenAI API、第三方视觉 API 或本地 Bridge 服务，也不需要 API Key。

## 仓库结构

```text
.
├── README.md
├── README.en.md
├── LICENSE
├── VERSION
├── dist/
│   ├── ecom-image-to-prompt-v0.1.0.zip
│   └── SHA256SUMS
└── skills/
    └── ecom-image-to-prompt/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/
            ├── ecommerce-reconstruction.md
            └── output-contract.md
```

## License

[MIT](./LICENSE)
