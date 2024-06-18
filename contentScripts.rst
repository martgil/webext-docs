.. container:: sticky-sidebar

  ≡ contentScripts API

  * `Functions`_
  * `Types`_
  * `External Types`_

  .. include:: /overlay/developer-resources.rst

==================
contentScripts API
==================

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-main-section

Functions
=========

.. _contentScripts.register:

register(contentScriptOptions)
------------------------------

.. api-section-annotation-hack:: 

Register a content script programmatically

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``contentScriptOptions``
      :type: (:ref:`contentScripts.RegisteredContentScriptOptions`)
   

.. rst-class:: api-main-section

Types
=====

.. _contentScripts.RegisteredContentScript:

RegisteredContentScript
-----------------------

.. api-section-annotation-hack:: 

An object that represents a content script registered programmatically

.. api-header::
   :label: object

   - ``unregister()`` Unregister a content script registered programmatically

.. _contentScripts.RegisteredContentScriptOptions:

RegisteredContentScriptOptions
------------------------------

.. api-section-annotation-hack:: 

Details of a content script registered programmatically

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``matches``
      :type: (array of :ref:`contentScripts.MatchPattern`)
   
   
   .. api-member::
      :name: [``allFrames``]
      :type: (boolean, optional)
      
      If allFrames is :code:`true`, implies that the JavaScript or CSS should be injected into all frames of current page. By default, it's :code:`false` and is only injected into the top frame.
   
   
   .. api-member::
      :name: [``cookieStoreId``]
      :type: (array of string or string, optional)
      
      limit the set of matched tabs to those that belong to the given cookie store id
   
   
   .. api-member::
      :name: [``css``]
      :type: (array of :ref:`contentScripts.extensionTypes.ExtensionFileOrCode`, optional)
      
      The list of CSS files to inject
   
   
   .. api-member::
      :name: [``excludeGlobs``]
      :type: (array of string, optional)
   
   
   .. api-member::
      :name: [``excludeMatches``]
      :type: (array of :ref:`contentScripts.MatchPattern`, optional)
   
   
   .. api-member::
      :name: [``includeGlobs``]
      :type: (array of string, optional)
   
   
   .. api-member::
      :name: [``js``]
      :type: (array of :ref:`contentScripts.extensionTypes.ExtensionFileOrCode`, optional)
      
      The list of JS files to inject
   
   
   .. api-member::
      :name: [``matchAboutBlank``]
      :type: (boolean, optional)
      
      If matchAboutBlank is true, then the code is also injected in about:blank and about:srcdoc frames if your extension has access to its parent document. Ignored if matchOriginAsFallback is specified. By default it is :code:`false`.
   
   
   .. api-member::
      :name: [``matchOriginAsFallback``]
      :type: (boolean, optional)
      
      If matchOriginAsFallback is true, then the code is also injected in about:, data:, blob: when their origin matches the pattern in 'matches', even if the actual document origin is opaque (due to the use of CSP sandbox or iframe sandbox). Match patterns in 'matches' must specify a wildcard path glob. By default it is :code:`false`.
   
   
   .. api-member::
      :name: [``runAt``]
      :type: (`RunAt <https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extensionTypes/RunAt>`__, optional)
      
      The soonest that the JavaScript or CSS will be injected into the tab. Defaults to "document_idle".
   
   
   .. api-member::
      :name: [``world``]
      :type: (`ExecutionWorld <https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extensionTypes/ExecutionWorld>`__, optional)
      
      The JavaScript world for a script to execute within. Defaults to "ISOLATED".
   

.. rst-class:: api-main-section

External Types
==============

The following types are not defined by this API, but by the underlying Mozilla WebExtension code base. They are included here, because there is no other public documentation available.

.. _contentScripts.extensionTypes.ExtensionFileOrCode:

ExtensionFileOrCode
-------------------

.. api-section-annotation-hack:: 

Specify code, either by pointing to a file or by providing the code directly. Only one of the two is allowed.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``code``
      :type: (string)
      
      Some JavaScript code to register.
   
   
   .. api-member::
      :name: ``file``
      :type: (string)
      
      A URL starting at the extension's manifest.json and pointing to a JavaScript file to register.
   
