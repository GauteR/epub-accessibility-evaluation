# NLB Production MathML Checklist

Validation checklist for MathML content against NLB production requirements (202202-mathml-requirements-nlb-production.tex). Used for talking books, TTS, and NLB distribution pipelines.

Reference: [mathml-guidelines archive](https://github.com/nlbdev/mathml-guidelines/blob/main/archive/202202-mathml-requirements-nlb-production.tex).

## Fundamental Requirements

### MathML Structure

- [ ] All mathematical expressions use **MathML Presentation Markup** (MathML 3.0 2nd Edition).
- [ ] Every `<math>` has an ancestor with **xml:lang** (e.g. `<html xml:lang="en">` or `<div xml:lang="no">`); `<math>` itself must not have xml:lang.
- [ ] Use **numeric XML entities** for characters (e.g. &#8289; not ApplyFunction).

### Default Markup Frame

```xml
<m:math xmlns:m="http://www.w3.org/1998/Math/MathML"
  alttext="[AsciiMath markup]"
  altimg="[Image path]"
  display="[block|inline]">
  <m:semantics>
    <m:mrow>
      [MathML markup]
    </m:mrow>
  </m:semantics>
</m:math>
```

- [ ] Each expression is wrapped in `<math>` → `<semantics>` → `<mrow>` (markup inside inner mrow).
- [ ] **alttext** on `<math>` contains AsciiMath that represents the expression.
- [ ] **altimg** on `<math>` where an image path is applicable.
- [ ] **display** attribute present and set to either `block` or `inline`.

### Display Attribute

- [ ] **display** is always explicitly `block` or `inline` (no omission).
- [ ] If `<math>` has a sibling that is a non-empty text node or an inline element (a, abbr, bdo, br, code, dfn, em, img, kbd, q, samp, span, strong, sub, sup), use `display="inline"`.
- [ ] If `<math>` is the only node in an inline context (e.g. alone in a paragraph), use `display="block"` instead of inline.
- [ ] Otherwise use `display="block"`.

## Invisible Operators

Use numeric entities; required where applicable to avoid ambiguity.

| Use | Numeric entity |
| --- | ---------------- | ------------------ |
| Function application | &#8289; |
| Invisible multiplication | &#8290; |
| Invisible separator | &#8291; |
| Invisible addition | &#8292; |

- [ ] Multiplication between expressions (e.g. (x+y)(x-y), 2 sin α) uses &#8290; (InvisibleTimes).
- [ ] Function application (e.g. f(x), sin α) uses &#8289; (ApplyFunction) between function name and argument.

## Comparison Operators

- [ ] Less than: `<mo>&#60;</mo>` (not literal &lt;)
- [ ] Greater than: `<mo>&#62;</mo>` (not literal &gt;)
- [ ] Less than or equal: `<mo>&#8804;</mo>`
- [ ] Greater than or equal: `<mo>&#8805;</mo>`

## Parentheses and Fences

- [ ] **Do not** use `<mo>(</mo>` / `<mo>)</mo>` for parentheses; use **mfenced**.
- [ ] Round brackets: `<mfenced open="(" close=")">` with content inside; multiple items inside an `<mrow>`.
- [ ] Square brackets: `<mfenced open="[" close="]">`
- [ ] Curly brackets: `<mfenced open="{" close="}">`
- [ ] Absolute value: `<mfenced open="|" close="|">` (both attributes value is `|`).

## Numbers and Decimals

- [ ] Decimal in a **single** `<mn>` (e.g. `<mn>20,0</mn>` or `<mn>20.0</mn>`); do not split into `<mn>20</mn><mo>,</mo><mn>0</mn>`.
- [ ] **No thousand separators** in `<mn>`; use `<mn>164000</mn>` not separate digits with space or mtext (TTS would split into 164 and 0).

## Token Elements

### Spaces

- [ ] No spaces inside `<mi>`, `<mo>`, or `<mn>`; use `<mspace>` for visual spacing.
- [ ] No `<mtext>` containing only a single space (except special chemistry isotope case); use `<mspace>`.

### Identifiers and Text

- [ ] Identifiers (variables, function names from a known set) in `<mi>`.
- [ ] Plain text (e.g. "All the values of A") in `<mtext>`.
- [ ] Do **not** split obvious words into single letters (e.g. "mean" as m, e, a, n in separate mi); use `<mtext>mean</mtext>` or `<mtext>` inside mrow.

## Named Functions

- [ ] Structure: `<mrow>` with **exactly three** children: (1) `<mi>` function name, (2) `<mo>&#8289;</mo>`, (3) element representing the argument(s).
- [ ] For expressions like cos 2x, the argument must be one element (e.g. `<mrow><mn>2</mn><mo>&#8290;</mo><mi>x</mi></mrow>`), not three separate siblings after the mo.

## Functions with One or Two Arguments

- [ ] One argument: `<mrow><mi>f</mi><mo>&#8289;</mo><mfenced open="(" close=")">[one child]</mfenced></mrow>`.
- [ ] Two or more arguments: same but mfenced has two or more children (commas auto-inserted).

## Lower Indices (msub)

- [ ] Base in `<mrow>` with single letter (Greek or a–z, A–Z) in `<mi>`; subscript numeric in `<mn>` or symbolic in `<mrow>` with `<mi>`.

## Degrees

- [ ] Positive: `<mrow><mn>value</mn><mo>&#176;</mo></mrow>` (degree symbol &#176;); do not use msup for degree.
- [ ] Negative: `<mrow><mrow><mo>-</mo><mn>value</mn></mrow><mo>&#176;</mo></mrow>`.
- [ ] Gradians (e.g. 50^g): `<msup><mn>50</mn><mtext>g</mtext></msup>` (or msup with minus mrow for negative).

## Roots

- [ ] Square root: `<msqrt>` with one child (or multiple direct children for radicand).
- [ ] Higher-order root: `<mroot>` with exactly two children (radicand, then index).

## Fractions

- [ ] Use `<mfrac>` for fractions (not mn/mo/mn with /).
- [ ] Slash-style: use `bevelled="true"` on mfrac when numerator and denominator are separated by slash.
- [ ] Horizontal line: omit bevelled when a horizontal line is required.

## Vectors

- [ ] Arrow notation: `<mover>[single element for vector]<mo>&#8594;</mo></mover>` (right arrow &#8594;).
- [ ] Bold notation: `<mi mathvariant="bold">` (or mathvariant string containing "bold", e.g. bold-italic, bold-sans-serif).

## Limits and Derivatives

- [ ] Limit: `<mrow><munder><mo>lim</mo>[condition]</munder><mo>&#8289;</mo>[expression]</mrow>`.
- [ ] Lagrange (prime): `<mrow><msup><mi>f</mi><mo>&#8242;</mo></msup><mo>&#8289;</mo><mfenced>...</mfenced></mrow>`; second derivative &#8243;, third &#8244;.
- [ ] Leibniz (d/dx): differential d as `<mo>&#8518;</mo>` (or &#8517; for italic d in denominator); structure mfrac with numerator mrow (&#8518; + function) and denominator mrow (&#8518; + variable).

## Integrals

- [ ] Integral signs: &#8747; (int), &#8748; (iint), &#8749; (iiint), &#8750; (contour).
- [ ] With integration variable: after integrand, `<mrow><mo>&#8517;</mo><mi>variable</mi></mrow>`.
- [ ] Definite: `<munderover>` with integral sign, lower limit, upper limit; then integrand; then d(variable) mrow.

## Matrices

- [ ] Use `<mfenced>` with open/close around `<mtable>` (not bare mo for parentheses).
- [ ] Rows in `<mtr>`, cells in `<mtd>`.

## Set Delimiters (Underbrace / Overbrace)

- [ ] Underbrace: `<munder accent="true"><mrow>...</mrow><mo>&#x23DF;</mo></munder>`.
- [ ] Overbrace: `<mover accent="true"><mrow>...</mrow><mo>&#x23DE;</mo></mover>`.

## Multiline Formulas

- [ ] Use `<mtable>` and `<maligngroup>` per MathML 3 / W3C for multiline formulas.

## Chemistry

- [ ] Add **class="chemistry"** on the `<math>` element for chemical formulas.
- [ ] Use `<mtext>` for element symbols (C, O, H, etc.) in chemistry formulas.
- [ ] Isotope (e.g. ^14 C): `<msup><mo>&#32;</mo><mn>14</mn></msup><mtext>C</mtext>` (&#32; = space).

## Physics

- [ ] Add **class="physics"** on the `<math>` element for physics formulas.

## Code

- [ ] When `<math>` is inside a code block, add **class="code"** on the `<math>` element.

## Tables

- [ ] Math inside HTML tables must use **display="inline"** on the `<math>` element.

## Union and Intersection

- [ ] Union: `<mo>&#8746;</mo>` (not letter U).
- [ ] Intersection: `<mo>&#8898;</mo>`.

## AsciiMath and alttext

- [ ] **alttext** on `<math>` must mirror the MathML (AsciiMath representation); very short alttext with long MathML is invalid.

## Validation Points (Summary)

- [ ] Frame: math → semantics → mrow; alttext and altimg present; display set.
- [ ] xml:lang on an ancestor of each math element.
- [ ] Parentheses/brackets/absolute value via mfenced, not mo.
- [ ] Invisible operators (&#8289;, &#8290;) used for function application and multiplication where required.
- [ ] Comparison operators with numeric entities (&#60;, &#62;, &#8804;, &#8805;).
- [ ] Decimals in one mn; no thousand separators in mn.
- [ ] No spaces in mi/mo/mn; use mspace; no single-space mtext (except chemistry isotope).
- [ ] Identifiers in mi, text in mtext; do not split words into single letters.
- [ ] Named functions: mrow with exactly three children (mi, mo &#8289;, argument).
- [ ] Chemistry: class="chemistry", mtext for elements; physics: class="physics"; code: class="code".
- [ ] Math in tables: display="inline".
- [ ] alttext reflects MathML (no gross mismatch).
