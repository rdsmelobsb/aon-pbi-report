# Power BI TMDL Audit - Progress Tracker

> Working checklist for AON_2024 PBIP Audit.

---

## Phase 1: Discovery and Inventory
- [x] Scan project folder structure recursively
- [x] Identify all `.tmdl` files (tables, relationships, expressions, roles, cultures)
- [x] Identify report manifests (`.pbi`, `.pbip`)
- [x] Identify theme JSON files, images, and custom visuals
- [x] Record model storage mode (Import)
- [x] Record compatibility level from `database.tmdl` (1606)
- [x] Summarize inventory (12 tables, 54 measures, 130 columns, 9 relationships)

## Phase 2: Domain 1 - Structure and Star Schema
- [x] STR-01: Check for missing relationships (passed, 9 valid relationships)
- [x] STR-02: Check for snowflake schema (passed, star-schema around DATA_DIM and DIM_VEICULOS_GERAL)
- [x] STR-03: Check for tables with no relationships (passed, only measure and parameter tables disconnected)
- [x] STR-04: Check for wide tables (evaluated, 17 columns hidden in REDES_FATO)
- [x] STR-05: Check for visible fact-table columns (fixed: 30 columns hidden in REDES_FATO, GA_FATO, GA_EVENTOS_FATO)

## Phase 3: Domain 2 - Modeling, Relationships and Naming
- [x] MOD-01: Check for bidirectional cross-filtering (passed, 0 bidirectional)
- [x] MOD-02: Check for many-to-many relationships (passed, 0 many-to-many)
- [x] MOD-03: Review inactive relationships (passed, 0 inactive)
- [x] MOD-04: Check for text-type join columns (evaluated, Id Seed preserved for matching)
- [x] MOD-05: Check for bidirectional security filtering without RLS (passed)
- [x] MOD-06: Check object name capitalization (passed)
- [x] MOD-07: Check for `Dim` / `Fact` prefixes in table names (evaluated)
- [x] MOD-08: Check for leading/trailing whitespace in names (passed)
- [x] MOD-09: Check for special characters in names (passed)
- [x] MOD-10: Check for unqualified column references in DAX (passed)
- [x] MOD-11: Check for qualified measure references in DAX (passed)
- [x] MOD-12: Check tables with >10 visible items and no display folders (fixed: display folders added across all measure tables)
- [x] MOD-13: Check hidden column CamelCase convention (passed)

## Phase 4: Domain 3 - Performance
- [x] Record complexity thresholds (passed)
- [x] PRF-01: Check calculated columns using `RELATED` (passed, 0 found)
- [x] PRF-02: Check calculated columns with aggregation functions (passed, 0 found)
- [x] PRF-03: Check for calculated tables (passed, only rd_LinhasGrafico)
- [x] PRF-04: Check for auto date/time tables (fixed: disabled, 7 auto tables removed)
- [x] PRF-05: Check date tables marked with `DataCategory: Time` (fixed: added to DATA_DIM)
- [x] PRF-06: Check DateTime columns with non-midnight values (passed)
- [x] PRF-07: Check `isAvailableInMdx` on non-attribute columns (passed)
- [x] PRF-08: Check numeric columns without `summarizeBy: none` (passed)
- [x] PRF-09: Check for floating-point `dataType: double` (evaluated)
- [x] PRF-10: Check DirectQuery model without aggregation tables (not applicable, import model)

## Phase 5: Domain 4 - Security
- [x] SEC-01: Check for hardcoded credentials in M expressions (evaluated Google Sheets API key)
- [x] SEC-02: Check for local file paths in partition sources (passed, 0 local file paths)
- [x] SEC-03: Check for hardcoded server/database names (passed)
- [x] SEC-04: Check for PII column names without RLS (passed, no PII)
- [x] SEC-05: Check for `USERNAME()` vs `USERPRINCIPALNAME()` in RLS (not applicable)
- [x] SEC-06: Check RLS filters on fact tables (not applicable)
- [x] SEC-07: Check for `LOOKUPVALUE` in RLS expressions (not applicable)
- [x] SEC-08: Check for empty roles (passed)
- [x] SEC-09: Check for hardcoded filter values in RLS (passed)
- [x] SEC-10: Check for overly complex RLS expressions (passed)
- [x] SEC-11: Check measures referencing OLS-hidden columns (passed)
- [x] SEC-12: Check OLS combined with RLS on same table (passed)

## Phase 6: Domain 5 - DAX Quality
- [x] DAX-01: Check `FILTER` on entire table inside `CALCULATE` (passed)
- [x] DAX-02: Check division operator instead of `DIVIDE()` (fixed: replaced with DIVIDE)
- [x] DAX-03: Check `FORMAT()` usage in measures (evaluated)
- [x] DAX-04: Check `IFERROR` / `ISERROR` usage (passed, 0 found)
- [x] DAX-05: Check `EARLIER` / `EARLIEST` usage (passed, 0 found)
- [x] DAX-06: Check nested `IF` >= 4 deep (passed)
- [x] DAX-07: Check `ALL()` on entire table without column specification (passed)
- [x] DAX-08: Check `COUNTROWS(VALUES())` instead of `DISTINCTCOUNT` (passed)
- [x] DAX-09: Check `HASONEVALUE + VALUES` instead of `SELECTEDVALUE` (passed)
- [x] DAX-10: Check iterator on single column instead of aggregator (passed)
- [x] DAX-11: Check for nested iterators (passed, 0 found)
- [x] DAX-12: Check measures >200 chars with no `VAR` (passed)
- [x] DAX-13: Check measure complexity thresholds (passed)
- [x] DAX-14: Check nested `CALCULATE` (passed, 0 found)
- [x] DAX-15: Check measure dependency chain depth (passed)

## Phase 7: Domain 6 - Metadata and Documentation
- [x] MET-01: Check measures without descriptions (fixed: 100% measures documented)
- [x] MET-02: Check visible columns without descriptions (evaluated)
- [x] MET-03: Check tables without descriptions (fixed: 100% tables documented)
- [x] MET-04: Check descriptions that duplicate object name (passed)
- [x] MET-05: Check descriptions shorter than 10 characters (passed)
- [x] MET-06: Check currency measures without currency format (passed)
- [x] MET-07: Check percentage measures without percentage format (passed)
- [x] MET-08: Check date columns without format string (passed)

## Phase 8: Final Review & Quality Leap Completed
- [x] Post-refactoring verification completed
- [x] Score updated to 95.2% (Grade A)
- [x] Final `AUDIT-REPORT.md` published
