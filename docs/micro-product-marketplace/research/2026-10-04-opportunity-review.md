# First product opportunity review

Last research date: **2026-10-04**

Status: **First validation candidate recommended; no product approved for development.**

## Recommendation

Investigate a **Jira Service Management (JSM) exporter for external ticket reports that includes public comments and excludes internal notes** first. The available evidence identifies a concrete workflow and an established commercial category. It does not yet demonstrate enough unmet demand, willingness to pay for a narrower product, or a defensible advantage to justify building.

The proposed advantage is easier setup and a lower price for this specific workflow. That is a hypothesis: existing exporters already support excluding internal comments. Buyer conversations and a technical feasibility check should decide whether this becomes the first product.

This review is based on public customer discussions, marketplace listings, vendor documentation, and platform documentation inspected on 4 October 2026. No customer interviews or installed-product tests were performed. Prices and platform capabilities should be checked again before a build decision.

## Candidate comparison

| Candidate | Evidence and counterevidence | Current assessment |
| --- | --- | --- |
| JSM public-comment exporter | A customer requested filtered ticket exports without internal comments. Existing paid exporters cover this function, and the same customer also wanted attachments and PDF output. | First validation candidate. A smaller workflow may be useful, but differentiation and sufficient scope remain unproven. |
| DataGrip saved result snapshots | Users discussed finding and preserving query results. Payment demand and plugin API stability remain uncertain; JetBrains is considering changes to query history. | Alternative to investigate if the JSM candidate fails validation. |
| Shopify shipping-profile reconciliation | A merchant reported manually reconciling more than 300 products. Existing automation competes with the idea, while Shopify is changing its shipping system. | Park pending a clearer gap and stable platform behavior. |
| Jira subscription handover audit | An unresolved request concerns subscriptions when employees leave. Access to other users' subscriptions may prevent a reliable product. | Park until technical feasibility is demonstrated. |

These are qualitative assessments. No numerical scores, sales estimates, or revenue forecasts were established.

## JSM public-comment exporter

### Observed evidence

A **March 2025** customer discussion asks how to export filtered Jira data while excluding internal comments for external use. Follow-up questions concern attachments and PDF output. This is evidence of one real workflow, not a market-size estimate or a purchase commitment. [Customer discussion](https://community.atlassian.com/forums/Jira-questions/Export-filtered-data-excluding-internal-comments/qaq-p/2971970)

The prior review recorded Better Excel Exporter pricing of **US$174.50 per month for 50 Jira users**, with a free tier for **up to 10 users**. This is a competitor's pricing context, not a proposed price or proof that customers would pay for a narrower app. Recheck pricing before using it in a commercial comparison. [Vendor pricing](https://www.midori-global.com/products/better-excel-exporter-for-jira/cloud/buy)

Better PDF Exporter documents a template setting that excludes internal comments. The core exclusion feature therefore already exists in a competing product. Any opportunity must come from a demonstrably better fit for the buyer's workflow, setup burden, or budget. [Existing functionality](https://www.midori-global.com/products/better-pdf-exporter-for-jira/cloud/documentation/integrations/jira-service-management)

### Product hypothesis

Some JSM administrators who regularly send ticket reports outside their organization may prefer a small, straightforward export tool over configuring a broader reporting product. Neither that preference nor willingness to pay has been validated.

A proposed smallest version is:

1. Select tickets using a saved filter or JQL.
2. Preview a fixed set of ticket fields and public comments.
3. Download a CSV with clearly identified tickets, comment authors, and timestamps.

CSV-only scope is tentative. The documented customer's interest in attachments and PDF could make this version insufficient. Those formats should enter the initial scope only if buyer evidence supports the additional work.

The [JSM request API](https://developer.atlassian.com/cloud/jira/service-desk/rest/api-group-request/) documents public/internal comment filtering and permission-dependent responses. End-to-end feasibility remains untested: verify ticket selection, pagination, missing request types, and the requesting user's permissions throughout selection, preview, and export. Proposed design rule: omit any comment whose visibility cannot be established. Documentation establishes an API route, not a tested implementation.

## Other candidates

### DataGrip saved result snapshots

On **25 June 2025**, a user asked to restore result tabs after restarting DataGrip; JetBrains support replied that this behavior was not supported. On **7 April 2026**, another user requested more useful persistent history; JetBrains discussed separate query-history and result-storage requests. A **10 May 2026** reply mentioned a possible query-history redesign that year. This is a roadmap risk, not confirmation that saved results have shipped. [Restart request](https://intellij-support.jetbrains.com/hc/en-us/community/posts/27622788431378-Keep-Query-Results-on-Shutdown-Restart), [2026 discussion](https://intellij-support.jetbrains.com/hc/en-us/community/posts/34626527771410-Trying-to-understand-how-to-find-and-use-query-history-Big-Query-and-Teradata-DG-2025-2-2?page=1)

The inferred opportunity is an explicit local snapshot of loaded rows, SQL, source label, and timestamp that can be reopened without rerunning a query. Native [Execute to File](https://www.jetbrains.com/help/datagrip/run-a-query.html) is a competing workaround. The scan did not establish willingness to pay or stable extension points for capturing a result grid. A proposed prototype would cap rows and storage and avoid automatic capture, cloud sync, or database re-execution.

### Shopify shipping-profile reconciliation

On **29 June 2026**, a merchant described manually reconciling **300+ products** because staff update a displayed shipping-price metafield without updating the shipping profile, or vice versa. The proposed gap is a read-only mismatch report; correcting shipping assignments is outside that initial scope. [Merchant discussion](https://community.shopify.com/t/setting-shipping-profiles-by-product/639116)

Existing assignment automation weakens the opportunity: [Shipr](https://apps.shopify.com/auto-shipping-profile-shipr) starts at **US$4.99 per 30 days for up to 3,000 variants**, while [ShipAssign](https://apps.shopify.com/shipassign) offers a free tier for up to 500 variants. These are adjacent solutions, not proof that the exact metafield reconciliation need is covered. Shopify is gradually migrating shipping profiles to shipping options by market, initially for certain stores. Product groupings become collections, creating maintenance risk and potentially changing the need. [Official migration guide](https://help.shopify.com/en/manual/fulfillment/setup/shipping-options/whats-changing-with-shipping)

### Jira subscription handover audit

Atlassian request **JRACLOUD-97525**, created **18 February 2026**, describes scheduled filter emails stopping after their creator is deactivated, even if filter ownership has been transferred. It was unresolved with seven votes and three support references when inspected. These are limited pain signals, not market-size estimates. [Atlassian request](https://jira.atlassian.com/browse/JRACLOUD-97525)

The inferred opportunity is an employee handover report showing affected subscriptions and what to recreate. However, [Group Audit's documentation](https://arbeitstyp.de/apps/group-audit/docs/) says subscriptions created by other users may be invisible. The [Cloud Filters API](https://developer.atlassian.com/cloud/jira/platform/rest/v3/api-group-filters/) includes subscription data but does not establish complete cross-user discovery or reassignment. That threatens the core product promise; do not assume an app can bypass this limitation.

## Proposed validation work

The recommendation is to speak with **three to five JSM administrators** who send ticket reports externally. This is a proposed research step; no outreach was authorized or performed in this conversation.

Ask about the most recent actual export: who received it, how often it happens, which fields and formats were required, how internal notes were excluded, what tool was used, and what remained difficult. Then test whether the proposed CSV output would satisfy that workflow and whether the administrator has a purchasing route and a reason to pay.

Proposed gates, not agreed acceptance criteria:

- **Proceed to a small build** only if multiple relevant buyers describe recurring pain that existing tools do not adequately resolve, accept a narrow initial scope, and give credible payment signals; also confirm supported API access and reliable permission handling.
- **Revise the scope** if otherwise promising buyers consistently require PDF or attachments, then reassess effort and differentiation before building.
- **Reject or park** if buyers need a full reporting suite, current products already solve the problem satisfactorily, payment interest is absent, or the required data cannot be accessed safely through supported APIs.

The next decision is whether this narrow workflow merits development. It is not yet a launch decision.
