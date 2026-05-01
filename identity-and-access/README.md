---
description: >-
  Manage who can sign in and what they can do — users, user groups, roles, and
  the catalogue of permissions they draw from.
layout:
  width: wide
---

# Identity and Access

Identity and Access is where you manage the people (and systems) that can sign in to the platform, and what each of them is allowed to do once they're in. You bring users in, organise them into groups, define named roles for the work they do, and grant access by combining the two.

The chapter has four building blocks — **users**, **user groups**, **roles**, and **authorisation resources**. They compose together: a user can belong to zero or more user groups and have zero or more roles assigned directly; both groups and roles draw their access from permissions defined on the authorisation resources the platform exposes.

## Key concepts

- **User.** An account that represents a person, or a system, on the platform. Each user has an email, a username, and a status that controls whether they can sign in. See [Users](users.md).
- **User group.** A named collection of users — for example, "Operations" or "Support". Roles and permissions assigned to the group apply to every user in it. See [User Groups](authorisation/user-groups.md).
- **Role.** A named bundle of permissions — "Claims handler", "Read-only auditor". Roles can be assigned to individual users or to user groups. See [Roles](authorisation/roles.md).
- **Permission.** A single, atomic access control on one action against one resource. Permissions are short verbs scoped to a resource — on the `User` resource, for example, the available permissions are `read`, `list`, `create`, `update`, and `delete`. A permission lets you do exactly that one thing on that one resource type.
- **Permission group.** A named collection of permissions on a single resource. For example, on `User` the `readonly` group bundles `read` and `list`, and the `manage` group bundles `read`, `list`, `create`, and `update`. Permission groups simplify what roles look like — instead of picking individual permissions, you grant a group.
- **Authorisation resource.** The catalogue that defines what permissions and permission groups exist for each resource type — User, Role, Document, and so on. The platform ships with system-defined authorisation resources, and developers can also define their own. See [Authorisation Resources](authorisation/authorisation-resources.md).

## How the building blocks fit together

A user gets the access they need through:

- **Roles** assigned directly to the user.
- **User groups** they belong to (which carry their own roles or permission groups).

A user's effective access is the union of everything granted by their roles and their group memberships. Permissions are not assigned to a user directly — they're always granted through a role or a group. This keeps individual user records simple, and makes wide-scale access changes (e.g. "everyone in Support now also needs read access to Claims") quick and consistent.

## More in this chapter

- [Users](users.md) — create, find, and manage the accounts that can sign in.
- [Authentication](authentication/README.md) — how users and external systems prove who they are.
- [Authorisation](authorisation/README.md) — roles, user groups, and the catalogue of permissions.

## Related pages

- [Audit Trail](../todo-audit-trail.md) — see what users have done.
- [Security](../todo-security.md) — the platform's overall security model.
