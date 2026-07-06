# Ecommerce reconstruction rules

## Contents

1. Classification
2. Reconstruction priority
3. Product identity lock
4. Layout blueprint
5. Text and evidence
6. Conversion diagnosis
7. Prompt assembly
8. Anti-drift rules
9. Multiple images

## 1. Classification

Classify the primary frame before describing its style. Use one main type and optional secondary types:

- **电商促销海报**: price, discount, bundle, urgency, offer, or dominant sales headline.
- **卖点信息图**: feature/benefit labels, icons, mechanism, measurements, or ingredient callouts.
- **场景图**: product in use, buyer emotion, environment, or lifestyle context.
- **对比图**: before/after, old/new, ordinary/this product, or side-by-side criteria.
- **步骤图**: numbered actions, arrows, setup, usage, or care instructions.
- **信任背书图**: certification, award, test, expert, stock code, media, guarantee, or proof block.
- **纯商品素材**: isolated product, packaging, transparent cutout, Logo, or white-background pack shot.

A single frame may be a compound creative. Name it accordingly, for example `电商促销 / 卖点 / 场景 / 背书复合海报`. A person in the frame does not make it a lifestyle photograph when title, price, products, and proof dominate the reading path.

## 2. Reconstruction priority

Reconstruct from high-cost errors to low-cost errors:

1. Product identity and number of sale units.
2. Work type and canvas ratio.
3. Layout skeleton and reading path.
4. Exact legible text and evidence-bound facts.
5. Conversion hierarchy and emphasis.
6. People, actions, expressions, and product interaction.
7. Color, light, materials, camera, and finish.
8. Decorative props and micro-details.

Do not spend most of the Prompt on faces, lenses, or lighting while leaving title zones, prices, package form, or proof bars implicit.

## 3. Product identity lock

Record the following independently from the scene:

- **Count**: distinguish large outer pack, inner sachets, bottles, accessories, and decorative repeats. Use `多条，精确数量因遮挡无法确认` when needed.
- **Package form**: pouch, sachet, bottle, tube, carton, rounded stand-up pack, gift box, tray, blister, etc.
- **Geometry**: width/height ratio, rounded corners, cap, handle, opening, thickness, silhouette, and front-facing area.
- **Color blocking**: dominant colors and their regions, not merely a palette list.
- **Brand marks**: exact visible Logo spelling, placement, size, and contrast. Mark uncertain marks instead of inventing them.
- **Angle and orientation**: front, three-quarter, side, tilted, standing, lying, held, or partially occluded.
- **Relative scale**: product size compared with people, hands, props, and the frame.
- **Visible package elements**: mascot, window, label panel, flavor cue, key illustration, badge, or pattern.
- **Immutable details**: everything that must survive generation without redesign.

Treat dedicated product assets as the best identity source. Treat a finished creative as the best layout source.

## 4. Layout blueprint

Build the frame as a coordinate system. Estimate percentages; do not claim pixel precision unless measured.

For each zone state:

- vertical range and approximate frame share;
- left/center/right anchor;
- element size and hierarchy;
- alignment and grouping;
- overlap and occlusion relationships;
- negative space and safe margins;
- visual counterweight;
- transition to the next zone.

State the reading path as a sequence, such as `品牌 → 主标题 → 卖点标签 → 价格 → 人物互动 → 主商品 → 背书 → 底部证明栏`.

For `reference_creative`, preserve source ratio and source-specific zone proportions. For `product_asset`, use `1024×1536` as `Default` and design one coherent detail frame, not an entire page or image pack.

Common errors to block:

- allowing people to expand until they become the entire frame;
- turning cutout-style product staging into a natural tabletop photo;
- moving price away from its promotion zone;
- omitting a bottom proof bar because it looks secondary;
- replacing irregular packaging with generic cartons or gift bags;
- adding products to fill empty space;
- describing only foreground objects while missing the information hierarchy.

## 5. Text and evidence

Create a literal transcription inventory. Separate:

- brand and Logo;
- headline and subheadline;
- badge or strapline;
- price, discount, quantity, and offer;
- selling points and icon labels;
- handwritten/emotional annotation;
- certification, award, experiment, code, and proof;
- packaging text;
- legal or bottom-bar text.

For each string, record content, location, hierarchy, and confidence. Use these rules:

- Copy only clear text; preserve punctuation, numerals, currency symbols, case, and line breaks when visible.
- Mark blurred, cropped, tiny, reflective, or occluded text as `不可辨识`.
- Do not infer a full claim from one readable fragment.
- Do not replace unreadable words with category conventions.
- Do not correct apparently unusual brand spelling without user confirmation.
- Include clear text in the final positive Prompt because this Skill's contract prioritizes full reconstruction.
- Keep a short generation warning: dense Chinese may still render incorrectly.

Hard facts require `Visible` or `User-provided` support. This applies even when another ecommerce workflow would normally permit promotional invention.

## 6. Conversion diagnosis

Identify the frame's single primary job:

- stop the scroll;
- explain a differentiator;
- prove usefulness or mechanism;
- show use and emotional fit;
- reduce a trust objection;
- compare options;
- teach a step;
- communicate offer and quantity;
- close the purchase decision.

Then describe:

- the first visual hook;
- the intended buyer visible from the creative, if any;
- the belief shift created by the frame;
- the proof or reassurance used;
- the likely next reading/action cue.

Do not infer demographics, medical need, or buyer intent beyond visible/contextual evidence. Label reasonable audience interpretation as `Inferred`.

## 7. Prompt assembly

Assemble the positive Prompt in this order:

1. **Work type and objective**: full ecommerce information poster, benefit infographic, comparison frame, etc.
2. **Canvas**: exact source ratio or labeled product-asset default.
3. **Layout skeleton**: zones, percentages, anchors, hierarchy, overlaps, and reading path.
4. **Product identity lock**: count, form, geometry, colors, Logo, angle, scale, and immutable details.
5. **Exact text map**: quote every clear string and place it in the correct zone.
6. **People and scene**: identity-neutral visual description, pose, gaze, interaction, crop, and props.
7. **Lighting and material behavior**: direction, temperature, contrast, shadows, reflections, packaging finish, and skin rendering.
8. **Commercial finish**: platform-appropriate polish, information density, compositing style, icon system, color hierarchy, and legibility.
9. **Strict constraints**: required zones, no redesign, no extra units, no random text, and fidelity statement.

Prefer concrete spatial instructions over adjectives. `右上约15%红色价格区` is more useful than `醒目的价格`. `一个黄色/深蓝圆角大包装 + 多条蓝白独立条袋` is more useful than `产品丰富陈列`.

## 8. Anti-drift rules

Build the Negative Prompt from observed risks rather than a generic quality list. Cover applicable risks:

- lifestyle photograph replacing the ecommerce composition;
- missing headline, price, proof, bottom bar, comparison column, or step markers;
- package redesign, changed color blocking, altered Logo, generic box substitution, or gift-bag substitution;
- wrong product count, duplicate product, merged units, extra accessories, or invented variants;
- oversized person, cropped main pack, blocked Logo, or changed hand-product interaction;
- random Chinese/English, fake brand copy, invented badge, certification, award, review, or code;
- changed aspect ratio, loose layout, wrong reading path, excessive empty space, or decorative clutter;
- irrelevant food, plants, props, icons, watermarks, QR codes, or people;
- distorted hands, impossible packaging geometry, floating products, or inconsistent shadows.

## 9. Multiple images

Default roles:

- Image 1: layout, reading path, visual hierarchy, color direction, and creative type.
- Image 2+: product geometry, packaging copy, Logo, alternate angle, proof, certification, or supporting material.

List each assigned role in the evidence section. When sources conflict:

1. obey an explicit user assignment;
2. use the clearest dedicated asset for product identity;
3. use the first finished creative for composition;
4. mark unresolved conflicts `Needs confirmation`;
5. never merge conflicting package versions into a fictional hybrid.
