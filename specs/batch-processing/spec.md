# Feature — Batch processing

The presenter starts processing after a photo batch has been staged. The backend owns the run lifecycle and the in-flight limit. Each ready item enters the queue, gets its Foundry result or a processing failure, and reaches a terminal state. Intake errors remain visible throughout the run. Each result is associated with its item ID, so responses can finish in any order.

For a valid result, compare the selected route's probability with the review threshold. At or above the threshold, apply the proposed route. Below the threshold, apply **Inspect** and mark **Human review**. Store the proposed route, applied route, and review reason. A presenter can reevaluate that policy against a saved answer.

The presenter page opens the live event stream before starting the batch. The backend sends package updates as they happen, along with the final outcome when every item has an applied route or a recorded failure. The page shows an interruption message if the stream stops unexpectedly.

See [global specification](../global.md#routing-policy) and [implementation tasks](tasks.md).
