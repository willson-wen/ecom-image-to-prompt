# Output contract

## Contents

1. Universal rules
2. Fixed nine-section template
3. `reference_creative` requirements
4. `product_asset` requirements
5. Compact examples

## 1. Universal rules

- Output Chinese by default.
- Use all nine headings in the prescribed order.
- Make uncertainties visible; do not bury them inside prose.
- Put the final positive and negative prompts in separate fenced `text` blocks.
- Do not add an alternate no-text Prompt unless the user explicitly asks.
- Do not generate an image or invoke an API as part of this contract.
- If the image is absent or inaccessible, stop and request the image instead of emitting the nine sections.

## 2. Fixed nine-section template

````markdown
## 1. 识别模式与图片类型

- 模式：`reference_creative` / `product_asset`
- 主类型：...
- 次类型：...
- 输入图片角色：图1 ...；图2 ...
- 判断依据：...

## 2. 电商任务诊断

- 主要转化任务：...
- 首屏视觉钩子：...
- 阅读路径：...
- 可见目标用户：...（来源标签）
- 认知转变：从 ... 到 ...
- 证明/行动线索：...

## 3. 商品身份锁

| 字段 | 锁定内容 | 证据状态 |
|---|---|---|
| 商品数量 | ... | Visible / Needs confirmation |
| 包装形态 | ... | ... |
| 主色与色块 | ... | ... |
| Logo/品牌 | ... | ... |
| 角度与朝向 | ... | ... |
| 相对比例 | ... | ... |
| 不可修改项 | ... | ... |
| 不确定项 | ... | ... |

## 4. 版式蓝图

- 画幅：...
- 区域划分：...
- 元素坐标：...
- 层级：...
- 遮挡关系：...
- 留白与安全边距：...
- 视觉平衡：...
- 最终阅读顺序：...

## 5. 文字清单

| 层级/类型 | 原文 | 位置 | 清晰度/处理 |
|---|---|---|---|
| ... | “...” | ... | 清晰，写入 Prompt |
| ... | 不可辨识 | ... | 不补写 |

## 6. 证据与假设

- `Visible`: ...
- `User-provided`: ...
- `Inferred`: ...
- `Default`: ...
- `Needs confirmation`: ...

## 7. 最终中文正向 Prompt

```text
...
```

## 8. Negative Prompt

```text
...
```

## 9. 生成提醒

密集中文和包装小字仍可能被生图模型写错；本 Prompt 已按可见证据保留文字与位置，但成图后仍需逐项校对。
````

If a source category has no content, write `无` rather than removing it. Do not label obvious visible facts as inferred.

## 3. `reference_creative` requirements

In section 1:

- classify compound ecommerce frames precisely;
- preserve the source aspect ratio;
- distinguish creative/layout references from later product/proof assets.

In sections 3-5:

- lock sale-unit count separately from internal pieces;
- state uncertainty when products overlap or leave the frame;
- map top/middle/bottom and left/center/right regions with approximate percentages;
- transcribe every clearly legible title, price, quantity, benefit, certification, code, and package string;
- record visible but unreadable strings as `不可辨识`.

In section 7:

- begin with the exact image category and `完整电商信息海报，不是纯摄影` for a designed composite poster;
- preserve information density, title zone, offer zone, person/product zone, and proof/footer zone;
- quote all clear text and assign its position;
- lock the product before describing people, props, and lighting;
- repeat strict constraints at the end.

In section 8, include source-specific failure modes. For a poster with one large pack and several sachets, explicitly block cartons, gift bags, three-box substitutions, and extra sale units.

## 4. `product_asset` requirements

In section 1:

- classify the input as product/packaging material, not as an already designed poster;
- identify whether it is front-facing, three-quarter, side, cropped, transparent, or white-background.

In section 2:

- choose one frame job supported by visible product characteristics and user context;
- mark the buyer and belief shift as `Inferred` when not provided;
- do not invent a full product strategy.

In section 3:

- lock every visible physical feature, material, color block, Logo, label panel, cap, port, accessory, and proportion;
- mark hidden back/side details as `Needs confirmation`.

In section 4:

- use `1024×1536 竖版详情图（Default）` unless the user gave a size;
- design one top-to-bottom frame with a clear product anchor and readable information zones;
- preserve enough negative space for unconfirmed copy placeholders.

In sections 5-7:

- use only visible packaging text and user-provided copy;
- insert `[待确认：主标题]`, `[待确认：核心卖点]`, `[待确认：证明材料]`, or `[待确认：价格/优惠]` where needed;
- never turn visible colors, shape, or category cues into an efficacy claim;
- exclude missing fields rather than filling them with common category slogans when the frame does not need them.

In section 8, block invented price, efficacy, certification, award, review, ingredients, Logo, packaging copy, extra variants, accessories, and package redesign.

## 5. Compact examples

### Finished mother-and-child supplement poster

Correct classification:

```text
模式：reference_creative
主类型：电商促销 / 卖点信息 / 场景 / 信任背书复合海报
关键结构：顶部标题与卖点、右上价格、中下部母子与主商品、右侧奖杯、底部证明栏
商品锁：一个黄色/深蓝圆角大包装 + 多条蓝白独立条袋；条袋精确数量因遮挡无法确认
清晰核心文字：“124纳米有机柠檬酸钙”、“¥159到手”、“22条”、“永安康健 股票代码 002365”
作品约束：完整电商信息海报，不是纯摄影
```

Incorrect interpretations:

- `温馨母子生活方式摄影`
- `三盒营养品和两个手提礼盒`
- treating every partially visible sachet as an exact count
- inventing unreadable bottom proof copy

### White-background product pack shot

Correct behavior:

```text
模式：product_asset
画幅：1024×1536 竖版详情图（Default）
标题：[待确认：主标题]
卖点：[待确认：核心卖点]
证明：[待确认：证明材料]
```

Incorrect behavior:

- inventing `销量第一`, `医师推荐`, `99.9%有效`, a price, or a certification;
- redesigning the package into a premium gift box;
- claiming a benefit solely because the pack color resembles a category convention.
