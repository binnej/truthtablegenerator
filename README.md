# Truth Table Generator

A vibe coded single-file web page that generates truth tables for propositional logic formulas. No build step, no dependencies: open `truth-table.html` in any modern browser.

## Usage

1. Type a formula, using single letters as propositions (e.g. `p`, `q`, `r`).
2. Insert operators with the on-screen buttons, or type the keyboard shortcuts below.
3. Press **Generate table** (or hit Enter).

The table lists rows from high to low, starting with all 1s and ending with all 0s. With propositions `p` and `q` the rows are:

| p | q |
|---|---|
| 1 | 1 |
| 1 | 0 |
| 0 | 1 |
| 0 | 0 |

## Supported operators

| Operator | Symbol | Keyboard shortcut |
|----------|--------|-------------------|
| Not | ¬ | `!` or `~` |
| And | ∧ | `&` or `^` |
| Or | ∨ | `\|` |
| Implication | ⇒ | `=>` or `→` |
| Equivalence | ⇔ | `<=>` or `↔` |
| Brackets | `( )` | `( )` |

Note that the letter `v` is a valid proposition, so ∨ is only entered with the button or the `|` key.

### Precedence

From tightest to loosest binding: `¬`, `∧`, `∨`, `⇒`, `⇔`.

Implication is right-associative: `p ⇒ q ⇒ r` is read as `p ⇒ (q ⇒ r)`.

## Features

- Button input for all symbols, plus a backspace and clear button
- Keyboard shortcuts that convert to logic symbols as you type
- Optional intermediate columns for every sub-expression (checkbox)
- Column headers keep the brackets you typed
- Result summary: tautology, contradiction, or contingency (with the number of true rows)
- Clear error messages for unmatched brackets, unexpected symbols and incomplete formulas
- Light and dark mode, responsive layout

## Limits

- Propositions are single letters (`a`–`z`, `A`–`Z`); case matters, so `p` and `P` are different propositions
- At most 8 different propositions (256 rows)

## Example

Input:

```
(p ⇒ q) ⇔ (¬q ⇒ ¬p)
```

This is the contrapositive law. The final column is 1 in every row, so the tool reports a **tautology**.

## How it works

1. The input is tokenised into letters, operators and brackets.
2. A recursive-descent parser builds a syntax tree following the precedence rules above.
3. For each combination of proposition values the tree is evaluated. Sub-expressions are de-duplicated into columns.
4. The table is rendered, and the final column is counted to classify the formula.
