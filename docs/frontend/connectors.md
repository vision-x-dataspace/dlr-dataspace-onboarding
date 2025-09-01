# Connectors

Connect your storage resources to the dataspace.

The Connectors page is central to your dataspace experience, allowing you to securely link your storage systems to the platform. Connectors enable seamless data exchange while maintaining control over your assets at all times.

!!! info
    Currently, the DLR Dataspace supports Amazon S3 and Azure Storage connectors, with more integrations planned for future releases.

## Creating a Connector

The connector creation process is straightforward and guided:

1. **Select connector type**
2. **Configure connection details**
3. **Set access permissions** 
4. **Test and validate connection**

To create a new connector, click the **"+ New Connector"** button in the top-right corner of the Connectors page and follow the setup wizard.

## Managing Connectors

Once created, you can manage your connectors from the main Connectors dashboard:

- **View status and health** - Monitor the connection status and synchronization health
- **Delete connector** - Remove a connector when it's no longer needed

## Supported Connector Types

### Amazon S3
Full integration with AWS S3 buckets

### Azure Storage  
Connect to Microsoft Azure Blob Storage

## Authentication & Security

For secure access to your storage systems, you'll need to provide appropriate authentication:

### Amazon S3 Authentication
- Access Key ID
- Secret Access Key
- Region
- Bucket Name

### Azure Storage Authentication
- Storage Account Name
- Storage Account Key
- Container Name
- Connection String (optional)

**Note:** All credentials are encrypted and securely stored. The DLR Dataspace platform never stores your raw credentials in plain text and uses industry-standard encryption methods.

!!! tip "Pro Tip"
    Set up at least one connector before exploring other parts of the platform. Without an active connector, you won't be able to share your data assets or create offers for other participants. Think of connectors as the foundation for all other dataspace activities.