# Power Query M Guardrails

Use this when writing, refactoring, or reviewing Power Query M partition queries, custom functions, or data-cleansing steps in Power BI PBIP models.

## Text.Select & Text.Remove Signatures

- `Text.Select(text, selectChars)` accepts a character list (e.g. `{"0".."9"}`) or text. It **never** accepts a predicate function (`each ...`). Passing a function causes:
  `Expression.Error: O valor de argumento não é válido. Detalhes: [Function]`
- `Text.Remove(text, removeChars)` accepts a character list to strip (e.g. `{"(", ")", "[", "]"}`).

## Pure Numeric Detection Without Record Bugs

Avoid `try Number.From(...)` without evaluating `[HasError]`, because Power Query records evaluate to truthy. The cleanest and fastest check in native M:

```powerquery
ehNumero = (Text.Select(termo, {"0".."9"}) = termo) and Text.Length(termo) >= 5
```

## Safe Delimiter Substring Extraction

Avoid bare `Text.BeforeDelimiter(text, delimiter)` if the delimiter might be missing, because standard defaults return an empty string `""`, wiping out legitimate data. Instead, test the position first:

```powerquery
posTracking = Text.PositionOf(texto, "(naugm", 0, Comparer.OrdinalIgnoreCase),
semTracking = if posTracking > 0 then Text.Start(texto, posTracking) else texto
```

## Multi-Delimiter Normalization

For normalizing mixed separators (`_`, `-`, `|`, `(`, `)`), explicit chained `Text.Replace` calls ensure predictable behavior without loop overhead:

```powerquery
substituido = Text.Replace(Text.Replace(Text.Replace(Text.Replace(semTracking, "(", " "), ")", " "), "_", " "), "-", " ")
```

## Culture-Explicit Date Text Functions

When creating textual date keys (e.g. `Month|Seed` or `Mês/Ano`) used in model relationships, NEVER rely on the default locale of `Date.MonthName`:

```powerquery
// WRONG - Breaks across different OS regional settings (e.g. "March" vs "Março"):
Date.MonthName([Date])

// CORRECT - Deterministic across all environments and gateways:
Date.MonthName([Date], "pt-BR")
```

## Dimension Cleansing & Foreign Key Integrity

When transforming noisy dimension keys for executive display:
1. Retain the raw technical column as `isHidden` to preserve 1:* model relationships.
2. Add the user-facing cleansed column (e.g. `Criativo`) via deterministic M transformations.
3. Update visual table and slicer projections to bind to the sanitized column.
