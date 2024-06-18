.. container:: sticky-sidebar

  ≡ idle API

  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

========
idle API
========

.. role:: permission

.. role:: value

.. role:: code

Use the :code:`browser.idle` API to detect when the machine's idle state changes.

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`idle` is required to use ``messenger.idle.*``.

.. rst-class:: api-main-section

Functions
=========

.. _idle.queryState:

queryState(detectionIntervalInSeconds)
--------------------------------------

.. api-section-annotation-hack:: 

Returns "idle" if the user has not generated any input for a specified number of seconds, or "active" otherwise.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``detectionIntervalInSeconds``
      :type: (integer)
      
      The system is considered idle if detectionIntervalInSeconds seconds have elapsed since the last user input detected.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`idle.IdleState`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`idle`

.. _idle.setDetectionInterval:

setDetectionInterval(intervalInSeconds)
---------------------------------------

.. api-section-annotation-hack:: 

Sets the interval, in seconds, used to determine when the system is in an idle state for onStateChanged events. The default interval is 60 seconds.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``intervalInSeconds``
      :type: (integer)
      
      Threshold, in seconds, used to determine when the system is in an idle state.
   

.. api-header::
   :label: Required permissions

   - :permission:`idle`

.. rst-class:: api-main-section

Events
======

.. _idle.onStateChanged:

onStateChanged
--------------

.. api-section-annotation-hack:: 

Fired when the system changes to an active or idle state. The event fires with "idle" if the the user has not generated any input for a specified number of seconds, and "active" when the user generates input on an idle system.

.. api-header::
   :label: Parameters for onStateChanged.addListener(listener)

   
   .. api-member::
      :name: ``listener(newState)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``newState``
      :type: (:ref:`idle.IdleState`)
   

.. api-header::
   :label: Required permissions

   - :permission:`idle`

.. rst-class:: api-main-section

Types
=====

.. _idle.IdleState:

IdleState
---------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`active`
         
         .. api-member::
            :name: :value:`idle`
   
