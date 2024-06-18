.. container:: sticky-sidebar

  ≡ downloads API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

=============
downloads API
=============

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`downloads`

   Download files and read and modify the browser’s download history

.. api-member::
   :name: :permission:`downloads.open`

   Open files downloaded to your computer

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`downloads` is required to use ``messenger.downloads.*``.

.. rst-class:: api-main-section

Functions
=========

.. _downloads.acceptDanger:

acceptDanger(downloadId, [callback])
------------------------------------

.. api-section-annotation-hack:: 

Prompt the user to either accept or cancel a dangerous download. :code:`acceptDanger()` does not automatically accept dangerous downloads.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
   
   
   .. api-member::
      :name: [``callback``]
      :type: (function, optional)
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.cancel:

cancel(downloadId)
------------------

.. api-section-annotation-hack:: 

Cancel a download. When :code:`callback` is run, the download is cancelled, completed, interrupted or doesn't exist anymore.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
      
      The id of the download to cancel.
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.download:

download(options)
-----------------

.. api-section-annotation-hack:: 

Download a URL. If the URL uses the HTTP[S] protocol, then the request will include all cookies currently set for its hostname. If both :code:`filename` and :code:`saveAs` are specified, then the Save As dialog will be displayed, pre-populated with the specified :code:`filename`. If the download started successfully, :code:`callback` will be called with the new <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`downloadId`. If there was an error starting the download, then :code:`callback` will be called with :code:`downloadId=undefined` and <a href='extension.html#property-lastError'>chrome.extension.lastError</a> will contain a descriptive string. The error strings are not guaranteed to remain backwards compatible between releases. You must not parse it.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``options``
      :type: (object)
      
      What to download and how.
      
      .. api-member::
         :name: ``url``
         :type: (string)
         
         The URL to download.
      
      
      .. api-member::
         :name: [``allowHttpErrors``]
         :type: (boolean, optional)
         
         When this flag is set to :code:`true`, then the browser will allow downloads to proceed after encountering HTTP errors such as :code:`404 Not Found`.
      
      
      .. api-member::
         :name: [``body``]
         :type: (string, optional)
         
         Post body.
      
      
      .. api-member::
         :name: [``conflictAction``]
         :type: (:ref:`downloads.FilenameConflictAction`, optional)
      
      
      .. api-member::
         :name: [``cookieStoreId``]
         :type: (string, optional)
         
         The cookie store ID of the contextual identity; requires "cookies" permission.
      
      
      .. api-member::
         :name: [``filename``]
         :type: (string, optional)
         
         A file path relative to the Downloads directory to contain the downloaded file.
      
      
      .. api-member::
         :name: [``headers``]
         :type: (array of object, optional)
         
         Extra HTTP headers to send with the request if the URL uses the HTTP[s] protocol. Each header is represented as a dictionary containing the keys :code:`name` and either :code:`value` or :code:`binaryValue`, restricted to those allowed by XMLHttpRequest.
      
      
      .. api-member::
         :name: [``incognito``]
         :type: (boolean, optional)
         
         Whether to associate the download with a private browsing session.
      
      
      .. api-member::
         :name: [``method``]
         :type: (`string`, optional)
         
         The HTTP method to use if the URL uses the HTTP[S] protocol.
         
         Supported values:
         
         .. api-member::
            :name: :value:`GET`
         
         .. api-member::
            :name: :value:`POST`
      
      
      .. api-member::
         :name: [``saveAs``]
         :type: (boolean, optional)
         
         Use a file-chooser to allow the user to select a filename. If the option is not specified, the file chooser will be shown only if the Firefox "Always ask you where to save files" option is enabled (i.e. the pref :code:`browser.download.useDownloadDir` is set to :code:`false`).
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: integer
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.drag:

drag(downloadId)
----------------

.. api-section-annotation-hack:: 

Initiate dragging the file to another application.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.erase:

erase(query)
------------

.. api-section-annotation-hack:: 

Erase matching <a href='#type-DownloadItem'>DownloadItems</a> from history

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``query``
      :type: (:ref:`downloads.DownloadQuery`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of integer
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.getFileIcon:

getFileIcon(downloadId, [options])
----------------------------------

.. api-section-annotation-hack:: 

Retrieve an icon for the specified download. For new downloads, file icons are available after the <a href='#event-onCreated'>onCreated</a> event has been received. The image returned by this function while a download is in progress may be different from the image returned after the download is complete. Icon retrieval is done by querying the underlying operating system or toolkit depending on the platform. The icon that is returned will therefore depend on a number of factors including state of the download, platform, registered file types and visual theme. If a file icon cannot be determined, <a href='extension.html#property-lastError'>chrome.extension.lastError</a> will contain an error message.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
      
      The identifier for the download.
   
   
   .. api-member::
      :name: [``options``]
      :type: (object, optional)
      
      .. api-member::
         :name: [``size``]
         :type: (integer, optional)
         
         The size of the icon.  The returned icon will be square with dimensions size * size pixels.  The default size for the icon is 32x32 pixels.
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: string
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.open:

open(downloadId)
----------------

.. api-section-annotation-hack:: 

Open the downloaded file.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`
   - :permission:`downloads.open`

.. _downloads.pause:

pause(downloadId)
-----------------

.. api-section-annotation-hack:: 

Pause the download. If the request was successful the download is in a paused state. Otherwise <a href='extension.html#property-lastError'>chrome.extension.lastError</a> contains an error message. The request will fail if the download is not active.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
      
      The id of the download to pause.
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.removeFile:

removeFile(downloadId)
----------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.resume:

resume(downloadId)
------------------

.. api-section-annotation-hack:: 

Resume a paused download. If the request was successful the download is in progress and unpaused. Otherwise <a href='extension.html#property-lastError'>chrome.extension.lastError</a> contains an error message. The request will fail if the download is not active.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
      
      The id of the download to resume.
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.search:

search(query)
-------------

.. api-section-annotation-hack:: 

Find <a href='#type-DownloadItem'>DownloadItems</a>. Set :code:`query` to the empty object to get all <a href='#type-DownloadItem'>DownloadItems</a>. To get a specific <a href='#type-DownloadItem'>DownloadItem</a>, set only the :code:`id` field.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``query``
      :type: (:ref:`downloads.DownloadQuery`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`downloads.DownloadItem`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.setShelfEnabled:

setShelfEnabled(enabled)
------------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``enabled``
      :type: (boolean)
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.show:

show(downloadId)
----------------

.. api-section-annotation-hack:: 

Show the downloaded file in its folder in a file manager.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: boolean
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.showDefaultFolder:

showDefaultFolder()
-------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. rst-class:: api-main-section

Events
======

.. _downloads.onChanged:

onChanged
---------

.. api-section-annotation-hack:: 

When any of a <a href='#type-DownloadItem'>DownloadItem</a>'s properties except :code:`bytesReceived` changes, this event fires with the :code:`downloadId` and an object containing the properties that changed.

.. api-header::
   :label: Parameters for onChanged.addListener(listener)

   
   .. api-member::
      :name: ``listener(downloadDelta)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``downloadDelta``
      :type: (object)
      
      .. api-member::
         :name: ``id``
         :type: (integer)
         
         The :code:`id` of the <a href='#type-DownloadItem'>DownloadItem</a> that changed.
      
      
      .. api-member::
         :name: [``canResume``]
         :type: (:ref:`downloads.BooleanDelta`, optional)
      
      
      .. api-member::
         :name: [``danger``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`danger`.
      
      
      .. api-member::
         :name: [``endTime``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`endTime`.
      
      
      .. api-member::
         :name: [``error``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`error`.
      
      
      .. api-member::
         :name: [``exists``]
         :type: (:ref:`downloads.BooleanDelta`, optional)
      
      
      .. api-member::
         :name: [``fileSize``]
         :type: (:ref:`downloads.DoubleDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`fileSize`.
      
      
      .. api-member::
         :name: [``filename``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`filename`.
      
      
      .. api-member::
         :name: [``mime``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`mime`.
      
      
      .. api-member::
         :name: [``paused``]
         :type: (:ref:`downloads.BooleanDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`paused`.
      
      
      .. api-member::
         :name: [``startTime``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`startTime`.
      
      
      .. api-member::
         :name: [``state``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`state`.
      
      
      .. api-member::
         :name: [``totalBytes``]
         :type: (:ref:`downloads.DoubleDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`totalBytes`.
      
      
      .. api-member::
         :name: [``url``]
         :type: (:ref:`downloads.StringDelta`, optional)
         
         Describes a change in a <a href='#type-DownloadItem'>DownloadItem</a>'s :code:`url`.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.onCreated:

onCreated
---------

.. api-section-annotation-hack:: 

This event fires with the <a href='#type-DownloadItem'>DownloadItem</a> object when a download begins.

.. api-header::
   :label: Parameters for onCreated.addListener(listener)

   
   .. api-member::
      :name: ``listener(downloadItem)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``downloadItem``
      :type: (:ref:`downloads.DownloadItem`)
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. _downloads.onErased:

onErased
--------

.. api-section-annotation-hack:: 

Fires with the :code:`downloadId` when a download is erased from history.

.. api-header::
   :label: Parameters for onErased.addListener(listener)

   
   .. api-member::
      :name: ``listener(downloadId)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``downloadId``
      :type: (integer)
      
      The :code:`id` of the <a href='#type-DownloadItem'>DownloadItem</a> that was erased.
   

.. api-header::
   :label: Required permissions

   - :permission:`downloads`

.. rst-class:: api-main-section

Types
=====

.. _downloads.BooleanDelta:

BooleanDelta
------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``current``]
      :type: (boolean, optional)
   
   
   .. api-member::
      :name: [``previous``]
      :type: (boolean, optional)
   

.. _downloads.DangerType:

DangerType
----------

.. api-section-annotation-hack:: 

<dl><dt>file</dt><dd>The download's filename is suspicious.</dd><dt>url</dt><dd>The download's URL is known to be malicious.</dd><dt>content</dt><dd>The downloaded file is known to be malicious.</dd><dt>uncommon</dt><dd>The download's URL is not commonly downloaded and could be dangerous.</dd><dt>safe</dt><dd>The download presents no known danger to the user's computer.</dd></dl>These string constants will never change, however the set of DangerTypes may change.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`file`
         
         .. api-member::
            :name: :value:`url`
         
         .. api-member::
            :name: :value:`content`
         
         .. api-member::
            :name: :value:`uncommon`
         
         .. api-member::
            :name: :value:`host`
         
         .. api-member::
            :name: :value:`unwanted`
         
         .. api-member::
            :name: :value:`safe`
         
         .. api-member::
            :name: :value:`accepted`
   

.. _downloads.DoubleDelta:

DoubleDelta
-----------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``current``]
      :type: (number, optional)
   
   
   .. api-member::
      :name: [``previous``]
      :type: (number, optional)
   

.. _downloads.DownloadItem:

DownloadItem
------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``bytesReceived``
      :type: (number)
      
      Number of bytes received so far from the host, without considering file compression.
   
   
   .. api-member::
      :name: ``canResume``
      :type: (boolean)
   
   
   .. api-member::
      :name: ``danger``
      :type: (:ref:`downloads.DangerType`)
      
      Indication of whether this download is thought to be safe or known to be suspicious.
   
   
   .. api-member::
      :name: ``exists``
      :type: (boolean)
   
   
   .. api-member::
      :name: ``fileSize``
      :type: (number)
      
      Number of bytes in the whole file post-decompression, or -1 if unknown.
   
   
   .. api-member::
      :name: ``filename``
      :type: (string)
      
      Absolute local path.
   
   
   .. api-member::
      :name: ``id``
      :type: (integer)
      
      An identifier that is persistent across browser sessions.
   
   
   .. api-member::
      :name: ``incognito``
      :type: (boolean)
      
      False if this download is recorded in the history, true if it is not recorded.
   
   
   .. api-member::
      :name: ``paused``
      :type: (boolean)
      
      True if the download has stopped reading data from the host, but kept the connection open.
   
   
   .. api-member::
      :name: ``startTime``
      :type: (string)
      
      Number of milliseconds between the unix epoch and when this download began.
   
   
   .. api-member::
      :name: ``state``
      :type: (:ref:`downloads.State`)
      
      Indicates whether the download is progressing, interrupted, or complete.
   
   
   .. api-member::
      :name: ``totalBytes``
      :type: (number)
      
      Number of bytes in the whole file, without considering file compression, or -1 if unknown.
   
   
   .. api-member::
      :name: ``url``
      :type: (string)
      
      Absolute URL.
   
   
   .. api-member::
      :name: [``byExtensionId``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``byExtensionName``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``cookieStoreId``]
      :type: (string, optional)
      
      The cookie store ID of the contextual identity.
   
   
   .. api-member::
      :name: [``endTime``]
      :type: (string, optional)
      
      Number of milliseconds between the unix epoch and when this download ended.
   
   
   .. api-member::
      :name: [``error``]
      :type: (:ref:`downloads.InterruptReason`, optional)
      
      Number indicating why a download was interrupted.
   
   
   .. api-member::
      :name: [``estimatedEndTime``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``mime``]
      :type: (string, optional)
      
      The file's MIME type.
   
   
   .. api-member::
      :name: [``referrer``]
      :type: (string, optional)
   

.. _downloads.DownloadQuery:

DownloadQuery
-------------

.. api-section-annotation-hack:: 

Parameters that combine to specify a predicate that can be used to select a set of downloads.  Used for example in search() and erase()

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``bytesReceived``]
      :type: (number, optional)
      
      Number of bytes received so far from the host, without considering file compression.
   
   
   .. api-member::
      :name: [``cookieStoreId``]
      :type: (string, optional)
      
      The cookie store ID of the contextual identity.
   
   
   .. api-member::
      :name: [``danger``]
      :type: (:ref:`downloads.DangerType`, optional)
      
      Indication of whether this download is thought to be safe or known to be suspicious.
   
   
   .. api-member::
      :name: [``endTime``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``endedAfter``]
      :type: (:ref:`downloads.DownloadTime`, optional)
      
      Limits results to downloads that ended after the given ms since the epoch.
   
   
   .. api-member::
      :name: [``endedBefore``]
      :type: (:ref:`downloads.DownloadTime`, optional)
      
      Limits results to downloads that ended before the given ms since the epoch.
   
   
   .. api-member::
      :name: [``error``]
      :type: (:ref:`downloads.InterruptReason`, optional)
      
      Why a download was interrupted.
   
   
   .. api-member::
      :name: [``exists``]
      :type: (boolean, optional)
   
   
   .. api-member::
      :name: [``fileSize``]
      :type: (number, optional)
      
      Number of bytes in the whole file post-decompression, or -1 if unknown.
   
   
   .. api-member::
      :name: [``filename``]
      :type: (string, optional)
      
      Absolute local path.
   
   
   .. api-member::
      :name: [``filenameRegex``]
      :type: (string, optional)
      
      Limits results to <a href='#type-DownloadItem'>DownloadItems</a> whose :code:`filename` matches the given regular expression.
   
   
   .. api-member::
      :name: [``id``]
      :type: (integer, optional)
   
   
   .. api-member::
      :name: [``limit``]
      :type: (integer, optional)
      
      Setting this integer limits the number of results. Otherwise, all matching <a href='#type-DownloadItem'>DownloadItems</a> will be returned.
   
   
   .. api-member::
      :name: [``mime``]
      :type: (string, optional)
      
      The file's MIME type.
   
   
   .. api-member::
      :name: [``orderBy``]
      :type: (array of string, optional)
      
      Setting elements of this array to <a href='#type-DownloadItem'>DownloadItem</a> properties in order to sort the search results. For example, setting :code:`orderBy='startTime'` sorts the <a href='#type-DownloadItem'>DownloadItems</a> by their start time in ascending order. To specify descending order, prefix :code:`orderBy` with a hyphen: '-startTime'.
   
   
   .. api-member::
      :name: [``paused``]
      :type: (boolean, optional)
      
      True if the download has stopped reading data from the host, but kept the connection open.
   
   
   .. api-member::
      :name: [``query``]
      :type: (array of string, optional)
      
      This array of search terms limits results to <a href='#type-DownloadItem'>DownloadItems</a> whose :code:`filename` or :code:`url` contain all of the search terms that do not begin with a dash '-' and none of the search terms that do begin with a dash.
   
   
   .. api-member::
      :name: [``startTime``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``startedAfter``]
      :type: (:ref:`downloads.DownloadTime`, optional)
      
      Limits results to downloads that started after the given ms since the epoch.
   
   
   .. api-member::
      :name: [``startedBefore``]
      :type: (:ref:`downloads.DownloadTime`, optional)
      
      Limits results to downloads that started before the given ms since the epoch.
   
   
   .. api-member::
      :name: [``state``]
      :type: (:ref:`downloads.State`, optional)
      
      Indicates whether the download is progressing, interrupted, or complete.
   
   
   .. api-member::
      :name: [``totalBytes``]
      :type: (number, optional)
      
      Number of bytes in the whole file, without considering file compression, or -1 if unknown.
   
   
   .. api-member::
      :name: [``totalBytesGreater``]
      :type: (number, optional)
      
      Limits results to downloads whose totalBytes is greater than the given integer.
   
   
   .. api-member::
      :name: [``totalBytesLess``]
      :type: (number, optional)
      
      Limits results to downloads whose totalBytes is less than the given integer.
   
   
   .. api-member::
      :name: [``url``]
      :type: (string, optional)
      
      Absolute URL.
   
   
   .. api-member::
      :name: [``urlRegex``]
      :type: (string, optional)
      
      Limits results to <a href='#type-DownloadItem'>DownloadItems</a> whose :code:`url` matches the given regular expression.
   

.. _downloads.DownloadTime:

DownloadTime
------------

.. api-section-annotation-hack:: 

A time specified as a Date object, a number or string representing milliseconds since the epoch, or an ISO 8601 string

.. api-header::
   :label: string

OR

.. api-header::
   :label: `Date <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date>`__

.. _downloads.FilenameConflictAction:

FilenameConflictAction
----------------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`uniquify`
         
         .. api-member::
            :name: :value:`overwrite`
         
         .. api-member::
            :name: :value:`prompt`
   

.. _downloads.InterruptReason:

InterruptReason
---------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`FILE_FAILED`
         
         .. api-member::
            :name: :value:`FILE_ACCESS_DENIED`
         
         .. api-member::
            :name: :value:`FILE_NO_SPACE`
         
         .. api-member::
            :name: :value:`FILE_NAME_TOO_LONG`
         
         .. api-member::
            :name: :value:`FILE_TOO_LARGE`
         
         .. api-member::
            :name: :value:`FILE_VIRUS_INFECTED`
         
         .. api-member::
            :name: :value:`FILE_TRANSIENT_ERROR`
         
         .. api-member::
            :name: :value:`FILE_BLOCKED`
         
         .. api-member::
            :name: :value:`FILE_SECURITY_CHECK_FAILED`
         
         .. api-member::
            :name: :value:`FILE_TOO_SHORT`
         
         .. api-member::
            :name: :value:`NETWORK_FAILED`
         
         .. api-member::
            :name: :value:`NETWORK_TIMEOUT`
         
         .. api-member::
            :name: :value:`NETWORK_DISCONNECTED`
         
         .. api-member::
            :name: :value:`NETWORK_SERVER_DOWN`
         
         .. api-member::
            :name: :value:`NETWORK_INVALID_REQUEST`
         
         .. api-member::
            :name: :value:`SERVER_FAILED`
         
         .. api-member::
            :name: :value:`SERVER_NO_RANGE`
         
         .. api-member::
            :name: :value:`SERVER_BAD_CONTENT`
         
         .. api-member::
            :name: :value:`SERVER_UNAUTHORIZED`
         
         .. api-member::
            :name: :value:`SERVER_CERT_PROBLEM`
         
         .. api-member::
            :name: :value:`SERVER_FORBIDDEN`
         
         .. api-member::
            :name: :value:`USER_CANCELED`
         
         .. api-member::
            :name: :value:`USER_SHUTDOWN`
         
         .. api-member::
            :name: :value:`CRASH`
   

.. _downloads.State:

State
-----

.. api-section-annotation-hack:: 

<dl><dt>in_progress</dt><dd>The download is currently receiving data from the server.</dd><dt>interrupted</dt><dd>An error broke the connection with the file host.</dd><dt>complete</dt><dd>The download completed successfully.</dd></dl>These string constants will never change, however the set of States may change.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`in_progress`
         
         .. api-member::
            :name: :value:`interrupted`
         
         .. api-member::
            :name: :value:`complete`
   

.. _downloads.StringDelta:

StringDelta
-----------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``current``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``previous``]
      :type: (string, optional)
   
