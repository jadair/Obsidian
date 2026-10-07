Source: [Drexel University Identity Guidelines: Colors](https://drexel.edu/identity/drexel/color)

This file is a working reference for future design iterations in this project. It is based on Drexel's official identity guidance and adapted for digital landing-page work.

## 1. Primary Brand Colors

These are the core colors that should anchor the design.


| Role | Official Name | Print | Digital HEX |

| Primary dark | Drexel Blue | Pantone 294C | `#07294D` |

| Primary accent | Drexel Gold | Pantone 7548C | `#FFC600` |

  

## 2. Official Supporting Colors


Use these as secondary accents only. Drexel's guidance indicates that complementary colors should be used sparingly.

  

### Dark accents

| Print | HEX | Notes |

| --- | --- | --- |

| PMS 7691C | `#006699` | strong secondary blue |

| PMS 7427C | `#971B2F` | deep burgundy accent |

| PMS 384C | `#949300` | olive accent |

| PMS 138C | `#DE7C00` | deep orange accent |

  

### Light accents

  | Print | HEX | Notes |

| --- | --- | --- |

| PMS 284C | `#6CACE4` | light Drexel-adjacent blue |

| PMS 7597C | `#D14124` | bright warm red-orange |

| PMS 583C | `#B7BF10` | light olive-green |

| PMS 1495C | `#FF8F1C` | bright orange |

  

### Neutrals
|Print | HEX | Notes |

| --- | --- | --- |

| Cool Gray 6C | `#333333` | dark neutral for text |

| PMS 5665C | `#BAC5B9` | muted soft green-gray |

| Warm Gray 3C | `#BFB8AF` | warm neutral |

| PMS 427C | `#D0D3D4` | light cool neutral |

  

## 3. Rules From Drexel Identity Guidance

  

- Use `#07294D` and `#FFC600` as the dominant brand colors.

- For digital work, use Drexel's approved HEX values directly.

- Do not rely on automatic HEX conversions from Pantone or CMYK values.

- Complementary colors should be limited accents, not replacements for blue and gold.

- If a design will be printed, match to the coated Pantone references rather than improvised conversions.

  

## 4. Recommended Project Palette

  

This is the practical palette I recommend using for the landing pages going forward.

  

### Core UI palette

  

| Usage | HEX |

| --- | --- |

| Brand navy | `#07294D` |

| Brand gold | `#FFC600` |

| Secondary blue | `#6CACE4` |

| Deep supporting blue | `#006699` |

| Main text on light backgrounds | `#333333` |

| Soft border / cool neutral | `#D0D3D4` |

| Warm neutral surface | `#BFB8AF` |

| Soft atmospheric neutral | `#BAC5B9` |

| Off-white background | `#F7F8F6` |

| White card background | `#FFFFFF` |

  

### Extended surfaces derived for UI use

  

These are not official Drexel named colors, but they are safe utility tones built around the official palette.

  

| Usage | HEX | Why |

| --- | --- | --- |

| Pale navy tint | `#EAF1F8` | light section backgrounds |

| Gold tint | `#FFF4CC` | subtle highlight panels |

| Dark hero background | `#061F3B` | near-brand dark surface |

| Muted body text | `#5E6875` | softer paragraph color |

  

## 5. Color Usage Guidelines for This Project

  

### Overall balance

  

- Keep Drexel Blue as the structural color.

- Use Drexel Gold as the emphasis color, not the background color for entire sections.

- Let white, near-white, and soft neutral fields create breathing room.

- Use supporting accent colors only for small moments: badges, data highlights, hover states, charts, or category tags.

  

### Recommended distribution

  

- `60-70%` neutral/light backgrounds

- `20-30%` Drexel Blue and navy-based surfaces

- `5-10%` Drexel Gold and accent colors

  

### Where each color should go

  

#### Drexel Blue `#07294D`

  

- header/footer anchors

- hero overlays

- primary buttons

- key headlines on light backgrounds

- major section dividers

  

#### Drexel Gold `#FFC600`

  

- CTAs

- underline accents

- tags

- active states

- small callout bars

  

#### Light Blue `#6CACE4`

  

- secondary highlights

- info chips

- hover fills

- supporting diagrams or data cards

  

#### Neutral tones

  

- cards

- body copy

- rules and borders

- low-contrast background transitions

  

## 6. What to Avoid

  

- Do not replace Drexel Blue with a different dominant blue.

- Do not overuse gold as a large-area background.

- Do not mix too many accent colors in one screen.

- Do not use saturated colors that are not part of the official Drexel system unless there is a strong functional reason.

- Do not create gradients that obscure the Drexel palette.

- Do not use low-contrast gold text on white backgrounds.

  

## 7. Accessibility Notes

  

- Prefer white text on `#07294D`.

- Prefer `#333333` or `#07294D` for body copy on light backgrounds.

- Use gold mainly for fills, borders, icons, or short labels rather than long passages of text.

- Test contrast whenever using `#6CACE4`, `#BAC5B9`, or `#BFB8AF` behind text.

  

## 8. CSS Starter Tokens

  

```css

:root {

--drexel-blue: #07294D;

--drexel-gold: #FFC600;

--drexel-blue-alt: #006699;

--drexel-blue-light: #6CACE4;

--drexel-red-accent: #D14124;

--drexel-orange: #FF8F1C;

--drexel-olive: #B7BF10;

--drexel-text: #333333;

--drexel-neutral-soft: #D0D3D4;

--drexel-neutral-warm: #BFB8AF;

--drexel-neutral-sage: #BAC5B9;

--surface-white: #FFFFFF;

--surface-offwhite: #F7F8F6;

--surface-blue-tint: #EAF1F8;

--surface-gold-tint: #FFF4CC;

--text-muted: #5E6875;

}

```

  

## 9. Design Direction for This Site

  

For this Advanced Therapeutics work, the safest ongoing approach is:

  

- use Drexel Blue for trust, structure, and institutional identity

- use Gold for direction and emphasis

- keep layouts mostly light and breathable

- reserve accent colors for research, events, or category-level differentiation

- make the page feel contemporary and premium without drifting away from Drexel's official brand system

