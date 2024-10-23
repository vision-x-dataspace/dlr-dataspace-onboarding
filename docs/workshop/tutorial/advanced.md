# 5. Advanced Topics

To get an overview of the full capabilities of the **Connector**, please check out the official [documentation](https://eclipse-edc.github.io/documentation/). Also have a look at the [API documentation](https://app.swaggerhub.com/apis/eclipse-tractusx-bot/tractusx-edc/0.6.0#/).

## Task 1

### Filter Catalog I

*Task:* Try the API to filter the catalog from Bobs connector to only get all assets where the id starts with `asset-`.

??? note "Tip 1"
    For the counterPartyAddress you need `http://bob-controlplane:8084/api/v1/dsp`.

??? success "Solution"
    You can download the solution postman collection [here](../../collections/Vision-X_Dataspace_Advanced.postman_collection.json).

## Task 2

### Filter Catalog II

*Task:* Try the API to get a single asset with id `asset-1`.

??? note "Tip 1"
    You can try a similar approach to the above approach. The operator can be changed to `=`.

??? success "Solution"
    You can download the solution postman collection [here](../../collections/Vision-X_Dataspace_Advanced.postman_collection.json).

## Task 3

### Contract Definition

*Task:* Try the API to create a Contract Definition where all Members can see your Asset but only Connector with a specific BPN can successfully negotiate.

??? note "Tip 1"
    First, you will need to create one new policy at least.

??? note "Tip 2"
    Remember: An Access Policy determines the members who can see your contract and a Contract Policy determines who can successfully negotiate.

??? success "Solution"
    You can download the solution postman collection [here](../../collections/Vision-X_Dataspace_Advanced.postman_collection.json).
