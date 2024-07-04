.. container:: sticky-sidebar

  ≡ messages API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

  ≡ Related information
  
  * :doc:`/examples/messageLists`
  * :doc:`/examples/eventListeners`

============
messages API
============

The messages API allows to access and manage the user's messages.

.. note::

  When the term ``messageId`` is used in these documents, it *doesn't* refer to the Message-ID
  email header. It is an internal tracking number that does not remain after a restart. Nor does
  it follow an email that has been moved to a different folder.

.. warning::

  Some functions in this API potentially return *a lot* of messages. Be careful what you wish for!
  See :doc:`examples/messageLists` for more information.

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`messagesDelete`

   Permanently delete your email messages

.. api-member::
   :name: :permission:`messagesImport`

   Import messages into Thunderbird

.. api-member::
   :name: :permission:`messagesMove`

   Copy or move your email messages (including moving them to the trash folder)

.. api-member::
   :name: :permission:`messagesRead`

   Read your email messages

.. api-member::
   :name: :permission:`messagesUpdate`

   Change properties and tags of your email messages

.. api-member::
   :name: :permission:`messagesModifyPermanent`

   Permanently modify the source of your messages (including headers, body and attachments)

.. api-member::
   :name: :permission:`sensitiveDataUpload`

   Transfer sensitive user data (if access has been granted) to a remote server for further processing

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`messagesRead` is required to use ``messenger.messages.*``.

.. rst-class:: api-main-section

Functions
=========

.. _messages.archive:

archive(messageIds)
-------------------

.. api-section-annotation-hack:: 

Archives messages using the current settings. Archiving external messages will throw an *ExtensionError*.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageIds``
      :type: (array of :ref:`messages.MessageId`)
      
      The IDs of the messages to archive.
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`messagesMove`

.. _messages.copy:

copy(messageIds, folderId)
--------------------------

.. api-section-annotation-hack:: 

Copies messages to a specified folder.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageIds``
      :type: (array of :ref:`messages.MessageId`)
      
      The IDs of the messages to copy.
   
   
   .. api-member::
      :name: ``folderId``
      :type: (:ref:`folders.MailFolderId`)
      
      The folder to copy the messages to.
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`
   - :permission:`messagesMove`

.. _messages.delete:

delete(messageIds, [skipTrash])
-------------------------------

.. api-section-annotation-hack:: 

Deletes messages permanently, or moves them to the trash folder (honoring the account's deletion behavior settings). Deleting external messages will throw an *ExtensionError*. The :value:`skipTrash` parameter allows immediate permanent deletion, bypassing the trash folder.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageIds``
      :type: (array of :ref:`messages.MessageId`)
      
      The IDs of the messages to delete.
   
   
   .. api-member::
      :name: [``skipTrash``]
      :type: (boolean, optional)
      
      If true, the message will be deleted permanently, regardless of the account's deletion behavior settings.
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`messagesDelete`

.. _messages.get:

get(messageId)
--------------

.. api-section-annotation-hack:: 

Returns the specified message.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`messages.MessageHeader`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.getFull:

getFull(messageId, [options])
-----------------------------

.. api-section-annotation-hack:: 

Returns the specified message, including all headers and MIME parts. Throws if the message could not be read, for example due to network issues.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   
   
   .. api-member::
      :name: [``options``]
      :type: (object, optional)
      
      .. api-member::
         :name: [``decrypt``]
         :type: (boolean, optional)
         
         Whether the message should be decrypted. If the message could not be decrypted, its parts are omitted. Defaults to true.
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`messages.MessagePart`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.getRaw:

getRaw(messageId, [options])
----------------------------

.. api-section-annotation-hack:: -- [Added in TB 72, backported to TB 68.7]

Returns the unmodified source of a message. Throws if the message could not be read, for example due to network issues.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   
   
   .. api-member::
      :name: [``options``]
      :type: (object, optional)
      
      .. api-member::
         :name: [``data_format``]
         :type: (`string`, optional)
         
         The message can either be returned as a DOM File (default) or as a `binary string <https://developer.mozilla.org/en-US/docs/Web/API/DOMString/Binary>`__. It is recommended to use the :value:`File` format, because the DOM File object can be used as-is with the downloads API and has useful methods to access the content, like `File.text() <https://developer.mozilla.org/en-US/docs/Web/API/Blob/text>`__ and `File.arrayBuffer() <https://developer.mozilla.org/en-US/docs/Web/API/Blob/arrayBuffer>`__. Working with binary strings is error prone and needs special handling: 
         
         .. literalinclude:: includes/messages/decodeBinaryString.js
           :language: JavaScript
         
         
         
         (see MDN for `supported input encodings <https://developer.mozilla.org/en-US/docs/Web/API/Encoding_API/Encodings>`__).
         
         Supported values:
         
         .. api-member::
            :name: :value:`BinaryString`
         
         .. api-member::
            :name: :value:`File`
      
      
      .. api-member::
         :name: [``decrypt``]
         :type: (boolean, optional)
         
         Whether the message should be decrypted. Throws, if the message could not be decrypted.
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: string or `File <https://developer.mozilla.org/en-US/docs/Web/API/File>`__
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.import:

import(file, folderId, [properties])
------------------------------------

.. api-section-annotation-hack:: -- [Added in TB 106]

Imports a message into a local Thunderbird folder. To import a message into an IMAP folder, add it to a local folder first and then move it to the IMAP folder.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``file``
      :type: (`File <https://developer.mozilla.org/en-US/docs/Web/API/File>`__)
   
   
   .. api-member::
      :name: ``folderId``
      :type: (:ref:`folders.MailFolderId`)
      
      The folder to import the messages into.
   
   
   .. api-member::
      :name: [``properties``]
      :type: (:ref:`messages.MessageProperties`, optional)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`messages.MessageHeader`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`
   - :permission:`messagesImport`

.. _messages.list:

list(folderId)
--------------

.. api-section-annotation-hack:: 

Gets all messages in a folder.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``folderId``
      :type: (:ref:`folders.MailFolderId`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`messages.MessageList`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`

.. _messages.listInlineTextParts:

listInlineTextParts(messageId)
------------------------------

.. api-section-annotation-hack:: 

Lists all inline text parts of a message. These parts are not returned by :ref:`messages.listAttachments` and usually make up the readable content of the message, mostly with content type :value:`text/plain` or :value:`text/html`. If a message only includes a part with content type :value:`text/html`, the method :ref:`messengerUtilities.convertToPlainText` can be used to retreive a plain text version. 

**Note:** A message usually contains only one inline text part per subtype, but technically messages can contain multiple inline text parts per subtype.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`messages.InlineTextPart`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.move:

move(messageIds, folderId)
--------------------------

.. api-section-annotation-hack:: 

Moves messages to a specified folder. If the messages cannot be removed from the source folder, they will be copied instead of moved. Moving external messages will throw an *ExtensionError*.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageIds``
      :type: (array of :ref:`messages.MessageId`)
      
      The IDs of the messages to move.
   
   
   .. api-member::
      :name: ``folderId``
      :type: (:ref:`folders.MailFolderId`)
      
      The folder to move the messages to.
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`
   - :permission:`messagesMove`

.. _messages.query:

query([queryInfo])
------------------

.. api-section-annotation-hack:: -- [Added in TB 69, backported to TB 68.2]

Gets all messages that have the specified properties, or all messages if no properties are specified. Messages of unified mailbox folders are not included by default (as that could double the amount of returned messages), but explicitly specifying a unified mailbox folder is supported.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``queryInfo``]
      :type: (object, optional)
      
      .. api-member::
         :name: [``accountId``]
         :type: (:ref:`accounts.MailAccountId`, optional)
         
         Limits the search to folders of the account with the specified id.
      
      
      .. api-member::
         :name: [``attachment``]
         :type: (boolean or :ref:`messages.QueryRange`, optional)
         :annotation: -- [Added in TB 96, backported to TB 91.4.1]
         
         Whether the message has attachments, or not. Supports to specify a :ref:`messages.QueryRange` (min/max) instead of a simple boolean value (none/some).
      
      
      .. api-member::
         :name: [``author``]
         :type: (string, optional)
         
         Returns only messages with this value matching the author. The search value is a single email address, a name or a combination (e.g.: :value:`Name <user@domain.org>`). The address part of the search value (if provided) must match the author's address completely. The name part of the search value (if provided) must match the author's name partially. All matches are done case-insensitive.
      
      
      .. api-member::
         :name: [``autoPaginationTimeout``]
         :type: (integer, optional)
         :annotation: -- [Added in TB 120]
         
         Set the timeout in ms after which results should be returned, even if the nominal number of messages-per-page has not yet been reached. Defaults to :value:`1000` ms. Setting it to :value:`0` will disable auto-pagination.
      
      
      .. api-member::
         :name: [``body``]
         :type: (string, optional)
         
         Returns only messages with this value in the body of the mail.
      
      
      .. api-member::
         :name: [``flagged``]
         :type: (boolean, optional)
         
         Returns only flagged (or unflagged if false) messages.
      
      
      .. api-member::
         :name: [``folderId``]
         :type: (:ref:`folders.MailFolderId`, optional)
         
         Returns only messages from the folder with the specified id. The :permission:`accountsRead` permission is required.
      
      
      .. api-member::
         :name: [``fromDate``]
         :type: (`Date <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date>`__, optional)
         
         Returns only messages with a date after this value.
      
      
      .. api-member::
         :name: [``fromMe``]
         :type: (boolean, optional)
         
         Returns only messages with the author's address matching any configured identity.
      
      
      .. api-member::
         :name: [``fullText``]
         :type: (string, optional)
         
         Returns only messages with this value somewhere in the mail (subject, body or author).
      
      
      .. api-member::
         :name: [``headerMessageId``]
         :type: (string, optional)
         :annotation: -- [Added in TB 85]
         
         Returns only messages with a Message-ID header matching this value.
      
      
      .. api-member::
         :name: [``includeSubFolders``]
         :type: (boolean, optional)
         :annotation: -- [Added in TB 91]
         
         Search the specified folder recursively.
      
      
      .. api-member::
         :name: [``junk``]
         :type: (boolean, optional)
         :annotation: -- [Added in TB 121]
         
         Returns only messages whith the specified junk state.
      
      
      .. api-member::
         :name: [``junkScore``]
         :type: (:ref:`messages.QueryRange`, optional)
         :annotation: -- [Added in TB 121]
         
         Returns only messages with a junk score in the specified range.
      
      
      .. api-member::
         :name: [``messagesPerPage``]
         :type: (integer, optional)
         :annotation: -- [Added in TB 120]
         
         Set the nominal number of messages-per-page for this query. Defaults to :value:`100` messages.
      
      
      .. api-member::
         :name: [``new``]
         :type: (boolean, optional)
         :annotation: -- [Added in TB 121]
         
         Returns only messages with the specified new state.
      
      
      .. api-member::
         :name: [``read``]
         :type: (boolean, optional)
         
         Returns only messages with the specified read state.
      
      
      .. api-member::
         :name: [``recipients``]
         :type: (string, optional)
         
         Returns only messages whose recipients match all specified addresses. The search value is a semicolon separated list of email addresses, names or combinations (e.g.: :value:`Name <user@domain.org>`). For a match, all specified addresses must equal a recipient's address completely and all specified names must match a recipient's name partially. All matches are done case-insensitive.
      
      
      .. api-member::
         :name: [``returnMessageListId``]
         :type: (boolean, optional)
         :annotation: -- [Added in TB 120]
         
         The *messageListId* is usually returned together with the first page, after some messages have been found. Enabling this option will change the return value of this function and return the *messageListId* directly.
      
      
      .. api-member::
         :name: [``size``]
         :type: (:ref:`messages.QueryRange`, optional)
         :annotation: -- [Added in TB 121]
         
         Returns only messages with a size in the specified byte range.
      
      
      .. api-member::
         :name: [``subject``]
         :type: (string, optional)
         
         Returns only messages whose subject contains the provided string.
      
      
      .. api-member::
         :name: [``tags``]
         :type: (:ref:`messages.tags.TagsDetail`, optional)
         :annotation: -- [Added in TB 74]
         
         Returns only messages with the specified tags. For a list of available tags, call the :ref:`messages.tags.list` method.
      
      
      .. api-member::
         :name: [``toDate``]
         :type: (`Date <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date>`__, optional)
         
         Returns only messages with a date before this value.
      
      
      .. api-member::
         :name: [``toMe``]
         :type: (boolean, optional)
         
         Returns only messages with at least one recipient address matching any configured identity.
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`messages.MessageList` or string
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.update:

update(messageId, newProperties)
--------------------------------

.. api-section-annotation-hack:: 

Updates message properties and tags. Updating external messages will throw an *ExtensionError*.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   
   
   .. api-member::
      :name: ``newProperties``
      :type: (:ref:`messages.MessageProperties`)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`messagesUpdate`

.. _messages.abortList:

abortList(messageListId)
------------------------

.. api-section-annotation-hack:: -- [Added in TB 120]

Finalizes the specified list and terminates any process currently still adding messages.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageListId``
      :type: (string)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.continueList:

continueList(messageListId)
---------------------------

.. api-section-annotation-hack:: 

Returns the next chunk of messages in a list. See :doc:`examples/messageLists` for more information.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageListId``
      :type: (string)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`messages.MessageList`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.deleteAttachments:

deleteAttachments(messageId, partNames)
---------------------------------------

.. api-section-annotation-hack:: -- [Added in TB 123]

Deletes the specified attachments and replaces them by placeholder text attachments with meta information about the original attachments and a :value:`text/x-moz-deleted` content type. This permanently modifies the message.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (integer)
   
   
   .. api-member::
      :name: ``partNames``
      :type: (array of string)
      
      An array of attachments, identifying the to be deleted attachments by their :value:`partName`.
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`messagesModifyPermanent`

.. _messages.getAttachmentFile:

getAttachmentFile(messageId, partName)
--------------------------------------

.. api-section-annotation-hack:: -- [Added in TB 88]

Gets the content of a :ref:`messages.MessageAttachment` as a `File <https://developer.mozilla.org/docs/Web/API/File>`__ object.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   
   
   .. api-member::
      :name: ``partName``
      :type: (string)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: `File <https://developer.mozilla.org/en-US/docs/Web/API/File>`__
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

The most simple way to get the content of an attachment is to use the `text() <https://developer.mozilla.org/en-US/docs/Web/API/Blob/text>`__ method of the returned `File <https://developer.mozilla.org/en-US/docs/Web/API/File>`__ object:

.. literalinclude:: includes/messages/file.js
  :language: JavaScript

.. _messages.listAttachments:

listAttachments(messageId)
--------------------------

.. api-section-annotation-hack:: -- [Added in TB 88]

Lists the attachments of a message.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`messages.MessageAttachment`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. _messages.openAttachment:

openAttachment(messageId, partName, tabId)
------------------------------------------

.. api-section-annotation-hack:: -- [Added in TB 114]

Opens the specified attachment.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``messageId``
      :type: (:ref:`messages.MessageId`)
   
   
   .. api-member::
      :name: ``partName``
      :type: (string)
   
   
   .. api-member::
      :name: ``tabId``
      :type: (integer)
      
      The ID of the tab associated with the message opening.
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. rst-class:: api-main-section

Events
======

.. _messages.onCopied:

onCopied
--------

.. api-section-annotation-hack:: -- [Added in TB 91]

Fired when messages have been copied.

.. api-header::
   :label: Parameters for onCopied.addListener(listener)

   
   .. api-member::
      :name: ``listener(originalMessages, copiedMessages)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``originalMessages``
      :type: (:ref:`messages.MessageList`)
   
   
   .. api-member::
      :name: ``copiedMessages``
      :type: (:ref:`messages.MessageList`)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`

.. _messages.onDeleted:

onDeleted
---------

.. api-section-annotation-hack:: -- [Added in TB 91]

Fired when messages have been permanently deleted.

.. api-header::
   :label: Parameters for onDeleted.addListener(listener)

   
   .. api-member::
      :name: ``listener(messages)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``messages``
      :type: (:ref:`messages.MessageList`)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`

.. _messages.onMoved:

onMoved
-------

.. api-section-annotation-hack:: -- [Added in TB 91]

Fired when messages have been moved.

.. api-header::
   :label: Parameters for onMoved.addListener(listener)

   
   .. api-member::
      :name: ``listener(originalMessages, movedMessages)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``originalMessages``
      :type: (:ref:`messages.MessageList`)
   
   
   .. api-member::
      :name: ``movedMessages``
      :type: (:ref:`messages.MessageList`)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`

.. _messages.onNewMailReceived:

onNewMailReceived
-----------------

.. api-section-annotation-hack:: -- [Added in TB 75]

Fired when a new message is received, and has been through junk classification and message filters.

.. api-header::
   :label: Parameters for onNewMailReceived.addListener(listener, monitorAllFolders)

   
   .. api-member::
      :name: ``listener(folder, messages)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: [``monitorAllFolders``]
      :type: (boolean, optional)
      :annotation: -- [Added in TB 121]
      
      Monitor all folders (including all special use folders as defined by :ref:`folders.MailFolderSpecialUse`) instead of just inbox folders and normal folders.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``folder``
      :type: (:ref:`folders.MailFolder`)
   
   
   .. api-member::
      :name: ``messages``
      :type: (:ref:`messages.MessageList`)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`
   - :permission:`accountsRead`

.. _messages.onUpdated:

onUpdated
---------

.. api-section-annotation-hack:: -- [Added in TB 91]

Fired when one or more properties of a message have been updated.

.. api-header::
   :label: Parameters for onUpdated.addListener(listener)

   
   .. api-member::
      :name: ``listener(message, changedProperties)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``message``
      :type: (:ref:`messages.MessageHeader`)
   
   
   .. api-member::
      :name: ``changedProperties``
      :type: (:ref:`messages.MessageProperties`)
   

.. api-header::
   :label: Required permissions

   - :permission:`messagesRead`

.. rst-class:: api-main-section

Types
=====

.. _messages.InlineTextPart:

InlineTextPart
--------------

.. api-section-annotation-hack:: 

An inline part with content type :value:`text/*`. These parts are not returned by :ref:`messages.listAttachments` and usually make up the readable content of the message, mostly with content type :value:`text/plain` or :value:`text/html`

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``content``
      :type: (string)
      
      The content of this inline text part.
   
   
   .. api-member::
      :name: ``contentType``
      :type: (string)
      
      The content type of the part. Most common types for inline text parts are :value:`text/plain` and :value:`text/html`. Possible other (deprecated) types are :value:`text/richtext` and :value:`text/enriched`. Some calendaring services include an inline text part with type :value:`text/calendar`.
   

.. _messages.MessageAttachment:

MessageAttachment
-----------------

.. api-section-annotation-hack:: 

Represents an attachment in a message. This includes all MIME parts with a *content-disposition* header set to :value:`attachment`, but also related parts like inline images.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``contentType``
      :type: (string)
      
      The content type of the attachment. A value of :value:`text/x-moz-deleted` indicates that the original attachment was permanently deleted and replaced by a placeholder text attachment with some meta information about the original attachment.
   
   
   .. api-member::
      :name: ``name``
      :type: (string)
      
      The name, as displayed to the user, of this attachment. This is usually but not always the filename of the attached file.
   
   
   .. api-member::
      :name: ``partName``
      :type: (string)
      
      Identifies the MIME part of the message associated with this attachment.
   
   
   .. api-member::
      :name: ``size``
      :type: (integer)
      
      The size in bytes of this attachment.
   
   
   .. api-member::
      :name: [``contentId``]
      :type: (string, optional)
      
      The content-id of this part. Available for related parts, which are referenced from other places inside the same message (e.g. inline images).
   
   
   .. api-member::
      :name: [``message``]
      :type: (:ref:`messages.MessageHeader`, optional)
      
      A MessageHeader, if this attachment is a message.
   

.. _messages.MessageHeader:

MessageHeader
-------------

.. api-section-annotation-hack:: 

Basic information about a message.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``author``
      :type: (string)
   
   
   .. api-member::
      :name: ``bccList``
      :type: (array of string)
      
      The Bcc recipients. Not populated for news/nntp messages.
   
   
   .. api-member::
      :name: ``ccList``
      :type: (array of string)
      
      The Cc recipients. Not populated for news/nntp messages.
   
   
   .. api-member::
      :name: ``date``
      :type: (`Date <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date>`__)
   
   
   .. api-member::
      :name: ``external``
      :type: (boolean)
      :annotation: -- [Added in TB 106]
      
      Whether this message is a real message or an external message (opened from a file or from an attachment).
   
   
   .. api-member::
      :name: ``flagged``
      :type: (boolean)
      
      Whether this message is flagged (a.k.a. starred).
   
   
   .. api-member::
      :name: ``headerMessageId``
      :type: (string)
      :annotation: -- [Added in TB 85]
      
      The message-id header of the message.
   
   
   .. api-member::
      :name: ``headersOnly``
      :type: (boolean)
      :annotation: -- [Added in TB 102]
      
      Some account types (for example :value:`pop3`) allow to download only the headers of the message, but not its body. The body of such messages will not be available.
   
   
   .. api-member::
      :name: ``id``
      :type: (:ref:`messages.MessageId`)
   
   
   .. api-member::
      :name: ``junk``
      :type: (boolean)
      :annotation: -- [Added in TB 74]
      
      Whether the message has been marked as junk. Always :value:`false` for news/nntp messages and external messages.
   
   
   .. api-member::
      :name: ``junkScore``
      :type: (integer)
      :annotation: -- [Added in TB 74]
      
      The junk score associated with the message. Always :value:`0` for news/nntp messages and external messages.
   
   
   .. api-member::
      :name: ``new``
      :type: (boolean)
      :annotation: -- [Added in TB 106]
      
      Whether the message has been received recently and is marked as new.
   
   
   .. api-member::
      :name: ``recipients``
      :type: (array of string)
      
      The To recipients. Not populated for news/nntp messages.
   
   
   .. api-member::
      :name: ``size``
      :type: (integer)
      :annotation: -- [Added in TB 90]
      
      The total size of the message in bytes.
   
   
   .. api-member::
      :name: ``subject``
      :type: (string)
      
      The subject of the message.
   
   
   .. api-member::
      :name: ``tags``
      :type: (array of string)
      
      Tags associated with this message. For a list of available tags, use :ref:`messages.tags.list`.
   
   
   .. api-member::
      :name: [``folder``]
      :type: (:ref:`folders.MailFolder`, optional)
      
      The :permission:`accountsRead` permission is required for this property to be included. Not available for external or attached messages.
   
   
   .. api-member::
      :name: [``read``]
      :type: (boolean, optional)
      
      Whether the message has been marked as read. Not available for external or attached messages.
   

.. _messages.MessageId:

MessageId
---------

.. api-section-annotation-hack:: 

A unique id representing a :ref:`messages.MessageHeader` and the associated message. This id doesn’t refer to the Message-ID email header. It is an internal tracking number that does not remain after a restart. Nor does it follow an email that has been moved to a different folder.

.. api-header::
   :label: integer

.. _messages.MessageList:

MessageList
-----------

.. api-section-annotation-hack:: 

See :doc:`examples/messageLists` for more information.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``id``
      :type: (string or null)
      
      Id of the message list, to be used with :ref:`messages.continueList` or :ref:`messages.abortList`.
   
   
   .. api-member::
      :name: ``messages``
      :type: (array of :ref:`messages.MessageHeader`)
   

.. _messages.MessagePart:

MessagePart
-----------

.. api-section-annotation-hack:: 

Represents an email message "part", which could be the whole message.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``body``]
      :type: (string, optional)
      
      The content of the part.
   
   
   .. api-member::
      :name: [``contentType``]
      :type: (string, optional)
   
   
   .. api-member::
      :name: [``decryptionStatus``]
      :type: (`string`, optional)
      
      The decryption status, only available for the root part.
      
      Supported values:
      
      .. api-member::
         :name: :value:`none`
      
      .. api-member::
         :name: :value:`skipped`
      
      .. api-member::
         :name: :value:`success`
      
      .. api-member::
         :name: :value:`fail`
   
   
   .. api-member::
      :name: [``headers``]
      :type: (object, optional)
      
      A *dictionary object* of part headers as *key-value* pairs, with the header name as *key*, and an array of headers as *value*.
   
   
   .. api-member::
      :name: [``name``]
      :type: (string, optional)
      
      Name of the part, if it is a file.
   
   
   .. api-member::
      :name: [``partName``]
      :type: (string, optional)
      
      The identifier of this part, used in :ref:`messages.getAttachmentFile`.
   
   
   .. api-member::
      :name: [``parts``]
      :type: (array of :ref:`messages.MessagePart`, optional)
      
      Any sub-parts of this part.
   
   
   .. api-member::
      :name: [``size``]
      :type: (integer, optional)
      
      The size of this part. The size of parts with content type *message/rfc822* is not the actual message size (on disc), but the total size of its decoded body parts, excluding headers.
   

.. _messages.MessageProperties:

MessageProperties
-----------------

.. api-section-annotation-hack:: 

Message properties used in :ref:`messages.update` and :ref:`messages.import`. They can also be monitored by :ref:`messages.onUpdated`.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``flagged``]
      :type: (boolean, optional)
      
      Whether the message is flagged (a.k.a starred).
   
   
   .. api-member::
      :name: [``junk``]
      :type: (boolean, optional)
      
      Whether the message is marked as junk. Only supported in :ref:`messages.update`.
   
   
   .. api-member::
      :name: [``new``]
      :type: (boolean, optional)
      :annotation: -- [Added in TB 106]
      
      Whether the message is marked as new. Only supported in :ref:`messages.import`.
   
   
   .. api-member::
      :name: [``read``]
      :type: (boolean, optional)
      
      Whether the message is marked as read.
   
   
   .. api-member::
      :name: [``tags``]
      :type: (array of string, optional)
      
      Tags associated with this message. For a list of available tags, call the :ref:`messages.tags.list` method.
   

.. _messages.QueryRange:

QueryRange
----------

.. api-section-annotation-hack:: 

An object defining a range.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``max``]
      :type: (integer, optional)
      
      The maximum value required to match the query.
   
   
   .. api-member::
      :name: [``min``]
      :type: (integer, optional)
      
      The minimum value required to match the query.
   
