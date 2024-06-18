.. container:: sticky-sidebar

  ≡ webNavigation API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

=================
webNavigation API
=================

.. role:: permission

.. role:: value

.. role:: code

Use the :code:`browser.webNavigation` API to receive notifications about the status of navigation requests in-flight.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`webNavigation`

   Access browser activity during navigation

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`webNavigation` is required to use ``messenger.webNavigation.*``.

.. rst-class:: api-main-section

Functions
=========

.. _webNavigation.getAllFrames:

getAllFrames(details)
---------------------

.. api-section-annotation-hack:: 

Retrieves information about all frames of a given tab.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      Information about the tab to retrieve all frames from.
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab.
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of object
      
      A list of frames in the given tab, null if the specified tab ID is invalid.
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.getFrame:

getFrame(details)
-----------------

.. api-section-annotation-hack:: 

Retrieves information about the given frame. A frame refers to an &lt;iframe&gt; or a &lt;frame&gt; of a web page and is identified by a tab ID and a frame ID.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      Information about the frame to retrieve information about.
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         The ID of the frame in the given tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the frame is.
      
      
      .. api-member::
         :name: [``processId``]
         :type: (integer, optional)
         
         The ID of the process runs the renderer for this tab.
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: object
      
      Information about the requested frame, null if the specified frame ID and/or tab ID are invalid.
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         The ID of the frame. 0 indicates that this is the main frame; a positive value indicates the ID of a subframe.
      
      
      .. api-member::
         :name: ``parentFrameId``
         :type: (integer)
         
         ID of frame that wraps the frame. Set to -1 of no parent frame exists.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the frame is.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
         
         The URL currently associated with this frame, if the frame identified by the frameId existed at one point in the given tab. The fact that an URL is associated with a given frameId does not imply that the corresponding frame still exists.
      
      
      .. api-member::
         :name: [``errorOccurred``]
         :type: (boolean, optional)
         
         True if the last navigation in this frame was interrupted by an error, i.e. the onErrorOccurred event fired.
      
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. rst-class:: api-main-section

Events
======

.. _webNavigation.onBeforeNavigate:

onBeforeNavigate
----------------

.. api-section-annotation-hack:: 

Fired when a navigation is about to occur.

.. api-header::
   :label: Parameters for onBeforeNavigate.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique for a given tab and process.
      
      
      .. api-member::
         :name: ``parentFrameId``
         :type: (integer)
         
         ID of frame that wraps the frame. Set to -1 of no parent frame exists.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation is about to occur.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the browser was about to start the navigation, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onCommitted:

onCommitted
-----------

.. api-section-annotation-hack:: 

Fired when a navigation is committed. The document (and the resources it refers to, such as images and subframes) might still be downloading, but at least part of the document has been received from the server and the browser has decided to switch to the new document.

.. api-header::
   :label: Parameters for onCommitted.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation occurs.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the navigation was committed, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``transitionQualifiers``
         :type: (array of :ref:`webNavigation.TransitionQualifier`)
         
         A list of transition qualifiers.
      
      
      .. api-member::
         :name: ``transitionType``
         :type: (:ref:`webNavigation.TransitionType`)
         
         Cause of the navigation.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onCompleted:

onCompleted
-----------

.. api-section-annotation-hack:: 

Fired when a document, including the resources it refers to, is completely loaded and initialized.

.. api-header::
   :label: Parameters for onCompleted.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation occurs.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the document finished loading, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onCreatedNavigationTarget:

onCreatedNavigationTarget
-------------------------

.. api-section-annotation-hack:: 

Fired when a new window, or a new tab in an existing window, is created to host a navigation.

.. api-header::
   :label: Parameters for onCreatedNavigationTarget.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``sourceFrameId``
         :type: (integer)
         
         The ID of the frame with sourceTabId in which the navigation is triggered. 0 indicates the main frame.
      
      
      .. api-member::
         :name: ``sourceProcessId``
         :type: (integer)
         
         The ID of the process runs the renderer for the source tab.
      
      
      .. api-member::
         :name: ``sourceTabId``
         :type: (integer)
         
         The ID of the tab in which the navigation is triggered.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the url is opened
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the browser was about to create a new view, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
         
         The URL to be opened in the new window.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onDOMContentLoaded:

onDOMContentLoaded
------------------

.. api-section-annotation-hack:: 

Fired when the page's DOM is fully constructed, but the referenced resources may not finish loading.

.. api-header::
   :label: Parameters for onDOMContentLoaded.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation occurs.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the page's DOM was fully constructed, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onErrorOccurred:

onErrorOccurred
---------------

.. api-section-annotation-hack:: 

Fired when an error occurs and the navigation is aborted. This can happen if either a network error occurred, or the user aborted the navigation.

.. api-header::
   :label: Parameters for onErrorOccurred.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``error``
         :type: (string) **Unsupported.**
         
         The error description.
      
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation occurs.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the error occurred, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onHistoryStateUpdated:

onHistoryStateUpdated
---------------------

.. api-section-annotation-hack:: 

Fired when the frame's history was updated to a new URL. All future events for that frame will use the updated URL.

.. api-header::
   :label: Parameters for onHistoryStateUpdated.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation occurs.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the navigation was committed, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``transitionQualifiers``
         :type: (array of :ref:`webNavigation.TransitionQualifier`)
         
         A list of transition qualifiers.
      
      
      .. api-member::
         :name: ``transitionType``
         :type: (:ref:`webNavigation.TransitionType`)
         
         Cause of the navigation.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onReferenceFragmentUpdated:

onReferenceFragmentUpdated
--------------------------

.. api-section-annotation-hack:: 

Fired when the reference fragment of a frame was updated. All future events for that frame will use the updated URL.

.. api-header::
   :label: Parameters for onReferenceFragmentUpdated.addListener(listener, filters)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``filters``]
      :type: (:ref:`webNavigation.EventUrlFilters`, optional)
      
      Conditions that the URL being navigated to must satisfy. The 'schemes' and 'ports' fields of UrlFilter are ignored for this event.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``processId``
         :type: (integer) **Unsupported.**
         
         The ID of the process runs the renderer for this tab.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the navigation occurs.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the navigation was committed, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``transitionQualifiers``
         :type: (array of :ref:`webNavigation.TransitionQualifier`)
         
         A list of transition qualifiers.
      
      
      .. api-member::
         :name: ``transitionType``
         :type: (:ref:`webNavigation.TransitionType`)
         
         Cause of the navigation.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. _webNavigation.onTabReplaced:

onTabReplaced
-------------

.. api-section-annotation-hack:: 

Fired when the contents of the tab is replaced by a different (usually previously pre-rendered) tab.

.. api-header::
   :label: Parameters for onTabReplaced.addListener(listener)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``replacedTabId``
         :type: (integer)
         
         The ID of the tab that was replaced.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab that replaced the old tab.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when the replacement happened, in milliseconds since the epoch.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`webNavigation`

.. rst-class:: api-main-section

Types
=====

.. _webNavigation.EventUrlFilters:

EventUrlFilters
---------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``url``
      :type: (array of :ref:`events.UrlFilter`)
   

.. _webNavigation.TransitionQualifier:

TransitionQualifier
-------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`client_redirect`
         
         .. api-member::
            :name: :value:`server_redirect`
         
         .. api-member::
            :name: :value:`forward_back`
         
         .. api-member::
            :name: :value:`from_address_bar`
   

.. _webNavigation.TransitionType:

TransitionType
--------------

.. api-section-annotation-hack:: 

Cause of the navigation. The same transition types as defined in the history API are used. These are the same transition types as defined in the $(topic:transition_types)[history API] except with :code:`"start_page"` in place of :code:`"auto_toplevel"` (for backwards compatibility).

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`link`
         
         .. api-member::
            :name: :value:`typed`
         
         .. api-member::
            :name: :value:`auto_bookmark`
         
         .. api-member::
            :name: :value:`auto_subframe`
         
         .. api-member::
            :name: :value:`manual_subframe`
         
         .. api-member::
            :name: :value:`generated`
         
         .. api-member::
            :name: :value:`start_page`
         
         .. api-member::
            :name: :value:`form_submit`
         
         .. api-member::
            :name: :value:`reload`
         
         .. api-member::
            :name: :value:`keyword`
         
         .. api-member::
            :name: :value:`keyword_generated`
   
