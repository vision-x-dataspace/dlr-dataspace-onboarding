## Introduction

In this part you will create an `Offer` and make it available in the `Dataspace`.

## Create Asset

The first step is to create an `Asset` for a file in some bucket of an `AmazonS3` storage. This `Asset` will later be available to others as an `Offer` by creating a `Contract Definition`.

The `Asset` contains all necessary information for the `Connector` to later retrieve the file as well as descriptions for others to see.

## Create Access Policy

The next step is to create a `Policy Definition` that will be used as the `Access Policy` for the `Offer`.

The specific `Policy` here madates to present `BpnCredential`. All `Participants` of the `Dataspace` already possess this `Credential` by default and the `Connectors` will automatically present this `Credential` when communicating with one another.

## Create Contract Policy

Similar to the last step, here another `Policy Definition` is created. It will later be used as the `Contract Policy` for the `Offer`.

The specific `Policy` here mandates to have the `Business Partner Number` of `Bob` which acts as a unique identifier for `Participants` in the `Dataspace`.

## Create Contract Definition

In this step a `Contract Definition` with the `Access Policy` and the `Contract Policy` from the previous steps is created. The `Assets Selector` is set to only select the `Asset` with the specific `ID` of the `Asset` created in the first step.

Upon requesting the `Catalog` the `Connector` will look through all `Contract Definitions` whose `Access Policy` is fulfilled and create an `Offer` for each `Asset` selected in the `Asset Selectors`.
