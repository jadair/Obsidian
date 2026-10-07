## Purpose

  **Create an audit trail for funds - **

This schema defines a clean, normalized master record for endowment tracking.

It is designed to combine the current-state structure from:

  

- `Sorted Updated _ FHT Classifications FY26 _stc.xlsx`

  

with supporting historical activity from:

  

- `FHT Fund History _ STC.xlsx`

  

The goal is governance and recordkeeping, not full financial reconstruction yet.

## Record Grain

One row per fund.

Use `canonical_fund_id` as the primary business key. Store it as text, not a number, because the source uses:


- numeric fund IDs such as `598609`

- hyphenated IDs such as `250-999998`

- occasional missing IDs such as `McAllister Estate`

**TODO** Clean up Principal Fund Org# or identify an alternate primary key

  

## Design Rules 

  
1. Preserve source text in `*_raw` fields.

2. Store cleaned values in `*_clean` fields when the cleanup is mechanical.

3. Store governed categories in `*_normalized` fields when the source values are inconsistent.

4. Keep official purpose language separate from operational interpretation.

5. Treat historical activity as supporting context, not the core schema.

6. Keep source lineage for every imported row.

  

## Core Fields

  

| Field                             | Type          | Required | Description                                                                                                                                                    |
| --------------------------------- | ------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `legacy_fund_id`                  | string        | No       | Original A-column ID when a future source distinguishes legacy and current values.                                                                             |
| `endowment_title`                 | string        | Yes      | Official fund or endowment title.                                                                                                                              |
| `principal_account_raw`           | string        | No       | Principal account value exactly as provided by the source.                                                                                                     |
| `principal_account_clean`         | string        | No       | Cleaned principal account value after trimming and formatting cleanup.                                                                                         |
| **`spending_account_raw`**        | **string**    | **No**   | **Spending account value exactly as provided by the source.**                                                                                                  |
| **`spending_account_clean`**      | **string**    | **No**   | **Cleaned spending account value after trimming and formatting cleanup.** <br><br>**Identify actual values or data type**                                      |
| `org_number`                      | string        | No       | Organization number from source when present.                                                                                                                  |
| `administrator_name`              | string        | No       | Source administrator or cost center owner.<br><br>**Establish Relationship using drexel user accounts if possible to potential manage rule based permissions** |
| `general_purpose_text`            | text          | No       | Official high-level purpose text.                                                                                                                              |
| `specific_purpose_text`           | text          | No       | Official detailed restriction or use text.<br><br>**Review and analyze text to allow for better lookups and matching**                                         |
| `department_school_text`          | string        | No       | Department or school text from source.<br><br>**Clean up list of departments - get additional context as to what a department is**                             |
| `classification_raw`              | string        | No       | Exact value from `Dean's Classification`.                                                                                                                      |
| `classification_normalized`       | string        | No       | Controlled vocabulary value for reporting and filtering.                                                                                                       |
| `suggested_use_raw`               | string        | No       | Exact value from `Current Suggested Use`.                                                                                                                      |
| `suggested_use_clean`             | string        | No       | Trimmed and mechanically cleaned suggested use text.                                                                                                           |
| `suggested_use_category`          | string        | No       | Controlled category for current suggested use.                                                                                                                 |
| `prior_usage_raw`                 | string        | No       | Exact value from `PRIOR USAGE`.                                                                                                                                |
| `prior_usage_clean`               | string        | No       | Trimmed and mechanically cleaned prior usage text.                                                                                                             |
| `prior_usage_category`            | string        | No       | Controlled category for prior usage.                                                                                                                           |
| ***`current_units_balance`***     | ***decimal*** | ***No*** | ***Current units from the classification workbook.***                                                                                                          |
| ***`current_fund_balance`***      | ***decimal*** | ***No*** | ***Current fund balance from the classification workbook.***                                                                                                   |
| ***`current_market_value`***      | ***decimal*** | ***No*** | ***Current market value from the classification workbook.***                                                                                                   |
| ***`activity_total_since_2014`*** | ***decimal*** | ***No*** | ***Historical total activity rollup from the history workbook.***                                                                                              |
| ***`activity_direction`***        | ***string***  | ***No*** | ***`negative`, `positive`, or `zero` based on `activity_total_since_2014`.***                                                                                  |
| `documentation_status`            | string        | No       | Controlled documentation status based on the source legend.                                                                                                    |
| `review_status`                   | string        | Yes      | Workflow state for tracking review progress.                                                                                                                   |
| `needs_review_reason`             | text          | No       | Why a record needs follow-up.                                                                                                                                  |
| `source_workbook_classification`  | string        | No       | Source workbook path or logical name for classification data.                                                                                                  |
| `source_sheet_classification`     | string        | No       | Source sheet name for classification data.                                                                                                                     |
| `source_row_classification`       | integer       | No       | Source row number for classification data.                                                                                                                     |
| `source_workbook_history`         | string        | No       | Source workbook path or logical name for historical activity data.                                                                                             |
| `source_sheet_history`            | string        | No       | Source sheet name for historical activity data.                                                                                                                |
| `source_row_history`              | integer       | No       | Source row number for historical activity data.                                                                                                                |
| `record_notes`                    | text          | No       | Freeform notes that do not belong in source-backed columns.                                                                                                    |



  

## Recommended Controlled Vocabularies

  
### `classification_normalized`



- `Clinical Innovation`

- `Community Care`

- `Community Care - Pediatrics`

- `Faculty Excellence`

- `Research and Innovation`

- `Student Experience`

- `Unknown / Needs Review`

  

### `suggested_use_category`

  


- `Capital`

- `Clinical Services`

- `Department Support`

- `Faculty Development`

- `Faculty Support / Recruitment`

- `Pediatrics`

- `Research`

- `Unknown / Needs Review`

  

### `prior_usage_category`

  

Use this controlled list:

  

- `Faculty Support / Recruitment`

- `HSB`

- `Unknown / Needs Review`

  

### `documentation_status`

  

Use this controlled list based on the legend in the classification workbook:

  

- `Complete documentation found`

- `Some documentation found`

- `No documentation found`

- `Not yet assigned`

  

### `review_status`

  

Use this controlled list:

  

- `Not reviewed`

- `Reviewed`

- `Needs documentation`

- `Needs gift review`

- `Needs classification review`

- `Ready for use guidance`

  

## Source-to-Master Mapping

  

### Classification Workbook

  

Base source:

  

- workbook: `Sorted Updated _ FHT Classifications FY26 _stc.xlsx`

- sheet: `Unitized Schedule`

  

| Source Column | Master Field |

| --- | --- |

| `A` | `canonical_fund_id` |

| `D` | `principal_account_raw` |

| `E` | `spending_account_raw` |

| `F` | `org_number` |

| `G` | `administrator_name` |

| `I` | `endowment_title` |

| `J` | `general_purpose_text` |

| `K` | `specific_purpose_text` |

| `L` | `department_school_text` |

| `N` | `classification_raw` |

| `P` | `current_units_balance` |

| `Q` | `current_fund_balance` |

| `R` | `current_market_value` |

| `S` | `suggested_use_raw` |

| `T` | `prior_usage_raw` |

  

### History Workbook

  

Supporting source:

  

- workbook: `FHT Fund History _ STC.xlsx`

- sheet: `Sheet1`

  

| Source Column | Master Field |

| --- | --- |

| `A` | `canonical_fund_id` or `legacy_fund_id` |

| `F` | `principal_account_raw` |

| `G` | `spending_account_raw` |

| `H` | `org_number` |

| `O` | `administrator_name` |

| `Q` | `endowment_title` |

| `R` | `general_purpose_text` |

| `S` | `specific_purpose_text` |

| `T` | `department_school_text` |

| `JR` | `activity_total_since_2014` |

  

## Normalization Strategy

  

### Identification


- Store all fund IDs as text.

- Preserve hyphens.

- Do not coerce IDs to integers.

- Track missing IDs explicitly and flag them for review.

  

### Names and Purpose Text


- Preserve official title and purpose language exactly.

- Trim leading and trailing whitespace only.

- Do not shorten or paraphrase official restriction text.

  

### Classification Cleanup

Normalize obvious source defects:

  

- `Cliinical Innovation` -> `Clinical Innovation`

- `Facutly Excellence` -> `Faculty Excellence`

- `Commity Care ` -> `Community Care`

- `Community care` -> `Community Care`

- `Community Care - Peds` -> `Community Care - Pediatrics`

  

### Suggested Use Cleanup


Keep the source text, but clean mechanical issues:


- trim whitespace

- normalize case where safe

- retain ambiguity markers in the raw field

- map broad operational meaning into `suggested_use_category`

  

Examples:

- `Cuthbert ` -> clean as `Cuthbert`

- `Clinical services` -> clean as `Clinical Services`

- `Clinical Services (?)` -> keep raw text, categorize as `Clinical Services`, and add a review note

- `?` -> categorize as `Unknown / Needs Review`

  

### Prior Usage Cleanup


- trim whitespace

- normalize exact duplicates such as `HSB ` -> `HSB`

- map recruitment-package rows to `Faculty Support / Recruitment`

  

## Known Source Issues

  

1. The classification workbook is the cleaner base file, but it still contains inconsistent category spellings.

2. The history workbook includes wide quarterly time-series data and should not be used as the primary register.

3. One shared record, `McAllister Estate`, appears without a fund ID in both workbooks and must be manually resolved.

4. Documentation legend values exist, but the first-sheet reference field is not populated enough to treat documentation status as complete.

5. Historical activity totals identify movement, but not transaction-level explanations.

  

## Recommended Build Order

  

1. Load the classification workbook as the base register.

2. Normalize identifiers and categorical values.

3. Attach historical activity totals from the history workbook.

4. Add workflow and documentation fields.

5. Resolve missing IDs and ambiguous classifications before broader downstream use.