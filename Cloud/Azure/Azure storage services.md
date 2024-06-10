
- **Azure Blobs**: A massively scalable object store for text and binary data. Also includes support for big data analytics through Data Lake Storage Gen2.
- **Azure Files**: Managed file shares for cloud or on-premises deployments.
- **Azure Queues**: A messaging store for reliable messaging between application components.
- **Azure Disks**: Block-level storage volumes for Azure VMs.
- **Azure Tables:** NoSQL table option for structured, non-relational data.

## Azure Blob storage 

- object store solution
- unstructured 
- aren't limited to common file formats

Advantages:
* does not require developers to think about or manage disks (Azure takes care of the physical storage needs)

Ideal for:
- Serving images or documents directly to a browser.
- Storing files for distributed access.
- Streaming video and audio.
- Storing data for backup and restore, disaster recovery, and archiving.
- Storing data for analysis by an on-premises or Azure-hosted service.

- **Hot access tier**: Optimized for storing data that is accessed frequently (for example, images for your website).
- **Cool access tier**: Optimized for data that is infrequently accessed and stored for at least 30 days (for example, invoices for your customers).
- **Cold access tier**: Optimized for storing data that is infrequently accessed and stored for at least 90 days.
- **Archive access tier**: Appropriate for data that is rarely accessed and stored for at least 180 days, with flexible latency requirements (for example, long-term backups).


## Azure files

Managed file shares for cloud or on-premises deployments.

Benefits:
* shared access
* fully managed 
* resiliency


## Azure Queues 

Stores large number of messages.

commonly used to create a backlog of work to process asynchronously

## Azure Disks

block-level storage volumes managed by Azure for use with Azure VMs

The same as physical disks (virtualized)

## Azure Tables

stores larges amounts of structured data

NoSQL 

ideal for storing structured, non-relational data.


