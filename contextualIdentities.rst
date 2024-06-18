.. container:: sticky-sidebar

  ≡ contextualIdentities API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

========================
contextualIdentities API
========================

.. role:: permission

.. role:: value

.. role:: code

Use the :code:`browser.contextualIdentities` API to query and modify contextual identity, also called as containers.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`contextualIdentities`

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`contextualIdentities` is required to use ``messenger.contextualIdentities.*``.

.. rst-class:: api-main-section

Functions
=========

.. _contextualIdentities.create:

create(details)
---------------

.. api-section-annotation-hack:: 

Creates a contextual identity with the given data.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      Details about the contextual identity being created.
      
      .. api-member::
         :name: ``color``
         :type: (string)
         
         The color of the contextual identity.
      
      
      .. api-member::
         :name: ``icon``
         :type: (string)
         
         The icon of the contextual identity.
      
      
      .. api-member::
         :name: ``name``
         :type: (string)
         
         The name of the contextual identity.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.get:

get(cookieStoreId)
------------------

.. api-section-annotation-hack:: 

Retrieves information about a single contextual identity.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``cookieStoreId``
      :type: (string)
      
      The ID of the contextual identity cookie store. 
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.move:

move(cookieStoreIds, position)
------------------------------

.. api-section-annotation-hack:: 

Reorder one or more contextual identities by their cookieStoreIDs to a given position.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``cookieStoreIds``
      :type: (string or array of string)
      
      The ID or list of IDs of the contextual identity cookie stores. 
   
   
   .. api-member::
      :name: ``position``
      :type: (integer)
      
      The position the contextual identity should move to.
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.query:

query(details)
--------------

.. api-section-annotation-hack:: 

Retrieves all contextual identities

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      Information to filter the contextual identities being retrieved.
      
      .. api-member::
         :name: [``name``]
         :type: (string, optional)
         
         Filters the contextual identity by name.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.remove:

remove(cookieStoreId)
---------------------

.. api-section-annotation-hack:: 

Deletes a contextual identity by its cookie Store ID.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``cookieStoreId``
      :type: (string)
      
      The ID of the contextual identity cookie store. 
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.update:

update(cookieStoreId, details)
------------------------------

.. api-section-annotation-hack:: 

Updates a contextual identity with the given data.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``cookieStoreId``
      :type: (string)
      
      The ID of the contextual identity cookie store. 
   
   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      Details about the contextual identity being created.
      
      .. api-member::
         :name: [``color``]
         :type: (string, optional)
         
         The color of the contextual identity.
      
      
      .. api-member::
         :name: [``icon``]
         :type: (string, optional)
         
         The icon of the contextual identity.
      
      
      .. api-member::
         :name: [``name``]
         :type: (string, optional)
         
         The name of the contextual identity.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. rst-class:: api-main-section

Events
======

.. _contextualIdentities.onCreated:

onCreated
---------

.. api-section-annotation-hack:: 

Fired when a new container is created.

.. api-header::
   :label: Parameters for onCreated.addListener(listener)

   
   .. api-member::
      :name: ``listener(changeInfo)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``changeInfo``
      :type: (object)
      
      .. api-member::
         :name: ``contextualIdentity``
         :type: (:ref:`contextualIdentities.ContextualIdentity`)
         
         Contextual identity that has been created
      
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.onRemoved:

onRemoved
---------

.. api-section-annotation-hack:: 

Fired when a container is removed.

.. api-header::
   :label: Parameters for onRemoved.addListener(listener)

   
   .. api-member::
      :name: ``listener(changeInfo)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``changeInfo``
      :type: (object)
      
      .. api-member::
         :name: ``contextualIdentity``
         :type: (:ref:`contextualIdentities.ContextualIdentity`)
         
         Contextual identity that has been removed
      
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. _contextualIdentities.onUpdated:

onUpdated
---------

.. api-section-annotation-hack:: 

Fired when a container is updated.

.. api-header::
   :label: Parameters for onUpdated.addListener(listener)

   
   .. api-member::
      :name: ``listener(changeInfo)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``changeInfo``
      :type: (object)
      
      .. api-member::
         :name: ``contextualIdentity``
         :type: (:ref:`contextualIdentities.ContextualIdentity`)
         
         Contextual identity that has been updated
      
   

.. api-header::
   :label: Required permissions

   - :permission:`contextualIdentities`

.. rst-class:: api-main-section

Types
=====

.. _contextualIdentities.ContextualIdentity:

ContextualIdentity
------------------

.. api-section-annotation-hack:: 

Represents information about a contextual identity.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``color``
      :type: (string)
      
      The color name of the contextual identity.
   
   
   .. api-member::
      :name: ``colorCode``
      :type: (string)
      
      The color hash of the contextual identity.
   
   
   .. api-member::
      :name: ``cookieStoreId``
      :type: (string)
      
      The cookie store ID of the contextual identity.
   
   
   .. api-member::
      :name: ``icon``
      :type: (string)
      
      The icon name of the contextual identity.
   
   
   .. api-member::
      :name: ``iconUrl``
      :type: (string)
      
      The icon url of the contextual identity.
   
   
   .. api-member::
      :name: ``name``
      :type: (string)
      
      The name of the contextual identity.
   
