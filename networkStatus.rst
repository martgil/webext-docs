.. container:: sticky-sidebar

  ≡ networkStatus API

  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

=================
networkStatus API
=================

.. role:: permission

.. role:: value

.. role:: code

This API provides the ability to determine the status of and detect changes in the network connection. This API can only be used in privileged extensions.

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`networkStatus` is required to use ``messenger.networkStatus.*``.

.. rst-class:: api-main-section

Functions
=========

.. _networkStatus.getLinkInfo:

getLinkInfo()
-------------

.. api-section-annotation-hack:: 

Returns the :ref:`NetworkLinkInfo` of the current network connection.

.. api-header::
   :label: Required permissions

   - :permission:`networkStatus`

.. rst-class:: api-main-section

Events
======

.. _networkStatus.onConnectionChanged:

onConnectionChanged
-------------------

.. api-section-annotation-hack:: 

Fired when the network connection state changes.

.. api-header::
   :label: Parameters for onConnectionChanged.addListener(listener)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (:ref:`networkStatus.NetworkLinkInfo`)
   

.. api-header::
   :label: Required permissions

   - :permission:`networkStatus`

.. rst-class:: api-main-section

Types
=====

.. _networkStatus.NetworkLinkInfo:

NetworkLinkInfo
---------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``status``
      :type: (`string`)
      
      Status of the network link, if "unknown" then link is usually assumed to be "up"
      
      Supported values:
      
      .. api-member::
         :name: :value:`unknown`
      
      .. api-member::
         :name: :value:`up`
      
      .. api-member::
         :name: :value:`down`
   
   
   .. api-member::
      :name: ``type``
      :type: (`string`)
      
      If known, the type of network connection that is avialable.
      
      Supported values:
      
      .. api-member::
         :name: :value:`unknown`
      
      .. api-member::
         :name: :value:`ethernet`
      
      .. api-member::
         :name: :value:`usb`
      
      .. api-member::
         :name: :value:`wifi`
      
      .. api-member::
         :name: :value:`wimax`
      
      .. api-member::
         :name: :value:`mobile`
   
   
   .. api-member::
      :name: [``id``]
      :type: (string, optional)
      
      If known, the network id or name.
   
