

Azure always **store copies of your data** and it's protected from (planned and unplanned) events as hardware failure, natural disasters, etc. 

Redundancy ensure that your storage account meets its availability and durability targets even in the face of failures


<i>Tradeoff of lower costs and higher availability</i>: ==↑ availability ↑ costs==
- How your data is replicated in the primary region.
- Whether your data is replicated to a second region that is geographically distant to the primary region, to protect against regional disasters.
- Whether your application requires read access to the replicated data in the secondary region if the primary region becomes unavailable.


### Redundancy in the primary region 

Data in Azure storage account is **always replicated 3 times in the primary region**: you choose between locally redundant storage (LRS) and zone-redundant storage (ZRS)

**LRS**
* replicate 3 times in a single data center in the primary region
* at least 11 nines of durability (99.999999999%)
* lowest-cost 
* least durability compared to other option
*  protects your data against server rack and drive failures
* LIMITATION:  if a disaster occurs with entire datacenter, such as fire, all replicas may be lost

**ZRS**
* replicates 3 times across 3 azure availability zones in the primary region
* at least 12 nines durability (99.9999999999%)
![[files/Pasted image 20240515152513.png]]
* Microsoft recommends using ZRS in the primary region for scenarios that require high availability


### Redundancy in the secondary region 

If high durability is required, you can choose to additionally copy in your storage account to a secondary region

When you create a storage account, you select the primary region for the account. The paired secondary region is based on Azure Region Pairs, and can't be changed. 

By default, data isn't in secondary region for read or write, unless the primary region becomes unavailable.

### Geo-redundant storage

GRS copies your data synchronously three times within a single physical location in the primary region using LRS. It then copies your data asynchronously to a single physical location in the secondary region (the region pair) using LRS. GRS offers durability for Azure Storage data objects of at least 16 nines (99.99999999999999%) over a given year.
![[files/Pasted image 20240515155052.png]]
### Geo-zone-redundant storage

* the high availability
* 
