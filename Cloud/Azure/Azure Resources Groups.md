Resource groups are simply groupings of [[Azure Resources]]. When a resource are created, you're required to place it into a resource group. 

A resource group can contain many resources, a single resource can only be in one resource group at time.

Resource groups can't be nested, meaning you can’t put resource group B inside of resource group A.

Resource groups provide a convenient way to group resources together. When you apply an action to a resource group, that action will apply to all the resources within the resource group. If you delete a resource group, all the resources will be deleted. If you grant or deny access to a resource group, you’ve granted or denied access to all the resources within the resource group.