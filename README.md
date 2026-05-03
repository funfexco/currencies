# Currency List

A per-locale ISO 4217 currency catalog in **XML format**, covering all major languages and language/region combinations.

## Repository layout

The repository contains 563 locale directories named by language code or language-region pair (for example `en`, `bg`, `bg_BG`, `pa_Guru`). Each directory holds two files:

- `currency.xml` — the full ISO 4217 currency catalog (154 codes), with titles localized for that locale.
- `popular_currency.xml` — a curated subset of the 30 most globally relevant currencies, sharing the same per-locale titles and symbols as `currency.xml`.

## `currency.xml` format

Each file is a UTF-8 XML document with a single `<currencies>` root element identifying the locale via the `language` attribute, and one `<currency>` child per ISO 4217 code:

```xml
<?xml version="1.0" encoding="utf-8"?>
<currencies language="en">
  <currency>
    <title><![CDATA[US Dollar]]></title>
    <code>USD</code>
    <symbol>$</symbol>
    <position>0</position>
  </currency>
  <currency>
    <title><![CDATA[Euro]]></title>
    <code>EUR</code>
    <symbol>€</symbol>
    <position>0</position>
  </currency>
  <!-- … -->
</currencies>
```

Field reference:

- `<title>` — the localized currency name, wrapped in `CDATA`.
- `<code>` — the ISO 4217 three-letter code.
- `<symbol>` — the currency symbol. May be empty (`<symbol/>`) when no widely-accepted symbol exists.
- `<position>` — symbol placement relative to the amount: `0` = before (e.g. `$10.00`), `1` = after (e.g. `10.00 kr`).

## `popular_currency.xml`

A curated subset of the 30 most globally relevant currencies, listed in priority order so downstream consumers can render a short top-of-list dropdown without additional sorting. The schema is identical to `currency.xml`, and per-locale titles and symbols are kept in sync between the two files.

The 30 included codes, in order, are:

`USD`, `EUR`, `GBP`, `JPY`, `CNY`, `CHF`, `CAD`, `AUD`, `HKD`, `SGD`, `NZD`, `SEK`, `INR`, `KRW`, `NOK`, `DKK`, `MXN`, `BRL`, `ZAR`, `TRY`, `AED`, `SAR`, `RUB`, `PLN`, `CZK`, `HUF`, `ILS`, `THB`, `MYR`, `IDR`.

## Source / attribution

Initial data was seeded from [umpirsky/currency-list](https://github.com/umpirsky/currency-list); the `<symbol>` and `<position>` fields were added on top.
