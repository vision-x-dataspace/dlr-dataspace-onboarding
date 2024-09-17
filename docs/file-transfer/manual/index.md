# File Transfer (Manual)

## Introduction

Here we describe how to interact with the DLR Base-X Dataspace manually via http requests.

The individual explanations were heavily drawn from and inspired by the [mangement-api-walkthrough](https://github.com/eclipse-tractusx/tractusx-edc/tree/release/0.6.0/docs/usage/management-api-walkthrough) (TractusX).

## Prerequisites

For the data transfer you will need two `AmazonS3` buckets. So either you use two separate storage instances with one bucket each or only one instance with two buckets. These storage instances will have to be reachable via some URLs. For setting up such storage instances you can check out [MinIO](https://github.com/minio/minio).

## Structure

This tutorial consists of two parts.

In the first part you will create an `Asset` and a `Policy Definition` as well as a corresponding `Contract Definition` on one `Connector`.

In the second part you will fetch the `Federated Catalog` of a second Connector and choose one `Offer` in it. Then you will initiate a `Contract Negotiation` for this `Offer` as well as an eventual `Transfer Process`.

Make sure to actually use different `Connectors` in these two parts.
