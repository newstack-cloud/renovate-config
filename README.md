# newstack-cloud/renovate-config

Org-wide Renovate configuration presets for **all** `newstack-cloud` repositories,
for all of the product families (Bluelink, Celerity, …).

## Presets

- **`default.json`** — universal policy every repo extends via
  `github>newstack-cloud/renovate-config`: schedule, the `deps` / `ci(deps)` commit
  convention, auto-merge tiers, and the "Dependabot handles security only" stance.

Product-specific rules do **not** belong here. For example, the Bluelink release
cascade (auto-merging internal `github.com/newstack-cloud/bluelink/*` bumps) lives
in a Bluelink-scoped preset at
`github>newstack-cloud/bluelink//renovate/bluelink-consumers`, which only the repos
in the Bluelink dependency graph extend.

## Layering

```
newstack-cloud/renovate-config//default            ← universal; ALL repos
        ▲
        │ extends
newstack-cloud/bluelink//renovate/bluelink-consumers  ← Bluelink cascade only
        ▲
        │ extends
bluelink · celerity-provider-aws · deploy-cli-sdk
        (celerity-node-sdk extends ONLY the org preset)
```

Every repo opts in explicitly with `extends`. For this to resolve, the
`newstack-cloud/renovate-config` repo must exist on GitHub (it is staged here for
review — see the rollout steps in bluelink's `RENOVATE.md`).
