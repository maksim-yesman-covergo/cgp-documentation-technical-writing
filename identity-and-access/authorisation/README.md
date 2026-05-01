---
description: >-
  Roles, user groups, and the catalogue of authorisation resources they draw
  from.
layout:
  width: wide
---

# Authorisation

Authorisation is what each user is allowed to do once they're signed in. The platform builds a user's effective access from **roles** assigned to them and from **user groups** they belong to. Both roles and user groups draw their permissions from **authorisation resources** — the catalogue of permissions exposed by every resource type on the platform.

## Key concepts

- **Role.** A named bundle of permissions. Roles can be assigned to individual users or to user groups. See [Roles](roles.md).
- **User group.** A named collection of users — for example, "Operations" or "Support". Roles and permissions assigned to the group apply to every user in it. See [User Groups](user-groups.md).
- **Permission.** A single, atomic access control on one action against one resource. Permissions are short verbs scoped to a resource — on the `User` resource, for example, the available permissions are `read`, `list`, `create`, `update`, and `delete`.
- **Permission group.** A named collection of permissions on a single resource. For example, on `User` the `readonly` group bundles `read` and `list`, and the `manage` group bundles `read`, `list`, `create`, and `update`. Permission groups simplify what roles look like — instead of picking individual permissions, you grant a group.
- **Authorisation resource.** The catalogue that defines what permissions and permission groups exist for each resource type — User, Role, Document, and so on. The platform ships with system-defined authorisation resources, and developers can also define their own. See [Authorisation Resources](authorisation-resources.md).

## How the building blocks fit together

A user gets the access they need through:

- **Roles** assigned directly to the user.
- **User groups** they belong to (which carry their own roles or permission groups).

A user's effective access is the union of everything granted by their roles and their group memberships. Permissions are not assigned to a user directly — they're always granted through a role or a group. This keeps individual user records simple, and makes wide-scale access changes (e.g. "everyone in Support now also needs read access to Claims") quick and consistent.

## More in this chapter

- [Roles](roles.md) — bundle permissions into named roles.
- [User Groups](user-groups.md) — organise users for collective access management.
- [Authorisation Resources](authorisation-resources.md) — the catalogue of permissions, including custom resources defined via the API.

## Related pages

- [Users](../users.md) — assign roles and group membership on individual user records.
- [Authentication](../authentication/README.md) — how the people you authorise here actually sign in.
