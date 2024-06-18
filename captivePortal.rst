.. container:: sticky-sidebar

  ≡ captivePortal API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Properties`_

  .. include:: /overlay/developer-resources.rst

=================
captivePortal API
=================

.. role:: permission

.. role:: value

.. role:: code

This API provides the ability detect the captive portal state of the users connection.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`captivePortal`

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`captivePortal` is required to use ``messenger.captivePortal.*``.

.. rst-class:: api-main-section

Functions
=========

.. _captivePortal.getLastChecked:

getLastChecked()
----------------

.. api-section-annotation-hack:: 

Returns the time difference between NOW and the last time a request was completed in milliseconds.

.. api-header::
   :label: Required permissions

   - :permission:`captivePortal`

.. _captivePortal.getState:

getState()
----------

.. api-section-annotation-hack:: 

Returns the current portal state, one of :value:`unknown`, :value:`not_captive`, :value:`unlocked_portal`, :value:`locked_portal`.

.. api-header::
   :label: Required permissions

   - :permission:`captivePortal`

.. rst-class:: api-main-section

Events
======

.. _captivePortal.onConnectivityAvailable:

onConnectivityAvailable
-----------------------

.. api-section-annotation-hack:: 

This notification will be emitted when the captive portal service has determined that we can connect to the internet. The service will pass either :value:`captive` if there is an unlocked captive portal present, or :value:`clear` if no captive portal was detected.

.. api-header::
   :label: Parameters for onConnectivityAvailable.addListener(listener)

   
   .. api-member::
      :name: ``listener(status)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``status``
      :type: (`string`)
      
      Supported values:
      
      .. api-member::
         :name: :value:`captive`
      
      .. api-member::
         :name: :value:`clear`
   

.. api-header::
   :label: Required permissions

   - :permission:`captivePortal`

.. _captivePortal.onStateChanged:

onStateChanged
--------------

.. api-section-annotation-hack:: 

Fired when the captive portal state changes.

.. api-header::
   :label: Parameters for onStateChanged.addListener(listener)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``state``
         :type: (`string`)
         
         The current captive portal state.
         
         Supported values:
         
         .. api-member::
            :name: :value:`unknown`
         
         .. api-member::
            :name: :value:`not_captive`
         
         .. api-member::
            :name: :value:`unlocked_portal`
         
         .. api-member::
            :name: :value:`locked_portal`
      
   

.. api-header::
   :label: Required permissions

   - :permission:`captivePortal`

.. rst-class:: api-main-section

Properties
==========

.. _captivePortal.canonicalURL:

canonicalURL
------------

.. api-section-annotation-hack:: 

Return the canonical captive-portal detection URL. Read-only.
