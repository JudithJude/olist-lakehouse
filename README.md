# Olist Lakehouse

End-to-end lakehouse pipeline on the Brazilian e-commerce (Olist) dataset.
PySpark + Delta Lake on Databricks, medallion architecture, dimensional
gold layer, served through Metabase.

## Architecture

Raw CSVs → Bronze (as-is, Delta) → Silver (cleaned, validated) →
Gold (star schema) → Metabase

*(diagram coming)*

## Status

- [x] Bronze — 9 tables, ~1.5M rows ingested to Delta
- [ ] Silver — cleaning & validation
- [ ] Gold — dimensional model (facts & dims)
- [ ] Dashboard — Metabase

## Decisions & lessons

- **Reviews CSV had 5,000 phantom rows** — review comments contain
  line breaks, which broke naive CSV parsing. Fixed with multiLine +
  quote/escape options. Lesson: always check row counts against
  expectations.
- **One read pattern for all files** — applied the same CSV options
  everywhere rather than special-casing; harmless for clean files,
  protective for messy ones.

## Dataset

[Olist Brazilian E-Commerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
— ~100k orders, 2016–2018, 9 related tables. CSVs not included in repo;
download from Kaggle.