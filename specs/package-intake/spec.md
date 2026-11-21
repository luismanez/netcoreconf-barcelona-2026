# Feature — Package intake

The presenter can drop one photo or a full stage batch into the web app and preview the items before processing. The backend resolves the filename stem against the preloaded JSON manifest. For example, `P024.jpg` gets the note associated with `P024`. A matching note may describe the contents, handling context, an observation, or the pickup deadline.

Each submission creates a staged batch with an item ID per upload, the warehouse package ID, and a ready or intake-error state. Item IDs distinguish the uploaded entries throughout the run. Supported, readable images with a manifest match become ready. A failed item shows its filename and failure reason alongside the remaining ready items.

The ready state is the starting point for the presenter to launch processing. The batch response carries the item summaries that the conveyor will use to render the incoming queue.

See [global specification](../global.md#load-the-packages) and [implementation tasks](tasks.md).
