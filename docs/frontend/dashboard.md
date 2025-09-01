# Dashboard

Your central command center for dataspace management.

The Dashboard provides at-a-glance visibility into your dataspace environment, connector status, and group memberships. From here, you can monitor your integration health, understand the organizational structure, and manage your storage connectors.

!!! info
    Currently, the DLR Dataspace supports S3 connectors, with more integrations planned for future releases.

## Connector Management

### Connector Status

The top section of the Dashboard displays the real-time status of your connector:

- **Connection status indicator** - Shows whether your connector is online, offline, or experiencing issues
- **Quick action buttons** - Restart connector, trigger synchronization, or access settings

### Creating a Connector

The connector creation process is straightforward and guided:

1. Select connector type
2. Configure connection details  
3. Set access permissions
4. Test and validate connection

To create a new connector, click the **"+ New Connector"** button in the top-right corner of the Connectors panel.

## Supported Connector Types

### Amazon S3
Connect to AWS S3 buckets for object storage

**Authentication Requirements:**
- Access Key ID
- Secret Access Key
- Region
- Bucket Name

**Note:** All credentials are encrypted and securely stored. The DLR Dataspace platform never stores your raw credentials in plain text and uses industry-standard encryption methods.

## Managing Connectors

Once created, you can manage your connectors from the Dashboard:

- **View status and health** - Monitor the connection status and synchronization health
- **Delete connector** - Remove a connector when it's no longer needed

### Removing a Connector

When you no longer need a connector, you can remove it from your dataspace:

1. Find the connector card on the Connectors page
2. Click on the 'Delete' button
3. Confirm deletion when prompted

**Important:** Removing a connector will:
- Remove all assets linked to this connector from the dataspace catalog
- Revoke any pending offers for assets from this connector  
- Delete the connection credentials from the platform (your actual storage remains untouched)

## Group Visualization & Management

### Interactive Group Visualization

The central feature of the Dashboard is an interactive pie chart visualization:

- **Group distribution** - Visual representation of all groups in the dataspace
- **Click-through navigation** - Select any segment to view detailed information about that group
- **Member count indicators** - See how many users belong to each group at a glance

!!! tip "Pro Tip"
    The Dashboard serves as both your command center and connector management hub. Set up at least one connector before exploring other parts of the platform, as without an active connector, you won't be able to share assets or create offers. The visual interface makes it easy to understand the organizational structure and check your connector's health before proceeding to other areas of the platform.