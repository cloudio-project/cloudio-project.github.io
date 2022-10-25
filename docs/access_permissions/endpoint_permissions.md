# Endpoint permissions

The endpoint permissions can be granted to users/user groups on whole endpoints/endpoint groups.

#### DENY
Access to the endpoint is denied for the user or the group. This is the default permission if no other permission is available.

#### ACCESS
The user or group can access part of the endpoint, and only the part of the endpoint's data model that is accessible is visible to the user.

#### BROWSE
The user or group can access part of the endpoint but the complete data model of the endpoint can be discovered, even the parts the user does not have access to.
     
*ACCESS* + browsing of data model.

#### READ
The user or group can read from the endpoint's data model. This includes the history for all data model elements.

*BROWSE* + read all attribute's values.

#### WRITE
The user or group can read and modify from/to the endpoint's data model. This includes the history for all data model elements.

*READ* + write to attributes.

#### CONFIGURE
The user or group can read and write from/to all attributes of the endpoint, and additionally modify the endpoint's settings.

*WRITE* + endpoint settings access.

#### GRANT
The user or the group can manage the endpoints settings, read and write from/to all attributes and additionally grant access to other users or group.

*CONFIGURE* + granting access to endpoint for other users/groups.

#### OWN
The user owns the endpoint. Only one user can own the endpoint at a given time. Only the user that owns the endpoint is able to delete it.

*GRANT* + delete endpoint.
