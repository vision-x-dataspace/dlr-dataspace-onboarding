# File Transfer (Postman)

## Introduction

Here we describe how to interact with the DLR-Dataspace via http requests using [Postman](https://www.postman.com).

You can download the `Postman` collection from [here](../../collections/Onboarding%20Tutorial%20Postman.postman_collection.json).

## Prerequisites

For the data transfer you will need two `AmazonS3` buckets. So either you use two separate storage instances with one bucket each or only one instance with two buckets. These storage instances will have to be reachable via some URLs. For setting up such storage instances you can check out [MinIO](https://github.com/minio/minio).

To use the collection it needs to be imported into `Postman` and the provided with values in the 'Variables' section:

| Variable                  | Description      |
|---------------------------|------------------|
| `ALICE_API_KEY`           | The X-Api-Key of the Provider <br> &lt;your-password-1&gt; |
| `ALICE_BPN`               | The `Business Partner Number` of the Provider `Connector` (required for locating the `Offer` in the `Catalog`) <br> &lt;your-connector-id-1&gt; |
| `ALICE_MANAGEMENT`        | The path to the Management URL of the Provider <br> <https://vision-x-dataspace.base-x-ecosystem.org/&lt;your-connector-name-1&gt;/management> |
| `ALICE_MINIO_URL`         | The URL where your `AmazonS3` storage containg the file you want to transfer is reachable from |
| `ALICE_BUCKET_NAME`       | The bucket in which the file is located |
| `ALICE_ACCESS_KEY_ID`     | Some username to access your `AmazonS3` storage |
| `ALICE_SECRET_ACCESS_KEY` | The password matching to the username to access your `AmazonS3` storage |
| `BOB_API_KEY`             | The X-Api-Key of the Consumer <br> &lt;your-password-2&gt; |
| `BOB_BPN`                 | The `Business Partner Number` of the Consumer `Connector` (required for setting a specific `Contract Policy`) <br> &lt;your-connector-id-2&gt; |
| `BOB_MANAGEMENT`          | The path to the Management URL of the Provider <br> <https://vision-x-dataspace.base-x-ecosystem.org/&lt;your-connector-name-2&gt;/management> |
| `BOB_MINIO_URL`           | The URL where your `AmazonS3` storage where you want the file to be transferred to is reachable from |
| `BOB_BUCKET_NAME`         | The bucket in which you want the file to be transferred to |
| `BOB_ACCESS_KEY_ID`       | Some username to access your `AmazonS3` storage |
| `BOB_SECRET_ACCESS_KEY`   | The password matching to the username to access your `AmazonS3` storage |
| `FILE_NAME`               | The name of the file you want to transfer |

## Structure

This tutorial consists of two parts.

In the first part ('Alice') you will create an `Asset` and two `Policy Definition` as well as a corresponding `Contract Definition` on one `Connector`.

In the second part ('Bob') you will fetch the `Federated Catalog` of a second Connector and choose one `Offer` in it. Then you will initiate a `Contract Negotiation` for this `Offer` as well as an eventual `Transfer Process`.
