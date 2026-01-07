# Azure Storage Accounts

Azure Storage Accounts are used to store files and data in the cloud.

## Setup

To create a new Storage Account:

### Basics

1. Go to the Azure Portal and start creating a **Storage Account**.
2. Under the **Basics** tab, select the appropriate resource group and provide a name (e.g., `stbolk`).
3. For **Preferred storage type**, choose **Azure Blob Storage or Azure Data Lake Storage Gen2**.
4. Leave the remaining options at their default values unless you have specific requirements.

### Advanced

No changes are required here. Optionally, you can enable the hierarchical namespace for Power BI or other advanced scenarios.

### Networking

Leave the default options unless you need to restrict access to specific networks.

### Data Protection

Keep the default values.

### Encryption

Keep the default values.

### Tags

Add tags only if necessary for resource management or cost tracking.

## Containers

Before you can store data, you need to create a container in your storage account. Containers organize blobs (files) within your storage account.

To create a container:

1. In the Azure Portal, navigate to your Storage Account.
2. In the left menu, select **Containers**.
3. Click **+ Container** to add a new container.
4. Enter a name for your container (e.g., `dwh`, `backups`).

## Connect

To connect to the storage account:

1. In the Azure Portal, navigate to your Storage Account.
2. In the left panel, select **Access keys**.
3. Copy one of the **connection strings** provided.
4. Use this connection string with the `azure-storage-blob` Python package to access your storage account programmatically.

### Example (Python)

Install the required package:

```
uv add azure-storage-blob
```

Sample code to connect and list blobs in a container:

```
from azure.storage.blob import BlobServiceClient

connection_string = "<your-connection-string>"  # Replace with your actual connection string
container_name = "<your-container-name>"        # Replace with your container name

blob_service_client = BlobServiceClient.from_connection_string(connection_string)
container_client = blob_service_client.get_container_client(container_name)

print("Blobs in container:")
for blob in container_client.list_blobs():
	print(blob.name)
```

Replace `<your-connection-string>` and `<your-container-name>` with your actual values.
