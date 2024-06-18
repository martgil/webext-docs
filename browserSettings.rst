.. container:: sticky-sidebar

  ≡ browserSettings API

  * `Permissions`_
  * `Types`_
  * `Properties`_

  .. include:: /overlay/developer-resources.rst

===================
browserSettings API
===================

.. role:: permission

.. role:: value

.. role:: code

Use the :code:`browser.browserSettings` API to control global settings of the browser.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`browserSettings`

   Read and modify browser settings

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`browserSettings` is required to use ``messenger.browserSettings.*``.

.. rst-class:: api-main-section

Types
=====

.. _browserSettings.ColorManagementMode:

ColorManagementMode
-------------------

.. api-section-annotation-hack:: 

Color management mode.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`off`
         
         .. api-member::
            :name: :value:`full`
         
         .. api-member::
            :name: :value:`tagged_only`
   

.. _browserSettings.ContextMenuMouseEvent:

ContextMenuMouseEvent
---------------------

.. api-section-annotation-hack:: 

After which mouse event context menus should popup.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`mouseup`
         
         .. api-member::
            :name: :value:`mousedown`
   

.. _browserSettings.ImageAnimationBehavior:

ImageAnimationBehavior
----------------------

.. api-section-annotation-hack:: 

How images should be animated in the browser.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`normal`
         
         .. api-member::
            :name: :value:`none`
         
         .. api-member::
            :name: :value:`once`
   

.. rst-class:: api-main-section

Properties
==========

.. _browserSettings.allowPopupsForUserEvents:

allowPopupsForUserEvents
------------------------

.. api-section-annotation-hack:: 

Allows or disallows pop-up windows from opening in response to user events.

.. _browserSettings.cacheEnabled:

cacheEnabled
------------

.. api-section-annotation-hack:: 

Enables or disables the browser cache.

.. _browserSettings.closeTabsByDoubleClick:

closeTabsByDoubleClick
----------------------

.. api-section-annotation-hack:: 

This boolean setting controls whether the selected tab can be closed with a double click.

.. _browserSettings.contextMenuShowEvent:

contextMenuShowEvent
--------------------

.. api-section-annotation-hack:: 

Controls after which mouse event context menus popup. This setting's value is of type ContextMenuMouseEvent, which has possible values of :code:`mouseup` and :code:`mousedown`.

.. _browserSettings.ftpProtocolEnabled:

ftpProtocolEnabled
------------------

.. api-section-annotation-hack:: 

Returns whether the FTP protocol is enabled. Read-only.

.. _browserSettings.homepageOverride:

homepageOverride
----------------

.. api-section-annotation-hack:: 

Returns the value of the overridden home page. Read-only.

.. _browserSettings.imageAnimationBehavior:

imageAnimationBehavior
----------------------

.. api-section-annotation-hack:: 

Controls the behaviour of image animation in the browser. This setting's value is of type ImageAnimationBehavior, defaulting to :code:`normal`.

.. _browserSettings.newTabPageOverride:

newTabPageOverride
------------------

.. api-section-annotation-hack:: 

Returns the value of the overridden new tab page. Read-only.

.. _browserSettings.newTabPosition:

newTabPosition
--------------

.. api-section-annotation-hack:: 

Controls where new tabs are opened. :value:`afterCurrent` will open all new tabs next to the current tab, :value:`relatedAfterCurrent` will open only related tabs next to the current tab, and :value:`atEnd` will open all tabs at the end of the tab strip. The default is :value:`relatedAfterCurrent`.

.. _browserSettings.openBookmarksInNewTabs:

openBookmarksInNewTabs
----------------------

.. api-section-annotation-hack:: 

This boolean setting controls whether bookmarks are opened in the current tab or in a new tab.

.. _browserSettings.openSearchResultsInNewTabs:

openSearchResultsInNewTabs
--------------------------

.. api-section-annotation-hack:: 

This boolean setting controls whether search results are opened in the current tab or in a new tab.

.. _browserSettings.openUrlbarResultsInNewTabs:

openUrlbarResultsInNewTabs
--------------------------

.. api-section-annotation-hack:: 

This boolean setting controls whether urlbar results are opened in the current tab or in a new tab.

.. _browserSettings.overrideContentColorScheme:

overrideContentColorScheme
--------------------------

.. api-section-annotation-hack:: 

This setting controls whether a light or dark color scheme overrides the page's preferred color scheme.

.. _browserSettings.overrideDocumentColors:

overrideDocumentColors
----------------------

.. api-section-annotation-hack:: 

This setting controls whether the user-chosen colors override the page's colors.

.. _browserSettings.useDocumentFonts:

useDocumentFonts
----------------

.. api-section-annotation-hack:: 

This setting controls whether the document's fonts are used.

.. _browserSettings.webNotificationsDisabled:

webNotificationsDisabled
------------------------

.. api-section-annotation-hack:: 

Disables webAPI notifications.

.. _browserSettings.zoomFullPage:

zoomFullPage
------------

.. api-section-annotation-hack:: 

This boolean setting controls whether zoom is applied to the full page or to text only.

.. _browserSettings.zoomSiteSpecific:

zoomSiteSpecific
----------------

.. api-section-annotation-hack:: 

This boolean setting controls whether zoom is applied on a per-site basis or to the current tab only. If privacy.resistFingerprinting is true, this setting has no effect and zoom is applied to the current tab only.
