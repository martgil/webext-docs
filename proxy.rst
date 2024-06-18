.. container:: sticky-sidebar

  ≡ proxy API

  * `Permissions`_
  * `Events`_
  * `Types`_
  * `Properties`_

  .. include:: /overlay/developer-resources.rst

=========
proxy API
=========

.. role:: permission

.. role:: value

.. role:: code

Provides access to global proxy settings for Firefox and proxy event listeners to handle dynamic proxy implementations.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`proxy`

   Control browser proxy settings

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`proxy` is required to use ``messenger.proxy.*``.

.. rst-class:: api-main-section

Events
======

.. _proxy.onError:

onError
-------

.. api-section-annotation-hack:: 

Notifies about errors caused by the invalid use of the proxy API.

.. api-header::
   :label: Parameters for onError.addListener(listener)

   
   .. api-member::
      :name: ``listener(error)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``error``
      :type: (object)
   

.. api-header::
   :label: Required permissions

   - :permission:`proxy`

.. _proxy.onRequest:

onRequest
---------

.. api-section-annotation-hack:: 

Fired when proxy data is needed for a request.

.. api-header::
   :label: Parameters for onRequest.addListener(listener, filter, extraInfoSpec)

   
   .. api-member::
      :name: ``listener(details)``
      
      A function that will be called when this event occurs.
   
   
   .. api-member::
      :name: ``filter``
      :type: (:ref:`webRequest.RequestFilter`)
      
      A set of filters that restricts the events that will be sent to this listener.
   
   
   .. api-member::
      :name: [``extraInfoSpec``]
      :type: (array of `string`, optional)
      
      Array of extra information that should be passed to the listener function.
      
      Supported values:
      
      .. api-member::
         :name: :value:`requestHeaders`
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``details``
      :type: (object)
      
      .. api-member::
         :name: ``frameId``
         :type: (integer)
         
         The value 0 indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (:code:`type` is :code:`main_frame` or :code:`sub_frame`), :code:`frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
      
      
      .. api-member::
         :name: ``fromCache``
         :type: (boolean)
         
         Indicates if this response was fetched from disk cache.
      
      
      .. api-member::
         :name: ``method``
         :type: (string)
         
         Standard HTTP method.
      
      
      .. api-member::
         :name: ``parentFrameId``
         :type: (integer)
         
         ID of frame that wraps the frame which sent the request. Set to -1 if no parent frame exists.
      
      
      .. api-member::
         :name: ``requestId``
         :type: (string)
         
         The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
      
      
      .. api-member::
         :name: ``tabId``
         :type: (integer)
         
         The ID of the tab in which the request takes place. Set to -1 if the request isn't related to a tab.
      
      
      .. api-member::
         :name: ``thirdParty``
         :type: (boolean)
         
         Indicates if this request and its content window hierarchy is third party.
      
      
      .. api-member::
         :name: ``timeStamp``
         :type: (number)
         
         The time when this signal is triggered, in milliseconds since the epoch.
      
      
      .. api-member::
         :name: ``type``
         :type: (:ref:`webRequest.ResourceType`)
         
         How the requested resource will be used.
      
      
      .. api-member::
         :name: ``url``
         :type: (string)
      
      
      .. api-member::
         :name: ``urlClassification``
         :type: (:ref:`webRequest.UrlClassification`)
         
         Url classification if the request has been classified.
      
      
      .. api-member::
         :name: [``cookieStoreId``]
         :type: (string, optional)
         
         The cookie store ID of the contextual identity.
      
      
      .. api-member::
         :name: [``documentUrl``]
         :type: (string, optional)
         
         URL of the page into which the requested resource will be loaded.
      
      
      .. api-member::
         :name: [``incognito``]
         :type: (boolean, optional)
         
         True for private browsing requests.
      
      
      .. api-member::
         :name: [``originUrl``]
         :type: (string, optional)
         
         URL of the resource that triggered this request.
      
      
      .. api-member::
         :name: [``requestHeaders``]
         :type: (:ref:`webRequest.HttpHeaders`, optional)
         
         The HTTP request headers that are going to be sent out with this request.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`proxy`

.. rst-class:: api-main-section

Types
=====

.. _proxy.ProxyConfig:

ProxyConfig
-----------

.. api-section-annotation-hack:: 

An object which describes proxy settings.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``autoConfigUrl``]
      :type: (string, optional)
      
      A URL to use to configure the proxy.
   
   
   .. api-member::
      :name: [``autoLogin``]
      :type: (boolean, optional)
      
      Do not prompt for authentication if password is saved.
   
   
   .. api-member::
      :name: [``ftp``]
      :type: (string, optional) **Deprecated.**
      
      The address of the ftp proxy, can include a port.  Deprecated since Firefox 88.
   
   
   .. api-member::
      :name: [``http``]
      :type: (string, optional)
      
      The address of the http proxy, can include a port.
   
   
   .. api-member::
      :name: [``httpProxyAll``]
      :type: (boolean, optional)
      
      Use the http proxy server for all protocols.
   
   
   .. api-member::
      :name: [``passthrough``]
      :type: (string, optional)
      
      A list of hosts which should not be proxied.
   
   
   .. api-member::
      :name: [``proxyDNS``]
      :type: (boolean, optional)
      
      Proxy DNS when using SOCKS. DNS queries get leaked to the network when set to false. True by default for SOCKS v5. False by default for SOCKS v4.
   
   
   .. api-member::
      :name: [``proxyType``]
      :type: (`string`, optional)
      
      The type of proxy to use.
      
      Supported values:
      
      .. api-member::
         :name: :value:`none`
      
      .. api-member::
         :name: :value:`autoDetect`
      
      .. api-member::
         :name: :value:`system`
      
      .. api-member::
         :name: :value:`manual`
      
      .. api-member::
         :name: :value:`autoConfig`
   
   
   .. api-member::
      :name: [``respectBeConservative``]
      :type: (boolean, optional)
      
       If true (the default value), do not use newer TLS protocol features that might have interoperability problems on the Internet. This is intended only for use with critical infrastructure like the updates, and is only available to privileged addons.
   
   
   .. api-member::
      :name: [``socks``]
      :type: (string, optional)
      
      The address of the socks proxy, can include a port.
   
   
   .. api-member::
      :name: [``socksVersion``]
      :type: (integer, optional)
      
      The version of the socks proxy.
   
   
   .. api-member::
      :name: [``ssl``]
      :type: (string, optional)
      
      The address of the ssl proxy, can include a port.
   

.. rst-class:: api-main-section

Properties
==========

.. _proxy.settings:

settings
--------

.. api-section-annotation-hack:: 

Configures proxy settings. This setting's value is an object of type ProxyConfig.
