# ecom-image-to-prompt

[中文说明](./README.md) · [Download v0.1.0 Skill ZIP](./dist/ecom-image-to-prompt-v0.1.0.zip) · [SHA-256](./dist/SHA256SUMS)

A Codex Skill that turns an uploaded ecommerce creative or isolated product asset into a detailed Chinese reconstruction specification, positive prompt, and Negative Prompt.

Instead of reducing a designed ecommerce image to a generic photography description, it locks product identity, layout structure, visible copy, and conversion intent before writing the final prompt.

## Use cases

- Reverse-engineer ecommerce hero images, promotional posters, and PDP/detail images
- Reconstruct selling-point infographics, comparisons, steps, lifestyle scenes, and trust/proof frames
- Plan a new vertical detail image from a white-background product or packaging asset
- Combine multiple inputs: one layout reference plus product, packaging, Logo, or proof assets

Text-only PDP planning without an image is intentionally outside this Skill's trigger scope.

## Highlights

- Automatically selects `reference_creative` or `product_asset` mode
- Locks product count, package form, color blocking, Logo, angle, scale, and immutable details
- Reconstructs aspect ratio, layout zones, hierarchy, overlaps, whitespace, and reading path
- Transcribes only clearly visible or user-provided copy; unclear copy is marked unreadable
- Never invents price, efficacy, certification, sales volume, reviews, codes, or proof
- Produces an image-specific Negative Prompt to prevent package and layout drift
- Uses Codex's current-session image understanding; no external vision API or API key is required

## Install

### Install with Codex

```text
Use $skill-installer to install this Skill:
https://github.com/willson-wen/ecom-image-to-prompt/tree/main/skills/ecom-image-to-prompt
```

### Manual installation

```bash
git clone https://github.com/willson-wen/ecom-image-to-prompt.git
mkdir -p ~/.codex/skills
cp -R ecom-image-to-prompt/skills/ecom-image-to-prompt ~/.codex/skills/
```

### ZIP installation

Download [ecom-image-to-prompt-v0.1.0.zip](./dist/ecom-image-to-prompt-v0.1.0.zip), extract it, and place the resulting folder at:

```text
~/.codex/skills/ecom-image-to-prompt
```

Restart Codex after installation so the new Skill is discovered.

Verify the ZIP against `dist/SHA256SUMS` if needed.

## Usage

Upload an image and say:

```text
Use $ecom-image-to-prompt to analyze my uploaded image and return the complete layout specification, positive prompt, and Negative Prompt.
```

For multiple images, the first image is treated as the creative/layout reference and later images as product, packaging, Logo, or proof assets unless you assign different roles.

## Fixed output contract

1. Recognition mode and image type
2. Ecommerce task diagnosis
3. Product identity lock
4. Layout blueprint
5. Text inventory
6. Evidence and assumptions
7. Final Chinese positive prompt
8. Negative Prompt
9. Generation reminder

Evidence is labeled `Visible`, `User-provided`, `Inferred`, `Default`, or `Needs confirmation`.

## Limitations

- This Skill analyzes images and writes prompts; it does not generate images.
- Without an accessible image, it asks for one instead of inventing a prompt.
- Dense Chinese and tiny packaging copy may still be misspelled by image-generation models.
- Version 0.1.0 does not call the OpenAI API, third-party vision APIs, or local bridge services.

## License

[MIT](./LICENSE)
