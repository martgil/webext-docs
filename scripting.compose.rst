.. container:: sticky-sidebar

  ≡ scripting.compose API

  * `Permissions`_
  * `Functions`_
  * `Types`_
  * `External Types`_

  .. include:: /overlay/developer-resources.rst

=====================
scripting.compose API
=====================

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`sensitiveDataUpload`

   Transfer sensitive user data (if access has been granted) to a remote server for further processing

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`compose` is required to use ``messenger.scripting.compose.*``.

.. rst-class:: api-main-section

Functions
=========

.. _scripting.compose.getRegisteredScripts:

getRegisteredScripts([filter])
------------------------------

.. api-section-annotation-hack:: 

Returns all registered compose scripts for this extension that match the given filter.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``filter``]
      :type: (:ref:`scripting.compose.ComposeScriptFilter`, optional)
      
      An object to filter the extension's registered compose scripts.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`scripting.compose.ComposeScriptDetails`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`compose`

.. _scripting.compose.registerScripts:

registerScripts(scripts)
------------------------

.. api-section-annotation-hack:: 

Registers one or more compose scripts for this extension, which should be injected into the message compose editor. **Note:** Registered scripts will only be applied to newly opened message compose tabs. To apply the script to already open message compose tabs, manually inject your script by calling :ref:`scripting.executeScript` for each of the open :value:`messageCompose` tabs.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``scripts``
      :type: (array of :ref:`scripting.compose.ComposeScriptDetails`)
      
      Contains a list of compose scripts to be registered. If there are errors during script parsing/file validation, or if the IDs specified already exist, then no scripts are registered.
   

.. api-header::
   :label: Required permissions

   - :permission:`compose`

.. _scripting.compose.unregisterScripts:

unregisterScripts([filter])
---------------------------

.. api-section-annotation-hack:: 

Unregisters one or more compose scripts for this extension.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``filter``]
      :type: (:ref:`scripting.compose.ComposeScriptFilter`, optional)
      
      If specified, only unregisters compose scripts which match the filter. Otherwise, all of the extension's compose scripts are unregistered.
   

.. api-header::
   :label: Required permissions

   - :permission:`compose`

.. rst-class:: api-main-section

Types
=====

.. _scripting.compose.ComposeScriptDetails:

ComposeScriptDetails
--------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``id``
      :type: (string)
      
      The id of the compose script, specified in the API call.
   
   
   .. api-member::
      :name: [``css``]
      :type: (array of :ref:`scripting.compose.ExtensionURL`, optional)
      
      The list of CSS files to be injected. These are injected in the order they appear in this array.
   
   
   .. api-member::
      :name: [``js``]
      :type: (array of :ref:`scripting.compose.ExtensionURL`, optional)
      
      The list of JavaScript files to be injected. These are injected in the order they appear in this array.
   
   
   .. api-member::
      :name: [``runAt``]
      :type: (`RunAt <https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extensionTypes/RunAt>`__, optional)
      
      Specifies when JavaScript files are injected. The preferred and default value is :code:`document_idle`.
   

.. _scripting.compose.ComposeScriptFilter:

ComposeScriptFilter
-------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``ids``]
      :type: (array of string, optional)
      
      The IDs of specific compose scripts to retrieve with :code:`getRegisteredScripts()` or to unregister with :code:`unregisterScripts()`.
   

.. rst-class:: api-main-section

External Types
==============

The following types are not defined by this API, but by the underlying Mozilla WebExtension code base. They are included here, because there is no other public documentation available.

.. _scripting.compose.ExtensionURL:

ExtensionURL
------------

.. api-section-annotation-hack:: 

A path relative to the root of the extension.

.. api-header::
   :label: string
