.. _cdns-dg-RBAC:

=========================
Role-based access control
=========================

.. important::

   Role based access control does not apply during the EA release period.  This section
   is intended only for future releases.

Role-based access control (RBAC) restricts access to the capabilities of Rackspace Cloud 
services, including the |apiservice|, to authorized users only. RBAC enables Rackspace 
Cloud customers to specify which account users of their Cloud account have access to which 
|apiservice| service capabilities, based on roles defined by Rackspace (see |product name| 
Product Roles and Permissions). The permissions to perform certain operations in the 
|apiservice| – create, read, update, delete – are assigned to specific roles. The account 
owner user assigns these roles, either global (multiproduct) or product-specific (for 
example, Managed DNS), to account users.

..  note::
    
    RBAC setup is not required for participation in the EA phase.

Assigning roles to account users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The account owner (identity:user-admin) can create account users on the account and then 
assign roles to those users. The roles grant the account users specific permissions for 
accessing the capabilities of the |product name| service. Each account has only one account 
owner, and that role is assigned by default to any Rackspace Cloud account when the account 
is created.

See the *Cloud Identity Client Developer Guide* for information about how to perform the 
following tasks:

-  :rax-devdocs:`Add user <cloud-identity/v2/developer-guide/#add-user>` 
   
-  :rax-devdocs:`Add role to user <cloud-identity/v2/developer-guide/#add-role-to-user>`

-  :rax-devdocs:`Delete global role from user <cloud-identity/v2/developer-guide/#delete-global-role-from-user>`

.. note::

    The account owner (identity:user-admin) role cannot hold any additional roles because 
    it already has full access to all capabilities.

Roles available for |product name|
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Three roles (observer, creator, and admin) can be used to access the |apiservice| 
specifically. The following table describes these roles and their permissions.

**Managed DNS product roles and permissions**

+-----------------+-------------------------------------------------------------------+
| Role name       | Role permissions                                                  |
+=================+===================================================================+
| dnsaas:admin    | This role provides create, read, update, and delete permissions   |
|                 | in |product name|, where access is granted.                       |
+-----------------+-------------------------------------------------------------------+
| dnsaas:creator  | This role provides create, read and update permissions            |
|                 | in |product name|, where access is granted.                       |
+-----------------+-------------------------------------------------------------------+
| dnsaas:observer | This role provides read permission in |product name|, where       |
|                 | access is granted.                                                |
+-----------------+-------------------------------------------------------------------+

Additionally, two multiproduct roles apply to all products. Users with multiproduct roles 
inherit access to future products when those products become RBAC-enabled. The following 
table describes these roles and their permissions.

**Multiproduct (global) roles and permissions**

+-----------+-------------------------------------------------------------------+
| Role name | Role permissions                                                  |
+===========+===================================================================+
| admin     | This role provides create, read, update, and delete permissions   |
|           | in all products, where access is granted.                         |
+-----------+-------------------------------------------------------------------+
| observer  | This role provides read permission in all products, where         |
|           | access is granted.                                                |
+-----------+-------------------------------------------------------------------+

Resolving conflicts between roles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The account owner can set roles for both multiproduct and |product name| scope, and it is 
important to understand how any potential conflicts among these roles are resolved. 
When two roles appear to conflict, the role that provides the more extensive permissions 
takes precedence. Therefore, admin roles take precedence over observer and creator 
roles, because admin roles provide more permissions.

The following scenarios show examples of how potential conflicts between user roles 
in the Control Panel are resolved:

**Scenario 1**
^^^^^^^^^^^^^^^

The user is assigned the following roles: multiproduct *observer* and |product name| 
*admin*. In the Control Panel, it appears that the user has only the multiproduct *observer* 
role. The user can perform product *admin* functions in the Control Panel for |product name| 
only, and has the *observer* role for the rest of the products.

**Scenario 2**
^^^^^^^^^^^^^^^

The user is assigned the following roles: multiproduct *admin* and |product name| *observer*. 
In the Control Panel, it appears that the user has only the multiproduct *admin* role. The 
user can perform product *admin* functions in the Control Panel for all of the products, 
and the |product name| *observer* role is ignored.

RBAC permissions cross-reference to |apiservice| operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

API operations for |product name| may or may not be available to all roles. To see which 
operations are permitted to invoke which operations, see the 
:how-to:`Detailed Permissions Matrix for DNS <detailed-permissions-matrix-for-dns>` 
