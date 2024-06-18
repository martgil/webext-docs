.. container:: sticky-sidebar

  ≡ alarms API

  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

==========
alarms API
==========

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`alarms` is required to use ``messenger.alarms.*``.

.. rst-class:: api-main-section

Functions
=========

.. _alarms.clear:

clear([name])
-------------

.. api-section-annotation-hack:: 

Clears the alarm with the given name.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``name``]
      :type: (string, optional)
      
      The name of the alarm to clear. Defaults to the empty string.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: boolean
      
      Whether an alarm of the given name was found to clear.
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`alarms`

.. _alarms.clearAll:

clearAll()
----------

.. api-section-annotation-hack:: 

Clears all alarms.

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: boolean
      
      Whether any alarm was found to clear.
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`alarms`

.. _alarms.create:

create([name], alarmInfo)
-------------------------

.. api-section-annotation-hack:: 

Creates an alarm. After the delay is expired, the onAlarm event is fired. If there is another alarm with the same name (or no name if none is specified), it will be cancelled and replaced by this alarm.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``name``]
      :type: (string, optional)
      
      Optional name to identify this alarm. Defaults to the empty string.
   
   
   .. api-member::
      :name: ``alarmInfo``
      :type: (object)
      
      Details about the alarm. The alarm first fires either at 'when' milliseconds past the epoch (if 'when' is provided), after 'delayInMinutes' minutes from the current time (if 'delayInMinutes' is provided instead), or after 'periodInMinutes' minutes from the current time (if only 'periodInMinutes' is provided). Users should never provide both 'when' and 'delayInMinutes'. If 'periodInMinutes' is provided, then the alarm recurs repeatedly after that many minutes.
      
      .. api-member::
         :name: [``delayInMinutes``]
         :type: (number, optional)
         
         Number of minutes from the current time after which the alarm should first fire.
      
      
      .. api-member::
         :name: [``periodInMinutes``]
         :type: (number, optional)
         
         Number of minutes after which the alarm should recur repeatedly.
      
      
      .. api-member::
         :name: [``when``]
         :type: (number, optional)
         
         Time when the alarm is scheduled to first fire, in milliseconds past the epoch.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`alarms`

.. _alarms.get:

get([name])
-----------

.. api-section-annotation-hack:: 

Retrieves details about the specified alarm.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``name``]
      :type: (string, optional)
      
      The name of the alarm to get. Defaults to the empty string.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`alarms.Alarm`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`alarms`

.. _alarms.getAll:

getAll()
--------

.. api-section-annotation-hack:: 

Gets an array of all the alarms.

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`alarms.Alarm`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`alarms`

.. rst-class:: api-main-section

Events
======

.. _alarms.onAlarm:

onAlarm
-------

.. api-section-annotation-hack:: 

Fired when an alarm has expired. Useful for transient background pages.

.. api-header::
   :label: Parameters for onAlarm.addListener(listener)

   
   .. api-member::
      :name: ``listener(name)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``name``
      :type: (:ref:`alarms.Alarm`)
      
      The alarm that has expired.
   

.. api-header::
   :label: Required permissions

   - :permission:`alarms`

.. rst-class:: api-main-section

Types
=====

.. _alarms.Alarm:

Alarm
-----

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``name``
      :type: (string)
      
      Name of this alarm.
   
   
   .. api-member::
      :name: ``scheduledTime``
      :type: (number)
      
      Time when the alarm is scheduled to fire, in milliseconds past the epoch.
   
   
   .. api-member::
      :name: [``periodInMinutes``]
      :type: (number, optional)
      
      When present, signals that the alarm triggers periodically after so many minutes.
   
