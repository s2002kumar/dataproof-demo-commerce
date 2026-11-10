# Commerce Orders & Refunds — DataProof demonstration

**A migration can pass PostgreSQL's checks and still change a customer's refund.** This intentionally small FastAPI, Next.js, and PostgreSQL application is the public test case for [DataProof](https://github.com/s2002kumar/DataProof), a pull-request migration verifier.

## See the evidence

In [demo pull request #2](https://github.com/s2002kumar/dataproof-demo-commerce/pull/2), a migration joins payment events to order items before aggregation. A **49.99** refund on an order with two items becomes **99.98**, even though the SQL succeeds and the usual schema constraints hold.

- [Blocked GitHub check](https://github.com/s2002kumar/dataproof-demo-commerce/runs/126168145938) — DataProof finds the exact expected-versus-observed refund mismatch.
- [Checked GitHub check](https://github.com/s2002kumar/dataproof-demo-commerce/runs/126170290869) — the corrected migration preserves the original amount.
- [Recorded live integration demo](https://github.com/s2002kumar/DataProof/blob/main/docs/media/live-demo.mp4) — shows the pull request, binding review, failure, correction, and result.

## Repository map

- [`sample-app/`](sample-app/) — the FastAPI service, Next.js interface, and PostgreSQL migrations.
- [`dataproof/oracles/`](dataproof/oracles/) — protected data and API contracts that a candidate pull request cannot weaken.
- [`dataproof/bindings/`](dataproof/bindings/) — proposed schema bindings; a maintainer approves them before dependent verification can pass.

This is a **synthetic demonstration**, not a production commerce system or evidence of third-party adoption. See the [DataProof architecture and verification scope](https://github.com/s2002kumar/DataProof#how-it-works).
