Class **Phalcon_Acl_Adapter_Memory**
====================================

Manages ACL lists in memory

Methods
---------

**setDefaultAction** (int $defaultAccess)

Sets the default access level (Phalcon_Acl::ALLOW or Phalcon_Acl::DENY)

**getDefaultAction** ()

Returns the default ACL access level

**boolean** **addRole** (string $roleObject, array $accessInherits)

Adds a role to the ACL list. Second parameter lets to inherit access data from other existing role  Example:  

.. code-block:: php

    <?php $acl->addRole('administrator', 'consultor');



  

.. code-block:: php

    <?php $acl->addRole('administrator', 'consultor');





**addInherit** (string $roleName, string $roleToInherit)

Do a role inherit from another existing role

**boolean** **isRole** (string $roleName)

Check whether role exist in the roles list

**boolean** **isResource** (string $resourceName)

Check whether resource exist in the resources list

**boolean** **addResource** (Phalcon_Acl_Resource $resource, unknown $accessList)

Adds a resource to the ACL list  Access names can be a particular action, by example  search, update, delete, etc or a list of them  Example:  

.. code-block:: php

    <?php

    
    //Add a resource to the the list allowing access to an action
     $acl->addResource(new Phalcon_Acl_Resource('customers'), 'search');
     $acl->addResource('customers', 'search');
    //Add a resource  with an access list
     $acl->addResource(new Phalcon_Acl_Resource('customers'), array('create', 'search'));
     $acl->addResource('customers', array('create', 'search'));
     





**addResourceAccess** (string $resourceName, mixed $accessList)

Adds access to resources

**dropResourceAccess** (string $resourceName, mixed $accessList)

Removes an access from a resource

**_allowOrDeny** (unknown $roleName, unknown $resourceName, unknown $access, unknown $action)



**allow** (string $roleName, string $resourceName, mixed $access)

Allow access to a role on a resource  You can use '*' as wildcard  Ej:  

.. code-block:: php

    <?php

    
    //Allow access to guests to search on customers
     $acl->allow('guests', 'customers', 'search');
    //Allow access to guests to search or create on customers
     $acl->allow('guests', 'customers', array('search', 'create'));
    //Allow access to any role to browse on products
     $acl->allow('*', 'products', 'browse');
    //Allow access to any role to browse on any resource
     $acl->allow('*', '*', 'browse');
     





**boolean** **deny** (string $roleName, string $resourceName, mixed $access)

Deny access to a role on a resource  You can use '*' as wildcard  Ej:  

.. code-block:: php

    <?php

    
    //Deny access to guests to search on customers
     $acl->deny('guests', 'customers', 'search');
    //Deny access to guests to search or create on customers
     $acl->deny('guests', 'customers', array('search', 'create'));
    //Deny access to any role to browse on products
     $acl->deny('*', 'products', 'browse');
    //Deny access to any role to browse on any resource
     $acl->deny('*', '*', 'browse');
     





**boolean** **isAllowed** (string $role, string $resource, unknown $access)

Check whether a role is allowed to access an action from a resource  

.. code-block:: php

    <?php

    
    //Does andres have access to the customers resource to create?
     $acl->isAllowed('andres', 'Products', 'create');
    //Do guests have access to any resource to edit?
     $acl->isAllowed('guests', '*', 'edit');
     





**_rebuildAccessList** ()

Rebuild the list of access from the inherit lists

