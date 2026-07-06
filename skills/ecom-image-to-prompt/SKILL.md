---
name: ecom-image-to-prompt
description: Analyze attached ecommerce creatives or product images and convert them into a detailed Chinese reconstruction specification plus a generator-ready positive prompt and Negative Prompt. Use when the user uploads one or more images and asks to reverse-engineer, deconstruct, recreate, imitate, or extract a prompt for an ecommerce hero, PDP/detail image, promotional poster, selling-point infographic, comparison image, usage image, trust/proof frame, packaging image, or isolated product asset, including requests such as “帮我拆这张电商图”, “反推商品详情图 Prompt”, and “这张商品图怎么复刻”. Do not use for text-only PDP planning without an image.
---

# E-commerce Image to Prompt

Convert visible image evidence into an executable ecommerce reconstruction brief. Preserve product identity and commercial layout before describing photographic style. Output analysis and prompts only; do not generate images or call external/local visual APIs.

## Load the references

Read both files before analyzing the image:

- `references/ecommerce-reconstruction.md` for classification, product locking, layout reconstruction, evidence boundaries, and anti-drift rules.
- `references/output-contract.md` for the exact nine-section Markdown interface and mode-specific field requirements.

## Inspect the input

1. Inspect every attached image directly with the available image-understanding capability. Use `view_image` for a local image path when available.
2. If no image is attached or accessible, ask the user to upload or reattach it. Do not invent an image or output a speculative Prompt.
3. For one image, analyze it directly.
4. For multiple images, treat the first image as the layout/creative reference and later images as product, packaging, Logo, or proof assets unless the user assigns different roles.
5. Record conflicts between images. Let a dedicated product asset override a partially obscured product rendering for identity details; never let it silently override the reference creative's layout.

## Select one mode

Choose exactly one primary mode:

- `reference_creative`: Select when the image already contains a designed composition such as headline, price, benefit labels, people, icons, offer, proof, or a deliberate reading path. Reconstruct the existing creative at high fidelity and preserve its aspect ratio.
- `product_asset`: Select when the input is primarily an isolated product, white-background pack shot, packaging asset, Logo, or raw material without a finished ecommerce composition. Plan one new ecommerce detail image. Use `1024×1536` as a labeled default unless the user supplies another size.

If signals are mixed, choose `reference_creative` whenever a meaningful layout and conversion hierarchy already exist. List secondary image roles separately.

## Apply the evidence gate

Use these source labels exactly:

- `Visible`: clearly observable in the image.
- `User-provided`: explicitly stated by the user.
- `Inferred`: a reversible interpretation based on visible structure or category context.
- `Default`: a Skill default used to keep the task moving.
- `Needs confirmation`: unreadable, occluded, ambiguous, conflicting, or absent.

Apply this priority: `User-provided` > `Visible` > `Inferred` > `Default`. Never convert an inference into a visible fact.

Treat price, discount, efficacy, ingredients, measurements, certifications, awards, stock codes, sales volume, reviews, test results, medical/safety claims, and packaging copy as evidence-bound. Include them only when clearly visible or user-provided. Mark unclear text as `不可辨识`; use a bracketed placeholder such as `[待确认：核心卖点]` only when the new design needs that field. Never complete cropped text from common sense.

## Reconstruct in priority order

1. Classify the ecommerce image type and its conversion job.
2. Lock product identity: count, package geometry, colors, Logo, angle, proportions, visible components, and immutable details.
3. Recover the frame skeleton: aspect ratio, zones, approximate percentages, anchors, overlaps, whitespace, and reading path.
4. Transcribe all clearly legible on-image and packaging text without rewriting it.
5. Separate visible facts, user facts, inferences, defaults, and unresolved fields.
6. Build the positive Prompt from work type to constraints: ecommerce purpose, canvas, layout, product lock, exact text, people/scene, lighting/materials, style, and fidelity constraints.
7. Build an image-specific Negative Prompt that blocks the most likely drift.

For `product_asset`, define the frame's conversion job before designing it. Do not expand the request into a full PDP sequence. Use placeholders instead of inventing missing selling points, price, proof, or reviews.

## Preserve text in the final Prompt

Insert every clearly legible requested string into the positive Prompt in quotation marks and assign its position and hierarchy. Keep `不可辨识` text out of the Prompt unless represented by a clearly labeled placeholder. Do not silently correct brand spellings or packaging copy.

When the source is a finished ecommerce creative, explicitly say `完整电商信息海报，不是纯摄影` or the equivalent image-type constraint. Photography may supply people, products, light, and texture, but must not replace the information architecture.

## Output the fixed contract

Return the following headings in this exact order and do not add a preface:

1. `## 1. 识别模式与图片类型`
2. `## 2. 电商任务诊断`
3. `## 3. 商品身份锁`
4. `## 4. 版式蓝图`
5. `## 5. 文字清单`
6. `## 6. 证据与假设`
7. `## 7. 最终中文正向 Prompt`
8. `## 8. Negative Prompt`
9. `## 9. 生成提醒`

Follow `references/output-contract.md` for required fields. Default to Chinese. Keep the positive and negative prompts ready to copy as fenced text blocks.

## Self-check before returning

- Confirm that image type is not reduced to lifestyle photography when commercial information zones are visible.
- Confirm product count and package form match the evidence; describe occluded counts as uncertain.
- Confirm every quoted hard fact appears in `Visible` or `User-provided` evidence.
- Confirm every uncertain item is marked and no blurry text was completed.
- Confirm layout percentages, positions, hierarchy, overlap, whitespace, and reading order are stated.
- Confirm the positive Prompt contains the product identity lock and all clearly legible text.
- Confirm the Negative Prompt blocks package redesign, product substitution, wrong counts, missing layout zones, random text, invented logos, and extra products.
- Confirm `product_asset` uses labeled placeholders rather than fabricated benefits or proof.
- Confirm no API, local service, or image-generation action was invoked.
