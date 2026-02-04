# Nordic MathML Guidelines Checklist

Validation checklist for MathML content in EPUB publications.

## When to Use MathML

### Must Use MathML

- [ ] All mathematical expressions, even simple ones like `4 − 1 = 3`
- [ ] Variables and parameters (e.g., x, y, α)
- [ ] Greek letters in STEM books
- [ ] Variables with accents/bars (e.g., x̄, ŷ)
- [ ] Variables with indexes (e.g., β₁)
- [ ] Numbers with minus sign (e.g., −4)
- [ ] Units with exponents, division, or Greek letters (e.g., m/s²)
- [ ] Chemical formulas (when MathML used elsewhere for chemistry)

### Should NOT Use MathML

- [ ] Non-negative numbers without context (3, 5.2)
- [ ] Units in plain text without operators (10 m)
- [ ] Years, dates, time periods
- [ ] ISBN, phone numbers, addresses
- [ ] Page numbers, chapter references
- [ ] Results like scores (MANU–LFC: 3–2)

## Math Element Requirements

### Namespace Declaration

```xml
<math xmlns="http://www.w3.org/1998/Math/MathML">
```

- [ ] Namespace declared on every `<math>` element
- [ ] No `m:` prefix (deprecated practice)

### Display Attribute

- [ ] Inline math: no `display` attribute (default is inline)
- [ ] Block math: `display="block"`
- [ ] Inline-block: use `displaystyle="true"` on encompassing element

### Deprecated Elements - MUST NOT USE

- [ ] No `<mfenced>` (use `<mo>` for fences instead)
- [ ] No `<mlabeledtr>` (use `<mtable>` with label in first `<mtd>`)
- [ ] No `alttext` attribute
- [ ] No `altimg` attribute

## Token Elements

### `<mn>` - Numbers

- [ ] All numeric characters including decimals
- [ ] Decimal separator included in same `<mn>`: `<mn>3,14</mn>`
- [ ] Thousand separator included: `<mn>89 000</mn>`
- [ ] Use non-breaking space for thousand separator: `&nbsp;`

### `<mo>` - Operators

- [ ] Mathematical operators: +, −, ·, /
- [ ] Parentheses and brackets: (, ), {, }, [, ]
- [ ] Percentage sign: `<mo>&#x25;</mo>`
- [ ] Comma as separator (not decimal): `<mo>,</mo>`
- [ ] Accents/bars over variables: `<mo>&#8254;</mo>` (overline)

### `<mi>` - Identifiers

- [ ] Single-letter variables: `<mi>x</mi>`
- [ ] Greek letters: `<mi>α</mi>`
- [ ] Function names: `<mi>sin</mi>`, `<mi>log</mi>`
- [ ] Units: `<mi mathvariant="normal">m</mi>`
- [ ] Multi-letter units as single element: `<mi>Nm</mi>`
- [ ] Ellipsis: `<mi>…</mi>`

### `<mtext>` - Text

Use sparingly, only when visually required:
- [ ] Text in tabular math (equation solving)
- [ ] Notation labels: `<mtext>numerator</mtext>`
- [ ] Subscript text: `<msub><mi>g</mi><mtext>weight</mtext></msub>`
- [ ] Punctuation at end of expressions: `<mtext>.</mtext>`

Avoid using `<mtext>` for:
- [ ] Explanatory text between expressions (use regular HTML)
- [ ] Text that can be outside `<math>` element

## Layout Elements

### `<mrow>` - Grouping

- [ ] Used to group multi-element numerators/denominators
- [ ] Used inside `<msup>`, `<msub>`, `<msubsup>` for complex scripts
- [ ] NOT used when unnecessary (avoid over-grouping)

### `<mfrac>` - Fractions

```xml
<mfrac>
  <mrow>numerator</mrow>
  <mrow>denominator</mrow>
</mfrac>
```

- [ ] Two children: numerator, denominator
- [ ] Binomials use `linethickness="0"`

### `<msqrt>` and `<mroot>` - Roots

- [ ] `<msqrt>` for square roots
- [ ] `<mroot>` for other roots: first child = radicand, second = index

### `<msub>`, `<msup>`, `<msubsup>` - Scripts

- [ ] `<msub>`: base, subscript
- [ ] `<msup>`: base, superscript
- [ ] `<msubsup>`: base, subscript, superscript (in that order)

### `<munder>`, `<mover>`, `<munderover>` - Under/Over

- [ ] `<munder>`: base, underscript
- [ ] `<mover>`: base, overscript
- [ ] `<munderover>`: base, underscript, overscript

Common uses:
- [ ] Summation limits: `<munder><mo>∑</mo><mrow>...</mrow></munder>`
- [ ] Vector arrows: `<mover><mi>x</mi><mo>→</mo></mover>`
- [ ] Bar notation: `<mover><mi>x</mi><mo>&#8254;</mo></mover>`

### `<mmultiscripts>` - Multiple Scripts

For prescripts and multiple postscripts:
```xml
<mmultiscripts>
  <mi>A</mi>           <!-- base -->
  <mi>m</mi>           <!-- post-subscript -->
  <mi>n</mi>           <!-- post-superscript -->
  <mprescripts/>
  <mi>q</mi>           <!-- pre-subscript -->
  <mi>t</mi>           <!-- pre-superscript -->
</mmultiscripts>
```

- [ ] Base element first
- [ ] Post-scripts in sub/super pairs
- [ ] `<mprescripts/>` before prescripts
- [ ] Empty positions use `<mrow></mrow>`

## Tabular Math

### When to Use `<mtable>`

- [ ] Matrices and determinants
- [ ] Piecewise functions
- [ ] Systems of equations
- [ ] Equation solving notation
- [ ] Labeled equations

### Structure

```xml
<mtable>
  <mtr>
    <mtd>cell 1</mtd>
    <mtd>cell 2</mtd>
  </mtr>
</mtable>
```

- [ ] `<mtr>` for rows
- [ ] `<mtd>` for cells
- [ ] Use `rowspan` and `columnspan` (not `colspan`) when needed

### Labeled Equations

```xml
<math id="equation-0" tabindex="0">
  <mtable>
    <mtr>
      <mtd intent=":equation-label"><mtext>(1.4)</mtext></mtd>
      <mtd>equation content</mtd>
    </mtr>
  </mtable>
</math>
```

- [ ] Label in first `<mtd>` of row (regardless of visual position)
- [ ] `intent=":equation-label"` on label cell
- [ ] `id="equation-[x]"` on `<math>` element
- [ ] `tabindex="0"` on `<math>` element
- [ ] References use `<a role="doc-backlink" href="#equation-x">`

## Invisible Operators

Use for disambiguation:

| Character | Code | Use |
|-----------|------|-----|
| Invisible times | `&#x2062;` | Implicit multiplication |
| Function application | `&#x2061;` | Function of argument |
| Invisible plus | `&#x2064;` | Mixed number parts |
| Invisible comma | `&#x2063;` | Implicit separator |

Example - number with unit:
```xml
<mn>100</mn>
<mo rspace="0.25em">&#x2062;</mo>
<mi mathvariant="normal" intent=":unit">m</mi>
```

## Special Characters

### Must Use Correct Unicode

Common confusions to check:
- [ ] Greek γ (U+03B3) vs Latin y
- [ ] Greek ρ (U+03C1) vs Latin p
- [ ] Greek χ (U+03C7) vs Latin x
- [ ] Micro µ (U+00B5) vs Greek μ (U+03BC)
- [ ] Prime ′ (U+2032) vs apostrophe ' (U+0027)
- [ ] Minus − (U+2212) vs hyphen - (U+002D)
- [ ] Derivative ⅆ (U+2146) vs ordinary d

### Escaping in MathML

- [ ] `&amp;` for &
- [ ] `&lt;` for <
- [ ] `&gt;` for >
- [ ] `&quot;` for "
- [ ] `&apos;` for '

## Chemistry in MathML

```xml
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>H</mi>
    <mn>2</mn>
  </msub>
  <mi>O</mi>
</math>
```

- [ ] Each element symbol in `<mi>`
- [ ] Subscripts for atom counts
- [ ] `<mmultiscripts>` for isotopes
- [ ] `<mo>` for reaction arrows (→)

## Content as Images

When MathML cannot represent content:
- [ ] Capture as image
- [ ] Use `alt="equation"` or `alt="drawing"`
- [ ] Provide MathML in image description where possible
- [ ] Use `<menclose notation="updiagonalstrike">` for crossed-out math

## Validation Points

### Common Errors

- [ ] Missing namespace declaration
- [ ] Using deprecated `<mfenced>`
- [ ] Wrong character (hyphen vs minus, etc.)
- [ ] Missing `mathvariant="normal"` on single-letter units
- [ ] Incorrect order in `<msubsup>` (sub before super)
- [ ] Text split into individual `<mi>` instead of `<mtext>`
- [ ] Manual numbering instead of `<ol>` equivalent

### Recommended Tools

- Nordic EPUB Validator
- [MathML Validator by Jan Martin Kvile](https://kvile.com/kvalidator/index.html)
