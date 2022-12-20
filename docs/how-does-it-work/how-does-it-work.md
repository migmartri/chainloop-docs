---
sidebar_position: 2
---

import MailingListForm from '../partials/\_mailing-list-form.mdx';
import Image from "@theme/IdealImage";

# How Does it Work?

ChainLoop is a Software as a Service (Open Source soon), that consists of a [SLSA level 3](https://slsa.dev/spec/v0.1/requirements#summary-table) provenance-compliant **control plane and single source of truth** for artifacts and attestation **plus a dead-simple, [contract-based](/getting-started/workflow-definition#workflow-contracts) attestation crafting process**.

In practice, that means a solution that provides

### Compliant Single Source of Truth

With ChainLoop, your Software Supply Chain can craft and store artifacts via a single integration point regardless of your CI/CD provider choice.

<Image img={require("./overview-1.png")} />

The result is having a SLSA level 3 compliant single Source of truth for artifacts and attestation built on OSS standards such as [Sigstore](https://www.sigstore.dev/), [in-toto](https://in-toto.io/), [SLSA](https://slsa.dev) and [OCI](https://github.com/opencontainers/image-spec/blob/main/spec.md).

ChainLoop also makes sure the crafting of artifacts and attestation follows **best practices and meets the requirements** declared in their associated Workflow Contract.

### Contract-based attestation

One key aspect is that in ChainLoop, CI/CD integrations are declared via [**Workflow Contracts**](/getting-started/workflow-definition#workflow-contracts).

A [Workflow Contract](/reference/operator/contract) gives operators **full control over what kind of data (build info, materials) must be received as part of the attestation and the environment where these workflows must be executed at**. This enables an easy, and maintainable, way of propagating and enforcing requirements downstream to your organization.

You can think of it as an [**API for your organization's Software Supply Chain**](/reference/operator/contract) that both parties, development and SecOps teams can use to interact effectively.

<Image img={require("./overview-3.png")} />

### Third-Party Integration fan-out

Operators can set up third-party integrations such as [Dependency-Track](https://dependencytrack.org/) for SBOM analysis or an OCI registry for storage of the received artifacts and attestation metadata.

<Image img={require("./overview-2.png")} />

Ops can mix and match with different integrations while **not requiring developers to make any changes on their side**!

### Observability/Auditability

The control plane provides org-wide workflow, attestation, and artifacts [visibility](/getting-started/operator-view), including error rates, and operational anomalies.

A new web user interface is [in the works](https://github.com/chainloop-dev/frontend) :)

### Role-tailored experience

ChainLoop makes sure to clearly define the responsibilities, experience and functional scope of the **two main personas, Security/Operation (SecOps) and Development/Application teams**.

SecOps are the ones in charge of defining the Workflow Contracts, setting up third-party integrations, or having access to the control plane where all the Software Supply Chain Security bells and whistles are exposed.

Development teams on the other hand, just need to integrate ChainLoop's jargon-free [crafting tool](/getting-started/attestation-crafting) and follow the steps via a familiar DevExp to make sure they comply with the Workflow Contract defined by the SecOps team. No need to learn in-toto, signing, SLSA, OCI APIs, nada :)

## Integration Overview

Let's walk through an overview of what a integration looks like:

![overview](/img/v2/chainloop-dev-overview.png#gh-light-mode-only)
![overview](/img/v2/chainloop-dev-overview-dark.png#gh-dark-mode-only)

In short, the integration process of a new pipeline in ChainLoop consists of

- The Operator registers a contract for that pipeline in the control plane.
- The developers that own the pipeline use ChainLoop's CLI to craft an attestation to comply with the contract.

![flow](./chainloop.dev.png#gh-light-mode-only)
![flow](./chainloop.dev-dark.png#gh-dark-mode-only)

### Operator - Setup

1. An operator [creates a Workflow, a Contract (schema), and a service account](/getting-started/workflow-definition#workflow-and-contract-creation)

### Developer - Attestation Crafting

2. Set up the provided service account in their CI

3. [Start the crafting process](/getting-started/attestation-crafting#initialization) by authenticating with the service account and **retrieving the contract**.

4. [Add the **materials required by the contract**](/getting-started/attestation-crafting#adding-materials), i.e artifact, OCI image ref, SBOM. If needed, the artifact will be uploaded to the built-in CAS and referenced by its content digest

5. [Generate and push](/getting-started/attestation-crafting#encode-sign-and-push-attestation) a signed in-toto statement once all the required materials have been added.

### Operator - Inspect data

6. [Verify Attestation/Artifact metadata](/getting-started/operator-view). They also have access to operational metrics

7. [Download Artifacts](/getting-started/operator-view#artifacts-download).

8. [Subscribe to exported Metrics](/getting-started/operator-view#metrics-coming-soon)

At this point, the SecOps team has control of the attestation and artifacts expectations (via Workflow contracts), which can be updated at any time with new requirements.

They also gained visibility, and have all the metadata and artifacts meeting the latest standards and best practices, while developers have been shielded from most of the complexity related to this process.

<MailingListForm />