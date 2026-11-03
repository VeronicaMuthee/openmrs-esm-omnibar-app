# Upstream patches

These are proposals for other OpenMRS repos, not merged work.

## ChartSearch

The ChartSearch work for the omnibar is no longer a proposal here. It was submitted upstream on 2026-11-03 under epic [O3-6235](https://openmrs.atlassian.net/browse/O3-6235), as two PRs:

- [#86](https://github.com/openmrs/openmrs-esm-chartsearchai/pull/86), which warms the prompt cache when the chat opens instead of on every chart open, ready for review;
- [#87](https://github.com/openmrs/openmrs-esm-chartsearchai/pull/87), the answer section on Query results and `/ask`, a draft until #86 merges.

The no-warmup patch that used to be here removed the chart-open `/warmup` request outright; #86 replaces it. The initial-question patch was retired with the bar's Ask ChartSearch row in ChartSearch step 3, and its ChartSearch side was left out of #87.

## Framework (esm-core)

`esm-config-extension-config-validation.patch` applies to
`openmrs/openmrs-esm-core` at commit `7a17208`. It stops the framework from
logging `Unknown config key ... Ignoring.` for keys a module does declare, such
as the omnibar's `chartLookup` and Cohort Builder's `drugCriteriaEnabled` on
o3. The framework mounts an extension before its module has loaded and defined
its schema, and checks the extension's config against the bare implicit schema
in that gap. The values are still read. The patch holds back that check until
the module has loaded, as the module config already does. No module-side fix
exists. See
[esm-config-extension-config-validation.md](esm-config-extension-config-validation.md)
for the root cause, tests and risks.

## Cohort Builder

The Cohort Builder work for the omnibar is no longer a proposal here. It was submitted upstream on 2026-11-03 under epic [O3-6230](https://openmrs.atlassian.net/browse/O3-6230), as four PRs that build on each other:

- [#781](https://github.com/openmrs/openmrs-esm-cohortbuilder-app/pull/781), the URL hand-off, ready for review;
- [#782](https://github.com/openmrs/openmrs-esm-cohortbuilder-app/pull/782), the count row;
- [#783](https://github.com/openmrs/openmrs-esm-cohortbuilder-app/pull/783), the phrases;
- [#784](https://github.com/openmrs/openmrs-esm-cohortbuilder-app/pull/784), the test results.

#782 to #784 are drafts until the PR before each one merges. The patch that used to be here was #781's first version.

For the `v=count` proposal (the cohort counts brief, step 5): `adhocquery` evaluates only cohort definitions on the `rowFilters` path, which reporting gates on Get Patients alone, so a user without Run Reports can call it directly. The proposal should check Run Reports on that path too.
