# Feature — Conveyor experience

The presenter starts a staged batch on a projection-friendly conveyor screen. The screen shows an incoming queue, packages in processing, and three destination lanes labeled **Continue**, **Repack**, and **Inspect**. Each package has a photo and an ID. Sorted packages show urgency using both color and a text label. Items marked for human review appear in **Inspect** with an explicit badge.

As results arrive, animate each package into its applied lane. The animation follows the backend result and the visual transitions can overlap. Intake and processing errors have visible states and reasons.

Clicking a package opens an in-place detail panel. It presents the photo, operator note, all three model answers, raw Foundry JSON, proposed and applied routes, review reason, and measured timings. A failed package shows the error and available diagnostics. The presenter can apply a different threshold to a completed package and see it move if the resulting route changes.

See [global specification](../global.md#watch-the-conveyor-run) and [implementation tasks](tasks.md).
