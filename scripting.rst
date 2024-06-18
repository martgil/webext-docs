.. container:: sticky-sidebar

  ≡ scripting API

  * `Permissions`_
  * `Functions`_
  * `Types`_
  * `External Types`_

  .. include:: /overlay/developer-resources.rst

=============
scripting API
=============

.. role:: permission

.. role:: value

.. role:: code

Use the scripting API to execute script in different contexts.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`scripting`

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`scripting` is required to use ``messenger.scripting.*``.

.. rst-class:: api-main-section

Functions
=========

.. _scripting.executeScript:

executeScript(injection)
------------------------

.. api-section-annotation-hack:: 

Injects a script into a target context. The script will be run at :code:`document_idle`.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``injection``
      :type: (:ref:`scripting.ScriptInjection`)
      
      The details of the script which to inject.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`scripting.InjectionResult`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. _scripting.getRegisteredContentScripts:

getRegisteredContentScripts([filter])
-------------------------------------

.. api-section-annotation-hack:: 

Returns all dynamically registered content scripts for this extension that match the given filter.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``filter``]
      :type: (:ref:`scripting.ContentScriptFilter`, optional)
      
      An object to filter the extension's dynamically registered scripts.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`scripting.RegisteredContentScript`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. _scripting.insertCSS:

insertCSS(injection)
--------------------

.. api-section-annotation-hack:: 

Inserts a CSS stylesheet into a target context. If multiple frames are specified, unsuccessful injections are ignored.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``injection``
      :type: (:ref:`scripting.CSSInjection`)
      
      The details of the styles to insert.
   

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. _scripting.registerContentScripts:

registerContentScripts(scripts)
-------------------------------

.. api-section-annotation-hack:: 

Registers one or more content scripts for this extension.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``scripts``
      :type: (array of :ref:`scripting.RegisteredContentScript`)
      
      Contains a list of scripts to be registered. If there are errors during script parsing/file validation, or if the IDs specified already exist, then no scripts are registered.
   

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. _scripting.removeCSS:

removeCSS(injection)
--------------------

.. api-section-annotation-hack:: 

Removes a CSS stylesheet that was previously inserted by this extension from a target context.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``injection``
      :type: (:ref:`scripting.CSSInjection`)
      
      The details of the styles to remove. Note that the :code:`css`, :code:`files`, and :code:`origin` properties must exactly match the stylesheet inserted through :code:`insertCSS`. Attempting to remove a non-existent stylesheet is a no-op.
   

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. _scripting.unregisterContentScripts:

unregisterContentScripts([filter])
----------------------------------

.. api-section-annotation-hack:: 

Unregisters one or more content scripts for this extension.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``filter``]
      :type: (:ref:`scripting.ContentScriptFilter`, optional)
      
      If specified, only unregisters dynamic content scripts which match the filter. Otherwise, all of the extension's dynamic content scripts are unregistered.
   

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. _scripting.updateContentScripts:

updateContentScripts(scripts)
-----------------------------

.. api-section-annotation-hack:: 

Updates one or more content scripts for this extension.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``scripts``
      :type: (array of object)
      
      Contains a list of scripts to be updated. If there are errors during script parsing/file validation, or if the IDs specified do not already exist, then no scripts are updated.
   

.. api-header::
   :label: Required permissions

   - :permission:`scripting`

.. rst-class:: api-main-section

Types
=====

.. _scripting.CSSInjection:

CSSInjection
------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``target``
      :type: (:ref:`scripting.InjectionTarget`)
      
      Details specifying the target into which to inject the CSS.
   
   
   .. api-member::
      :name: [``css``]
      :type: (string, optional)
      
      A string containing the CSS to inject. Exactly one of :code:`files` and :code:`css` must be specified.
   
   
   .. api-member::
      :name: [``files``]
      :type: (array of string, optional)
      
      The path of the CSS files to inject, relative to the extension's root directory. Exactly one of :code:`files` and :code:`css` must be specified.
   
   
   .. api-member::
      :name: [``origin``]
      :type: (`string`, optional)
      
      The style origin for the injection. Defaults to :code:`'AUTHOR'`.
      
      Supported values:
      
      .. api-member::
         :name: :value:`USER`
      
      .. api-member::
         :name: :value:`AUTHOR`
   

.. _scripting.ContentScriptFilter:

ContentScriptFilter
-------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``ids``]
      :type: (array of string, optional)
      
      The IDs of specific scripts to retrieve with :code:`getRegisteredContentScripts()` or to unregister with :code:`unregisterContentScripts()`.
   

.. _scripting.ExecutionWorld:

ExecutionWorld
--------------

.. api-section-annotation-hack:: 

The JavaScript world for a script to execute within. :code:`ISOLATED` is the default execution environment of content scripts, :code:`MAIN` is the web page's execution environment.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`ISOLATED`
         
         .. api-member::
            :name: :value:`MAIN`
   

.. _scripting.InjectionResult:

InjectionResult
---------------

.. api-section-annotation-hack:: 

Result of a script injection.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``frameId``
      :type: (integer)
      
      The frame ID associated with the injection.
   
   
   .. api-member::
      :name: [``error``]
      :type: (any, optional)
      
      The error property is set when the script execution failed. The value is typically an (Error) object with a message property, but could be any value (including primitives and undefined) if the script threw or rejected with such a value.
   
   
   .. api-member::
      :name: [``result``]
      :type: (any, optional)
      
      The result of the script execution.
   

.. _scripting.InjectionTarget:

InjectionTarget
---------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``tabId``
      :type: (number)
      
      The ID of the tab into which to inject.
   
   
   .. api-member::
      :name: [``allFrames``]
      :type: (boolean, optional)
      
      Whether the script should inject into all frames within the tab. Defaults to false. This must not be true if :code:`frameIds` is specified.
   
   
   .. api-member::
      :name: [``frameIds``]
      :type: (array of number, optional)
      
      The IDs of specific frames to inject into.
   

.. _scripting.RegisteredContentScript:

RegisteredContentScript
-----------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``id``
      :type: (string)
      
      The id of the content script, specified in the API call.
   
   
   .. api-member::
      :name: [``allFrames``]
      :type: (boolean, optional)
      
      If specified true, it will inject into all frames, even if the frame is not the top-most frame in the tab. Each frame is checked independently for URL requirements; it will not inject into child frames if the URL requirements are not met. Defaults to false, meaning that only the top frame is matched.
   
   
   .. api-member::
      :name: [``css``]
      :type: (array of :ref:`scripting.ExtensionURL`, optional)
      
      The list of CSS files to be injected into matching pages. These are injected in the order they appear in this array.
   
   
   .. api-member::
      :name: [``excludeMatches``]
      :type: (array of string, optional)
      
      Excludes pages that this content script would otherwise be injected into.
   
   
   .. api-member::
      :name: [``js``]
      :type: (array of :ref:`scripting.ExtensionURL`, optional)
      
      The list of JavaScript files to be injected into matching pages. These are injected in the order they appear in this array.
   
   
   .. api-member::
      :name: [``matchOriginAsFallback``]
      :type: (boolean, optional)
      
      If matchOriginAsFallback is true, then the code is also injected in about:, data:, blob: when their origin matches the pattern in 'matches', even if the actual document origin is opaque (due to the use of CSP sandbox or iframe sandbox). Match patterns in 'matches' must specify a wildcard path glob. By default it is :code:`false`.
   
   
   .. api-member::
      :name: [``matches``]
      :type: (array of string, optional)
      
      Specifies which pages this content script will be injected into. Must be specified for :code:`registerContentScripts()`.
   
   
   .. api-member::
      :name: [``persistAcrossSessions``]
      :type: (boolean, optional)
      
      Specifies if this content script will persist into future sessions. Defaults to true.
   
   
   .. api-member::
      :name: [``runAt``]
      :type: (`RunAt <https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extensionTypes/RunAt>`__, optional)
      
      Specifies when JavaScript files are injected into the web page. The preferred and default value is :code:`document_idle`.
   
   
   .. api-member::
      :name: [``world``]
      :type: (:ref:`scripting.ExecutionWorld`, optional)
      
      The JavaScript world for a script to execute within. Defaults to "ISOLATED".
   

.. _scripting.ScriptInjection:

ScriptInjection
---------------

.. api-section-annotation-hack:: 

Details of a script injection

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``target``
      :type: (:ref:`scripting.InjectionTarget`)
      
      Details specifying the target into which to inject the script.
   
   
   .. api-member::
      :name: [``args``]
      :type: (array of any, optional)
      
      The arguments to curry into a provided function. This is only valid if the :code:`func` parameter is specified. These arguments must be JSON-serializable.
   
   
   .. api-member::
      :name: [``files``]
      :type: (array of string, optional)
      
      The path of the JS files to inject, relative to the extension's root directory. Exactly one of :code:`files` and :code:`func` must be specified.
   
   
   .. api-member::
      :name: [``func``]
      :type: (function, optional)
      
      A JavaScript function to inject. This function will be serialized, and then deserialized for injection. This means that any bound parameters and execution context will be lost. Exactly one of :code:`files` and :code:`func` must be specified.
   
   
   .. api-member::
      :name: [``injectImmediately``]
      :type: (boolean, optional)
      
      Whether the injection should be triggered in the target as soon as possible (but not necessarily prior to page load).
   
   
   .. api-member::
      :name: [``world``]
      :type: (:ref:`scripting.ExecutionWorld`, optional)
   

.. rst-class:: api-main-section

External Types
==============

The following types are not defined by this API, but by the underlying Mozilla WebExtension code base. They are included here, because there is no other public documentation available.

.. _scripting.ExtensionURL:

ExtensionURL
------------

.. api-section-annotation-hack:: 

A path relative to the root of the extension.

.. api-header::
   :label: string
