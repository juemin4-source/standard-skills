# Router Regression Set

Run this before and after any archetype-router changes.

## Test Set (5 skills)

1. frontend-design → Director primary
2. high-end-visual-design → Director primary
3. baoyu-infographic → Delivery primary
4. baoyu-slide-deck → Delivery primary
5. ui-ux-pro-max → Director primary

## Acceptance Criteria

- frontend-design must NOT be Delivery primary (artifact-producing Director)
- high-end-visual-design must NOT be Delivery primary (artifact-producing Director)
- baoyu-infographic must NOT be Director primary (true Delivery)
- baoyu-slide-deck must NOT be Director primary (true Delivery)
- ui-ux-pro-max primary should be Director or Knowledge, secondary Delivery
- All confidence >= 0.85

## Command

Workflow({scriptPath: "G:\AI\Claude\projects\G--AI-Claude\55ec85b8-4310-4c6e-a89e-4f401f7b9acc\workflows\scripts\router-regression-5-wf_3d9f1036-c0d.js"})
