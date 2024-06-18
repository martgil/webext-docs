.. container:: sticky-sidebar

  ≡ addressBooks.contacts API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

=========================
addressBooks.contacts API
=========================

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`addressBooks`

   Read and modify your address books and contacts

.. api-member::
   :name: :permission:`sensitiveDataUpload`

   Transfer sensitive user data (if access has been granted) to a remote server for further processing

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`addressBooks` is required to use ``messenger.addressBooks.contacts.*``.

.. rst-class:: api-main-section

Functions
=========

.. _addressBooks.contacts.create:

create(parentId, vCard)
-----------------------

.. api-section-annotation-hack:: 

Adds a new contact to the address book with the id :value:`parentId`.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``parentId``
      :type: (string)
   
   
   .. api-member::
      :name: ``vCard``
      :type: (string)
      
      The vCard for the new contact. If it includes an (optional) id and an existing contact has this id already, an exception is thrown.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: string
      
      The ID of the new contact.
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.delete:

delete(id)
----------

.. api-section-annotation-hack:: 

Removes a contact from the address book. The contact is also removed from any mailing lists it is a member of.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.get:

get(id)
-------

.. api-section-annotation-hack:: 

Gets a single contact.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`addressBooks.contacts.ContactNode`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.getPhoto:

getPhoto(id)
------------

.. api-section-annotation-hack:: 

Gets the photo associated with this contact. Returns :value:`null`, if no photo is available.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: `File <https://developer.mozilla.org/en-US/docs/Web/API/File>`__ or null
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.list:

list(parentId)
--------------

.. api-section-annotation-hack:: 

Gets all the contacts in the address book with the id :value:`parentId`.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``parentId``
      :type: (string)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`addressBooks.contacts.ContactNode`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.query:

query(queryInfo)
----------------

.. api-section-annotation-hack:: 

Gets all contacts matching :value:`queryInfo`.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``queryInfo``
      :type: (:ref:`addressBooks.contacts.QueryInfo`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`addressBooks.contacts.ContactNode`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.setPhoto:

setPhoto(id, file)
------------------

.. api-section-annotation-hack:: 

Sets the photo associated with this contact.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   
   
   .. api-member::
      :name: ``file``
      :type: (`File <https://developer.mozilla.org/en-US/docs/Web/API/File>`__)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.update:

update(id, vCard)
-----------------

.. api-section-annotation-hack:: 

Updates a contact.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   
   
   .. api-member::
      :name: ``vCard``
      :type: (string)
      
      The updated vCard for the contact.
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. rst-class:: api-main-section

Events
======

.. _addressBooks.contacts.onCreated:

onCreated
---------

.. api-section-annotation-hack:: 

Fired when a contact is created.

.. api-header::
   :label: Parameters for onCreated.addListener(listener)

   
   .. api-member::
      :name: ``listener(node)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``node``
      :type: (:ref:`addressBooks.contacts.ContactNode`)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.onDeleted:

onDeleted
---------

.. api-section-annotation-hack:: 

Fired when a contact is removed from an address book.

.. api-header::
   :label: Parameters for onDeleted.addListener(listener)

   
   .. api-member::
      :name: ``listener(parentId, id)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``parentId``
      :type: (string)
   
   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.contacts.onUpdated:

onUpdated
---------

.. api-section-annotation-hack:: 

Fired when a contact is changed.

.. api-header::
   :label: Parameters for onUpdated.addListener(listener)

   
   .. api-member::
      :name: ``listener(node, oldVCard)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``node``
      :type: (:ref:`addressBooks.contacts.ContactNode`)
   
   
   .. api-member::
      :name: ``oldVCard``
      :type: (string)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. rst-class:: api-main-section

Types
=====

.. _addressBooks.contacts.ContactNode:

ContactNode
-----------

.. api-section-annotation-hack:: 

A node representing a contact in an address book.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``id``
      :type: (string)
      
      The unique identifier for the node. IDs are unique within the current profile, and they remain valid even after the program is restarted.
   
   
   .. api-member::
      :name: ``type``
      :type: (:ref:`addressBooks.NodeType`)
      
      Always set to :value:`contact`.
   
   
   .. api-member::
      :name: ``vCard``
      :type: (string)
   
   
   .. api-member::
      :name: [``parentId``]
      :type: (string, optional)
      
      The :value:`id` of the parent object.
   
   
   .. api-member::
      :name: [``readOnly``]
      :type: (boolean, optional)
      
      Indicates if the object is read-only.
   
   
   .. api-member::
      :name: [``remote``]
      :type: (boolean, optional)
      
      Indicates if the object came from a remote address book.
   

.. _addressBooks.contacts.ContactProperties:

ContactProperties
-----------------

.. api-section-annotation-hack:: 

A set of individual properties for a particular contact, and its vCard string. Further information can be found in $(doc:examples/vcard).

.. api-header::
   :label: object

.. _addressBooks.contacts.PropertyChange:

PropertyChange
--------------

.. api-section-annotation-hack:: 

A dictionary of changed properties. Keys are the property name that changed, values are an object containing :value:`oldValue` and :value:`newValue`. Values can be either a string or :value:`null`.

.. api-header::
   :label: object

.. _addressBooks.contacts.QueryInfo:

QueryInfo
---------

.. api-section-annotation-hack:: 

Object defining a query for $(ref:contacts.quickSearch).

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``includeLocal``]
      :type: (boolean, optional)
      
      Whether to include results from local address books. Defaults to :value:`true`.
   
   
   .. api-member::
      :name: [``includeReadOnly``]
      :type: (boolean, optional)
      
      Whether to include results from read-only address books. Defaults to :value:`true`.
   
   
   .. api-member::
      :name: [``includeReadWrite``]
      :type: (boolean, optional)
      
      Whether to include results from read-write address books. Defaults to :value:`true`.
   
   
   .. api-member::
      :name: [``includeRemote``]
      :type: (boolean, optional)
      
      Whether to include results from remote address books. Defaults to :value:`true`.
   
   
   .. api-member::
      :name: [``parentId``]
      :type: (string, optional)
      
      The id of the address book to search. If not specified, all address books are searched.
   
   
   .. api-member::
      :name: [``searchString``]
      :type: (string, optional)
      
      One or more space-separated terms to search for in predefined contact fields (defined by the preference :value:`mail.addr_book.quicksearchquery.format`).
   
