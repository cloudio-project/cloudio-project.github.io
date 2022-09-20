# Element permissions

The element permissions can be granted to users/user groups on any element of endpoints/endpoint groups data model. This allows to manage the permissions with a lot of flexibility.

!> When an element permission is granted to an endpoint/endpoint group, the endpoint *ACCESS* permission will be automatically granted to the user/user group.

#### DENY
Access to the endpoint data model element is denied for the user or the group and all elements that are children of the element itself until another
permission is attributed to one of such elements. This is the default permission if no other permission is available.

#### VIEW
The user or group can see the model element and all it's children. Note that this does not include to read the actual value.

#### READ
The user or group can read the model element and all it's children.

#### WRITE
The user or group can read and write the model element and all it's children.