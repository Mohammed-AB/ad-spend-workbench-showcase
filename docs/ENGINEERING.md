# Ad-Spend Decision Workbench: engineering notes

An attractive performance metric can hide bad inputs or weak margins. Ad-Spend Decision Workbench reconciles spend and order data before producing a recommendation.

## System path

~~~mermaid
flowchart LR
  SpendAndOrders --> Mapping
  Mapping --> Reconciliation
  Reconciliation --> DecimalMetrics
  DecimalMetrics --> Scenarios
  Scenarios --> CheckedNarrative
  CheckedNarrative --> ReviewedReport
~~~

This diagram describes the demonstrated system boundary, not a production deployment topology.

## Decisions and tradeoffs

### Reconcile before calculating

Import mappings and inconsistent rows remain visible before metrics are computed.

### Keep formulas inspectable

Decimal arithmetic, row provenance and explicit assumptions support drill-down from a metric to the inputs that produced it.

### Check the narrative against the numbers

A generated explanation is validated against calculated facts. Review and report export remain separate from any real spending action.

## Review questions

- What evidence demonstrates **reconcile before calculating**, and what would fail without it?
- What evidence demonstrates **keep formulas inspectable**, and what would fail without it?
- What evidence demonstrates **check the narrative against the numbers**, and what would fail without it?

## Verification boundary

14 database regressions and 19 browser checks passed in the current verification pass. The synthetic corpus spans six campaigns, three countries and ten edge cases. Recorded reconciliation, metric drill-down, assumption comparison and recommendation review.

A controlled decision-support demo, not financial advice or a prediction of campaign returns. No automatic ad-platform writes exist in the showcased flow.
