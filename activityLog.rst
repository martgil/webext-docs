.. container:: sticky-sidebar

  ≡ activityLog API

  * `Events`_

  .. include:: /overlay/developer-resources.rst

===============
activityLog API
===============

.. role:: permission

.. role:: value

.. role:: code

Monitor extension activity

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`activityLog` is required to use ``messenger.activityLog.*``.

.. rst-class:: api-main-section

Events
======

.. _activityLog.onExtensionActivity:

onExtensionActivity
-------------------

.. api-section-annotation-hack:: 

Receives an activityItem for each logging event.

.. api-header::
   :label: Parameters for onExtensionActivity.addListener(listener, id)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``data``
         :type: (object)
         
         .. api-member::
            :name: [``args``]
            :type: (array of any, optional)
            
            A list of arguments passed to the call.
         
         
         .. api-member::
            :name: [``result``]
            :type: (object, optional)
            
            The result of the call.
         
         
         .. api-member::
            :name: [``tabId``]
            :type: (integer, optional)
            
            The tab associated with this event if it is a tab or content script.
         
         
         .. api-member::
            :name: [``url``]
            :type: (string, optional)
            
            If the type is content_script, this is the url of the script that was injected.
         
      
      
      .. api-member::
         :name: ``name``
         :type: (string)
         
         The name of the api call or event, or the script url if this is a content or user script event.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (`Date <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date>`__)
         
         The date string when this call is triggered.
      
      
      .. api-member::
         :name: ``type``
         :type: (`string`)
         
         The type of log entry.  api_call is a function call made by the extension and api_event is an event callback to the extension.  content_script is logged when a content script is injected.
         
         Supported values:
         
         .. api-member::
            :name: :value:`api_call`
         
         .. api-member::
            :name: :value:`api_event`
         
         .. api-member::
            :name: :value:`content_script`
         
         .. api-member::
            :name: :value:`user_script`
      
      
      .. api-member::
         :name: [``viewType``]
         :type: (`string`, optional)
         
         The type of view where the activity occurred.  Content scripts will not have a viewType.
         
         Supported values:
         
         .. api-member::
            :name: :value:`background`
         
         .. api-member::
            :name: :value:`popup`
         
         .. api-member::
            :name: :value:`sidebar`
         
         .. api-member::
            :name: :value:`tab`
         
         .. api-member::
            :name: :value:`devtools_page`
         
         .. api-member::
            :name: :value:`devtools_panel`
      
   

.. api-header::
   :label: Required permissions

   - :permission:`activityLog`
