### etcdserverpb


##### service `Auth` ([testdata/rpc.proto](../testdata/rpc.proto))

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| AuthEnable | AuthEnableRequest | AuthEnableResponse | AuthEnable enables authentication. |
| AuthDisable | AuthDisableRequest | AuthDisableResponse | AuthDisable disables authentication. |
| Authenticate | AuthenticateRequest | AuthenticateResponse | Authenticate processes an authenticate request. |
| UserAdd | AuthUserAddRequest | AuthUserAddResponse | UserAdd adds a new user. |
| UserGet | AuthUserGetRequest | AuthUserGetResponse | UserGet gets detailed user information or lists all users. |
| UserDelete | AuthUserDeleteRequest | AuthUserDeleteResponse | UserDelete deletes a specified user. |
| UserChangePassword | AuthUserChangePasswordRequest | AuthUserChangePasswordResponse | UserChangePassword changes the password of a specified user. |
| UserGrantRole | AuthUserGrantRoleRequest | AuthUserGrantRoleResponse | UserGrant grants a role to a specified user. |
| UserRevokeRole | AuthUserRevokeRoleRequest | AuthUserRevokeRoleResponse | UserRevokeRole revokes a role of specified user. |
| RoleAdd | AuthRoleAddRequest | AuthRoleAddResponse | RoleAdd adds a new role. |
| RoleGet | AuthRoleGetRequest | AuthRoleGetResponse | RoleGet gets detailed role information or lists all roles. |
| RoleDelete | AuthRoleDeleteRequest | AuthRoleDeleteResponse | RoleDelete deletes a specified role. |
| RoleGrantPermission | AuthRoleGrantPermissionRequest | AuthRoleGrantPermissionResponse | RoleGrantPermission grants a permission of a specified key or range to a specified role. |
| RoleRevokePermission | AuthRoleRevokePermissionRequest | AuthRoleRevokePermissionResponse | RoleRevokePermission revokes a key or range permission of a specified role. |



##### service `Cluster` ([testdata/rpc.proto](../testdata/rpc.proto))

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| MemberAdd | MemberAddRequest | MemberAddResponse | MemberAdd adds a member into the cluster. |
| MemberRemove | MemberRemoveRequest | MemberRemoveResponse | MemberRemove removes an existing member from the cluster. |
| MemberUpdate | MemberUpdateRequest | MemberUpdateResponse | MemberUpdate updates the member configuration. |
| MemberList | MemberListRequest | MemberListResponse | MemberList lists all the members in the cluster. |



##### service `KV` ([testdata/rpc.proto](../testdata/rpc.proto))

for grpc-gateway

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| Range | RangeRequest | RangeResponse | Range gets the keys in the range from the key-value store. |
| Put | PutRequest | PutResponse | Put puts the given key into the key-value store. A put request increments the revision of the key-value store and generates one event in the event history. |
| DeleteRange | DeleteRangeRequest | DeleteRangeResponse | DeleteRange deletes the given range from the key-value store. A delete request increments the revision of the key-value store and generates a delete event in the event history for every deleted key. |
| Txn | TxnRequest | TxnResponse | Txn processes multiple requests in a single transaction. A txn request increments the revision of the key-value store and generates events with the same revision for every completed request. It is not allowed to modify the same key several times within one txn. |
| Compact | CompactionRequest | CompactionResponse | Compact compacts the event history in the etcd key-value store. The key-value store should be periodically compacted or the event history will continue to grow indefinitely. |



##### service `Lease` ([testdata/rpc.proto](../testdata/rpc.proto))

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| LeaseGrant | LeaseGrantRequest | LeaseGrantResponse | LeaseGrant creates a lease which expires if the server does not receive a keepAlive within a given time to live period. All keys attached to the lease will be expired and deleted if the lease expires. Each expired key generates a delete event in the event history. |
| LeaseRevoke | LeaseRevokeRequest | LeaseRevokeResponse | LeaseRevoke revokes a lease. All keys attached to the lease will expire and be deleted. |
| LeaseKeepAlive | LeaseKeepAliveRequest | LeaseKeepAliveResponse | LeaseKeepAlive keeps the lease alive by streaming keep alive requests from the client to the server and streaming keep alive responses from the server to the client. |



##### service `Maintenance` ([testdata/rpc.proto](../testdata/rpc.proto))

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| Alarm | AlarmRequest | AlarmResponse | Alarm activates, deactivates, and queries alarms regarding cluster health. |
| Status | StatusRequest | StatusResponse | Status gets the status of the member. |
| Defragment | DefragmentRequest | DefragmentResponse | Defragment defragments a member's backend database to recover storage space. |
| Hash | HashRequest | HashResponse | Hash returns the hash of the local KV state for consistency checking purpose. This is designed for testing; do not use this in production when there are ongoing transactions. |
| Snapshot | SnapshotRequest | SnapshotResponse | Snapshot sends a snapshot of the entire backend from a member over a stream to a client. |



##### service `Watch` ([testdata/rpc.proto](../testdata/rpc.proto))

| Method | Request Type | Response Type | Description |
| ------ | ------------ | ------------- | ----------- |
| Watch | WatchRequest | WatchResponse | Watch watches for events happening or that have happened. Both input and output are streams; the input stream is for creating and canceling watchers and the output stream sends events. One watch RPC can watch on multiple key ranges, streaming events for several watches at once. The entire event history can be watched starting from the last compaction revision. |



##### service `AlarmMember` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| memberID | memberID is the ID of the member associated with the raised alarm. | uint64 | uint64 | long | int/long | uint64 |
| alarm | alarm is the type of alarm which has been raised. | AlarmType | | | | |



##### service `AlarmRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

default, used to query if any alarm is active space quota is exhausted

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| action | action is the kind of alarm request to issue. The action may GET alarm statuses, ACTIVATE an alarm, or DEACTIVATE a raised alarm. | AlarmAction | | | | |
| memberID | memberID is the ID of the member associated with the alarm. If memberID is 0, the alarm request covers all members. | uint64 | uint64 | long | int/long | uint64 |
| alarm | alarm is the type of alarm to consider for this request. | AlarmType | | | | |



##### service `AlarmResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| alarms | alarms is a list of alarms associated with the alarm request. | (slice of) AlarmMember | | | | |



##### service `AuthDisableRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `AuthDisableResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthEnableRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `AuthEnableResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthRoleAddRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name | name is the name of the role to add to the authentication system. | string | string | String | str/unicode | string |



##### service `AuthRoleAddResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthRoleDeleteRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| role |  | string | string | String | str/unicode | string |



##### service `AuthRoleDeleteResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthRoleGetRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| role |  | string | string | String | str/unicode | string |



##### service `AuthRoleGetResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| perm |  | (slice of) authpb.Permission | | | | |



##### service `AuthRoleGrantPermissionRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name | name is the name of the role which will be granted the permission. | string | string | String | str/unicode | string |
| perm | perm is the permission to grant to the role. | authpb.Permission | | | | |



##### service `AuthRoleGrantPermissionResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthRoleRevokePermissionRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| role |  | string | string | String | str/unicode | string |
| key |  | string | string | String | str/unicode | string |
| range_end |  | string | string | String | str/unicode | string |



##### service `AuthRoleRevokePermissionResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthUserAddRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name |  | string | string | String | str/unicode | string |
| password |  | string | string | String | str/unicode | string |



##### service `AuthUserAddResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthUserChangePasswordRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name | name is the name of the user whose password is being changed. | string | string | String | str/unicode | string |
| password | password is the new password for the user. | string | string | String | str/unicode | string |



##### service `AuthUserChangePasswordResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthUserDeleteRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name | name is the name of the user to delete. | string | string | String | str/unicode | string |



##### service `AuthUserDeleteResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthUserGetRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name |  | string | string | String | str/unicode | string |



##### service `AuthUserGetResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| roles |  | (slice of) string | (slice of) string | (slice of) String | (slice of) str/unicode | (slice of) string |



##### service `AuthUserGrantRoleRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| user | user is the name of the user which should be granted a given role. | string | string | String | str/unicode | string |
| role | role is the name of the role to grant to the user. | string | string | String | str/unicode | string |



##### service `AuthUserGrantRoleResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthUserRevokeRoleRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name |  | string | string | String | str/unicode | string |
| role |  | string | string | String | str/unicode | string |



##### service `AuthUserRevokeRoleResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `AuthenticateRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name |  | string | string | String | str/unicode | string |
| password |  | string | string | String | str/unicode | string |



##### service `AuthenticateResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| token | token is an authorized token that can be used in succeeding RPCs | string | string | String | str/unicode | string |



##### service `CompactionRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

CompactionRequest compacts the key-value store up to a given revision. All superseded keys with a revision less than the compaction revision will be removed.

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| revision | revision is the key-value store revision for the compaction operation. | int64 | int64 | long | int/long | int64 |
| physical | physical is set so the RPC will wait until the compaction is physically applied to the local database such that compacted entries are totally removed from the backend database. | bool | bool | boolean | boolean | bool |



##### service `CompactionResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `Compare` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| result | result is logical comparison operation for this comparison. | CompareResult | | | | |
| target | target is the key-value field to inspect for the comparison. | CompareTarget | | | | |
| key | key is the subject key for the comparison operation. | bytes | []byte | ByteString | str | string |
| target_union |  | oneof | | | | |
| version | version is the version of the given key | int64 | int64 | long | int/long | int64 |
| create_revision | create_revision is the creation revision of the given key | int64 | int64 | long | int/long | int64 |
| mod_revision | mod_revision is the last modified revision of the given key. | int64 | int64 | long | int/long | int64 |
| value | value is the value of the given key, in bytes. | bytes | []byte | ByteString | str | string |



##### service `DefragmentRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `DefragmentResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `DeleteRangeRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| key | key is the first key to delete in the range. | bytes | []byte | ByteString | str | string |
| range_end | range_end is the key following the last key to delete for the range [key, range_end). If range_end is not given, the range is defined to contain only the key argument. If range_end is '\0', the range is all keys greater than or equal to the key argument. | bytes | []byte | ByteString | str | string |



##### service `DeleteRangeResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| deleted | deleted is the number of keys deleted by the delete range request. | int64 | int64 | long | int/long | int64 |



##### service `EmptyResponse` ([testdata/raft_internal.proto](../testdata/raft_internal.proto))

Empty field.



##### service `HashRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `HashResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| hash | hash is the hash value computed from the responding member's key-value store. | uint32 | uint32 | int | int/long | uint32 |



##### service `InternalAuthenticateRequest` ([testdata/raft_internal.proto](../testdata/raft_internal.proto))

What is the difference between AuthenticateRequest (defined in rpc.proto) and InternalAuthenticateRequest? InternalAuthenticateRequest has a member that is filled by etcdserver and shouldn't be user-facing. For avoiding misusage the field, we have an internal version of AuthenticateRequest.

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| name |  | string | string | String | str/unicode | string |
| password |  | string | string | String | str/unicode | string |
| simple_token | simple_token is generated in API layer (etcdserver/v3_server.go) | string | string | String | str/unicode | string |



##### service `InternalRaftRequest` ([testdata/raft_internal.proto](../testdata/raft_internal.proto))

An InternalRaftRequest is the union of all requests which can be sent via raft.

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | RequestHeader | | | | |
| ID |  | uint64 | uint64 | long | int/long | uint64 |
| v2 |  | Request | | | | |
| range |  | RangeRequest | | | | |
| put |  | PutRequest | | | | |
| delete_range |  | DeleteRangeRequest | | | | |
| txn |  | TxnRequest | | | | |
| compaction |  | CompactionRequest | | | | |
| lease_grant |  | LeaseGrantRequest | | | | |
| lease_revoke |  | LeaseRevokeRequest | | | | |
| alarm |  | AlarmRequest | | | | |
| auth_enable |  | AuthEnableRequest | | | | |
| auth_disable |  | AuthDisableRequest | | | | |
| authenticate |  | InternalAuthenticateRequest | | | | |
| auth_user_add |  | AuthUserAddRequest | | | | |
| auth_user_delete |  | AuthUserDeleteRequest | | | | |
| auth_user_get |  | AuthUserGetRequest | | | | |
| auth_user_change_password |  | AuthUserChangePasswordRequest | | | | |
| auth_user_grant_role |  | AuthUserGrantRoleRequest | | | | |
| auth_user_revoke_role |  | AuthUserRevokeRoleRequest | | | | |
| auth_role_add |  | AuthRoleAddRequest | | | | |
| auth_role_delete |  | AuthRoleDeleteRequest | | | | |
| auth_role_get |  | AuthRoleGetRequest | | | | |
| auth_role_grant_permission |  | AuthRoleGrantPermissionRequest | | | | |
| auth_role_revoke_permission |  | AuthRoleRevokePermissionRequest | | | | |



##### service `LeaseGrantRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| TTL | TTL is the advisory time-to-live in seconds. | int64 | int64 | long | int/long | int64 |
| ID | ID is the requested ID for the lease. If ID is set to 0, the lessor chooses an ID. | int64 | int64 | long | int/long | int64 |



##### service `LeaseGrantResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| ID | ID is the lease ID for the granted lease. | int64 | int64 | long | int/long | int64 |
| TTL | TTL is the server chosen lease time-to-live in seconds. | int64 | int64 | long | int/long | int64 |
| error |  | string | string | String | str/unicode | string |



##### service `LeaseKeepAliveRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID | ID is the lease ID for the lease to keep alive. | int64 | int64 | long | int/long | int64 |



##### service `LeaseKeepAliveResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| ID | ID is the lease ID from the keep alive request. | int64 | int64 | long | int/long | int64 |
| TTL | TTL is the new time-to-live for the lease. | int64 | int64 | long | int/long | int64 |



##### service `LeaseRevokeRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID | ID is the lease ID to revoke. When the ID is revoked, all associated keys will be deleted. | int64 | int64 | long | int/long | int64 |



##### service `LeaseRevokeResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `Member` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID | ID is the member ID for this member. | uint64 | uint64 | long | int/long | uint64 |
| name | name is the human-readable name of the member. If the member is not started, the name will be an empty string. | string | string | String | str/unicode | string |
| peerURLs | peerURLs is the list of URLs the member exposes to the cluster for communication. | (slice of) string | (slice of) string | (slice of) String | (slice of) str/unicode | (slice of) string |
| clientURLs | clientURLs is the list of URLs the member exposes to clients for communication. If the member is not started, clientURLs will be empty. | (slice of) string | (slice of) string | (slice of) String | (slice of) str/unicode | (slice of) string |



##### service `MemberAddRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| peerURLs | peerURLs is the list of URLs the added member will use to communicate with the cluster. | (slice of) string | (slice of) string | (slice of) String | (slice of) str/unicode | (slice of) string |



##### service `MemberAddResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| member | member is the member information for the added member. | Member | | | | |



##### service `MemberListRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `MemberListResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| members | members is a list of all members associated with the cluster. | (slice of) Member | | | | |



##### service `MemberRemoveRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID | ID is the member ID of the member to remove. | uint64 | uint64 | long | int/long | uint64 |



##### service `MemberRemoveResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `MemberUpdateRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID | ID is the member ID of the member to update. | uint64 | uint64 | long | int/long | uint64 |
| peerURLs | peerURLs is the new list of URLs the member will use to communicate with the cluster. | (slice of) string | (slice of) string | (slice of) String | (slice of) str/unicode | (slice of) string |



##### service `MemberUpdateResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `Metadata` ([testdata/etcdserver.proto](../testdata/etcdserver.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| NodeID |  | uint64 | uint64 | long | int/long | uint64 |
| ClusterID |  | uint64 | uint64 | long | int/long | uint64 |



##### service `PutRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| key | key is the key, in bytes, to put into the key-value store. | bytes | []byte | ByteString | str | string |
| value | value is the value, in bytes, to associate with the key in the key-value store. | bytes | []byte | ByteString | str | string |
| lease | lease is the lease ID to associate with the key in the key-value store. A lease value of 0 indicates no lease. | int64 | int64 | long | int/long | int64 |



##### service `PutResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |



##### service `RangeRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| key | default, no sorting lowest target value first highest target value first key is the first key for the range. If range_end is not given, the request only looks up key. | bytes | []byte | ByteString | str | string |
| range_end | range_end is the upper bound on the requested range [key, range_end). If range_end is '\0', the range is all keys >= key. If the range_end is one bit larger than the given key, then the range requests get the all keys with the prefix (the given key). If both key and range_end are '\0', then range requests returns all keys. | bytes | []byte | ByteString | str | string |
| limit | limit is a limit on the number of keys returned for the request. | int64 | int64 | long | int/long | int64 |
| revision | revision is the point-in-time of the key-value store to use for the range. If revision is less or equal to zero, the range is over the newest key-value store. If the revision has been compacted, ErrCompacted is returned as a response. | int64 | int64 | long | int/long | int64 |
| sort_order | sort_order is the order for returned sorted results. | SortOrder | | | | |
| sort_target | sort_target is the key-value field to use for sorting. | SortTarget | | | | |
| serializable | serializable sets the range request to use serializable member-local reads. Range requests are linearizable by default; linearizable requests have higher latency and lower throughput than serializable requests but reflect the current consensus of the cluster. For better performance, in exchange for possible stale reads, a serializable range request is served locally without needing to reach consensus with other nodes in the cluster. | bool | bool | boolean | boolean | bool |



##### service `RangeResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| kvs | kvs is the list of key-value pairs matched by the range request. | (slice of) mvccpb.KeyValue | | | | |
| more | more indicates if there are more keys to return in the requested range. | bool | bool | boolean | boolean | bool |



##### service `Request` ([testdata/etcdserver.proto](../testdata/etcdserver.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID |  | uint64 | uint64 | long | int/long | uint64 |
| Method |  | string | string | String | str/unicode | string |
| Path |  | string | string | String | str/unicode | string |
| Val |  | string | string | String | str/unicode | string |
| Dir |  | bool | bool | boolean | boolean | bool |
| PrevValue |  | string | string | String | str/unicode | string |
| PrevIndex |  | uint64 | uint64 | long | int/long | uint64 |
| PrevExist |  | bool | bool | boolean | boolean | bool |
| Expiration |  | int64 | int64 | long | int/long | int64 |
| Wait |  | bool | bool | boolean | boolean | bool |
| Since |  | uint64 | uint64 | long | int/long | uint64 |
| Recursive |  | bool | bool | boolean | boolean | bool |
| Sorted |  | bool | bool | boolean | boolean | bool |
| Quorum |  | bool | bool | boolean | boolean | bool |
| Time |  | int64 | int64 | long | int/long | int64 |
| Stream |  | bool | bool | boolean | boolean | bool |
| Refresh |  | bool | bool | boolean | boolean | bool |



##### service `RequestHeader` ([testdata/raft_internal.proto](../testdata/raft_internal.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| ID |  | uint64 | uint64 | long | int/long | uint64 |
| username | username is a username that is associated with an auth token of gRPC connection | string | string | String | str/unicode | string |



##### service `RequestOp` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| request | request is a union of request types accepted by a transaction. | oneof | | | | |
| request_range |  | RangeRequest | | | | |
| request_put |  | PutRequest | | | | |
| request_delete_range |  | DeleteRangeRequest | | | | |



##### service `ResponseHeader` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| cluster_id | cluster_id is the ID of the cluster which sent the response. | uint64 | uint64 | long | int/long | uint64 |
| member_id | member_id is the ID of the member which sent the response. | uint64 | uint64 | long | int/long | uint64 |
| revision | revision is the key-value store revision when the request was applied. | int64 | int64 | long | int/long | int64 |
| raft_term | raft_term is the raft term when the request was applied. | uint64 | uint64 | long | int/long | uint64 |



##### service `ResponseOp` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| response | response is a union of response types returned by a transaction. | oneof | | | | |
| response_range |  | RangeResponse | | | | |
| response_put |  | PutResponse | | | | |
| response_delete_range |  | DeleteRangeResponse | | | | |



##### service `SnapshotRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `SnapshotResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header | header has the current key-value store information. The first header in the snapshot stream indicates the point in time of the snapshot. | ResponseHeader | | | | |
| remaining_bytes | remaining_bytes is the number of blob bytes to be sent after this message | uint64 | uint64 | long | int/long | uint64 |
| blob | blob contains the next chunk of the snapshot in the snapshot stream. | bytes | []byte | ByteString | str | string |



##### service `StatusRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

Empty field.



##### service `StatusResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| version | version is the cluster protocol version used by the responding member. | string | string | String | str/unicode | string |
| dbSize | dbSize is the size of the backend database, in bytes, of the responding member. | int64 | int64 | long | int/long | int64 |
| leader | leader is the member ID which the responding member believes is the current leader. | uint64 | uint64 | long | int/long | uint64 |
| raftIndex | raftIndex is the current raft index of the responding member. | uint64 | uint64 | long | int/long | uint64 |
| raftTerm | raftTerm is the current raft term of the responding member. | uint64 | uint64 | long | int/long | uint64 |



##### service `TxnRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

From google paxosdb paper: Our implementation hinges around a powerful primitive which we call MultiOp. All other database operations except for iteration are implemented as a single call to MultiOp. A MultiOp is applied atomically and consists of three components: 1. A list of tests called guard. Each test in guard checks a single entry in the database. It may check for the absence or presence of a value, or compare with a given value. Two different tests in the guard may apply to the same or different entries in the database. All tests in the guard are applied and MultiOp returns the results. If all tests are true, MultiOp executes t op (see item 2 below), otherwise it executes f op (see item 3 below). 2. A list of database operations called t op. Each operation in the list is either an insert, delete, or lookup operation, and applies to a single database entry. Two different operations in the list may apply to the same or different entries in the database. These operations are executed if guard evaluates to true. 3. A list of database operations called f op. Like t op, but executed if guard evaluates to false.

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| compare | compare is a list of predicates representing a conjunction of terms. If the comparisons succeed, then the success requests will be processed in order, and the response will contain their respective responses in order. If the comparisons fail, then the failure requests will be processed in order, and the response will contain their respective responses in order. | (slice of) Compare | | | | |
| success | success is a list of requests which will be applied when compare evaluates to true. | (slice of) RequestOp | | | | |
| failure | failure is a list of requests which will be applied when compare evaluates to false. | (slice of) RequestOp | | | | |



##### service `TxnResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| succeeded | succeeded is set to true if the compare evaluated to true or false otherwise. | bool | bool | boolean | boolean | bool |
| responses | responses is a list of responses corresponding to the results from applying success if succeeded is true or failure if succeeded is false. | (slice of) ResponseOp | | | | |



##### service `WatchCancelRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| watch_id | watch_id is the watcher id to cancel so that no more events are transmitted. | int64 | int64 | long | int/long | int64 |



##### service `WatchCreateRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| key | key is the key to register for watching. | bytes | []byte | ByteString | str | string |
| range_end | range_end is the end of the range [key, range_end) to watch. If range_end is not given, only the key argument is watched. If range_end is equal to '\0', all keys greater than or equal to the key argument are watched. | bytes | []byte | ByteString | str | string |
| start_revision | start_revision is an optional revision to watch from (inclusive). No start_revision is "now". | int64 | int64 | long | int/long | int64 |
| progress_notify | progress_notify is set so that the etcd server will periodically send a WatchResponse with no events to the new watcher if there are no recent events. It is useful when clients wish to recover a disconnected watcher starting from a recent known revision. The etcd server may decide how often it will send notifications based on current load. | bool | bool | boolean | boolean | bool |



##### service `WatchRequest` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| request_union | request_union is a request to either create a new watcher or cancel an existing watcher. | oneof | | | | |
| create_request |  | WatchCreateRequest | | | | |
| cancel_request |  | WatchCancelRequest | | | | |



##### service `WatchResponse` ([testdata/rpc.proto](../testdata/rpc.proto))

| Field | Description | Type | Go | Java | Python | C++ |
| ----- | ----------- | ---- | --- | ---- | ------ | --- |
| header |  | ResponseHeader | | | | |
| watch_id | watch_id is the ID of the watcher that corresponds to the response. | int64 | int64 | long | int/long | int64 |
| created | created is set to true if the response is for a create watch request. The client should record the watch_id and expect to receive events for the created watcher from the same stream. All events sent to the created watcher will attach with the same watch_id. | bool | bool | boolean | boolean | bool |
| canceled | canceled is set to true if the response is for a cancel watch request. No further events will be sent to the canceled watcher. | bool | bool | boolean | boolean | bool |
| compact_revision | compact_revision is set to the minimum index if a watcher tries to watch at a compacted index.  This happens when creating a watcher at a compacted revision or the watcher cannot catch up with the progress of the key-value store.  The client should treat the watcher as canceled and should not try to create any watcher with the same start_revision again. | int64 | int64 | long | int/long | int64 |
| events |  | (slice of) mvccpb.Event | | | | |



