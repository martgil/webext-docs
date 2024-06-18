.. container:: sticky-sidebar

  ≡ extensionTypes API

  * `Types`_
  * `External Types`_

  .. include:: /overlay/developer-resources.rst

==================
extensionTypes API
==================

.. role:: permission

.. role:: value

.. role:: code

The :code:`browser.extensionTypes` API contains type declarations for WebExtensions.

.. rst-class:: api-main-section

Types
=====

.. _extensionTypes.CSSOrigin:

CSSOrigin
---------

.. api-section-annotation-hack:: 

The origin of the CSS to inject, this affects the cascading order (priority) of the stylesheet.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`user`
         
         .. api-member::
            :name: :value:`author`
   

.. _extensionTypes.Date:

Date
----

.. api-section-annotation-hack:: 

.. api-header::
   :label: string

OR

.. api-header::
   :label: integer

OR

.. api-header::
   :label: `Date <https://developer.mozilla.org/en-US/docs/Web/API/Date>`__

.. _extensionTypes.ExecutionWorld:

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
   

.. _extensionTypes.ExtensionFileOrCode:

ExtensionFileOrCode
-------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         .. api-member::
            :name: ``file``
            :type: (:ref:`extensionTypes.ExtensionURL`)
         
   

OR

.. api-header::
   :label: object

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         .. api-member::
            :name: ``code``
            :type: (string)
         
   

.. _extensionTypes.ImageDetails:

ImageDetails
------------

.. api-section-annotation-hack:: 

Details about the format, quality, area and scale of the capture.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``format``]
      :type: (:ref:`extensionTypes.ImageFormat`, optional)
      
      The format of the resulting image.  Default is :code:`"jpeg"`.
   
   
   .. api-member::
      :name: [``quality``]
      :type: (integer, optional)
      
      When format is :code:`"jpeg"`, controls the quality of the resulting image.  This value is ignored for PNG images.  As quality is decreased, the resulting image will have more visual artifacts, and the number of bytes needed to store it will decrease.
   
   
   .. api-member::
      :name: [``rect``]
      :type: (object, optional)
      
      The area of the document to capture, in CSS pixels, relative to the page.  If omitted, capture the visible viewport.
      
      .. api-member::
         :name: ``height``
         :type: (number)
      
      
      .. api-member::
         :name: ``width``
         :type: (number)
      
      
      .. api-member::
         :name: ``x``
         :type: (number)
      
      
      .. api-member::
         :name: ``y``
         :type: (number)
      
   
   
   .. api-member::
      :name: [``resetScrollPosition``]
      :type: (boolean, optional)
      
      If true, temporarily resets the scroll position of the document to 0. Only takes effect if rect is also specified.
   
   
   .. api-member::
      :name: [``scale``]
      :type: (number, optional)
      
      The scale of the resulting image.  Defaults to :code:`devicePixelRatio`.
   

.. _extensionTypes.ImageFormat:

ImageFormat
-----------

.. api-section-annotation-hack:: 

The format of an image.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`jpeg`
         
         .. api-member::
            :name: :value:`png`
   

.. _extensionTypes.InjectDetails:

InjectDetails
-------------

.. api-section-annotation-hack:: 

Details of the script or CSS to inject. Either the code or the file property must be set, but both may not be set at the same time.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``allFrames``]
      :type: (boolean, optional)
      
      If allFrames is :code:`true`, implies that the JavaScript or CSS should be injected into all frames of current page. By default, it's :code:`false` and is only injected into the top frame.
   
   
   .. api-member::
      :name: [``code``]
      :type: (string, optional)
      
      JavaScript or CSS code to inject.<br><br>**Warning:**<br>Be careful using the :code:`code` parameter. Incorrect use of it may open your extension to `cross site scripting <https://en.wikipedia.org/wiki/Cross-site_scripting>`__ attacks.
   
   
   .. api-member::
      :name: [``cssOrigin``]
      :type: (:ref:`extensionTypes.CSSOrigin`, optional)
      
      The css origin of the stylesheet to inject. Defaults to "author".
   
   
   .. api-member::
      :name: [``file``]
      :type: (string, optional)
      
      JavaScript or CSS file to inject.
   
   
   .. api-member::
      :name: [``frameId``]
      :type: (integer, optional)
      
      The ID of the frame to inject the script into. This may not be used in combination with :code:`allFrames`.
   
   
   .. api-member::
      :name: [``matchAboutBlank``]
      :type: (boolean, optional)
      
      If matchAboutBlank is true, then the code is also injected in about:blank and about:srcdoc frames if your extension has access to its parent document. Code cannot be inserted in top-level about:-frames. By default it is :code:`false`.
   
   
   .. api-member::
      :name: [``runAt``]
      :type: (:ref:`extensionTypes.RunAt`, optional)
      
      The soonest that the JavaScript or CSS will be injected into the tab. Defaults to "document_idle".
   

.. _extensionTypes.PlainJSONValue:

PlainJSONValue
--------------

.. api-section-annotation-hack:: 

A plain JSON value

.. api-header::
   :label: null

OR

.. api-header::
   :label: number

OR

.. api-header::
   :label: string

OR

.. api-header::
   :label: boolean

OR

.. api-header::
   :label: array of :ref:`extensionTypes.PlainJSONValue`

OR

.. api-header::
   :label: object

.. _extensionTypes.RunAt:

RunAt
-----

.. api-section-annotation-hack:: 

The soonest that the JavaScript or CSS will be injected into the tab.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`document_start`
         
         .. api-member::
            :name: :value:`document_end`
         
         .. api-member::
            :name: :value:`document_idle`
   

.. rst-class:: api-main-section

External Types
==============

The following types are not defined by this API, but by the underlying Mozilla WebExtension code base. They are included here, because there is no other public documentation available.

.. _extensionTypes.ExtensionURL:

ExtensionURL
------------

.. api-section-annotation-hack:: 

A path relative to the root of the extension.

.. api-header::
   :label: string
