.. container:: sticky-sidebar

  ≡ privacy.network API

  * `Permissions`_
  * `Types`_
  * `Properties`_

  .. include:: /overlay/developer-resources.rst

===================
privacy.network API
===================

.. role:: permission

.. role:: value

.. role:: code

Use the :code:`browser.privacy` API to control usage of the features in the browser that can affect a user's privacy.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`privacy`

   Read and modify privacy settings

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`privacy` is required to use ``messenger.privacy.network.*``.

.. rst-class:: api-main-section

Types
=====

.. _privacy.network.HTTPSOnlyModeOption:

HTTPSOnlyModeOption
-------------------

.. api-section-annotation-hack:: 

The mode for https-only mode.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`always`
         
         .. api-member::
            :name: :value:`private_browsing`
         
         .. api-member::
            :name: :value:`never`
   

.. _privacy.network.IPHandlingPolicy:

IPHandlingPolicy
----------------

.. api-section-annotation-hack:: 

The IP handling policy of WebRTC.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`default`
         
         .. api-member::
            :name: :value:`default_public_and_private_interfaces`
         
         .. api-member::
            :name: :value:`default_public_interface_only`
         
         .. api-member::
            :name: :value:`disable_non_proxied_udp`
         
         .. api-member::
            :name: :value:`proxy_only`
   

.. _privacy.network.tlsVersionRestrictionConfig:

tlsVersionRestrictionConfig
---------------------------

.. api-section-annotation-hack:: 

An object which describes TLS minimum and maximum versions.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``maximum``]
      :type: (`string`, optional)
      
      The maximum TLS version supported.
      
      Supported values:
      
      .. api-member::
         :name: :value:`TLSv1`
      
      .. api-member::
         :name: :value:`TLSv1.1`
      
      .. api-member::
         :name: :value:`TLSv1.2`
      
      .. api-member::
         :name: :value:`TLSv1.3`
      
      .. api-member::
         :name: :value:`unknown`
   
   
   .. api-member::
      :name: [``minimum``]
      :type: (`string`, optional)
      
      The minimum TLS version supported.
      
      Supported values:
      
      .. api-member::
         :name: :value:`TLSv1`
      
      .. api-member::
         :name: :value:`TLSv1.1`
      
      .. api-member::
         :name: :value:`TLSv1.2`
      
      .. api-member::
         :name: :value:`TLSv1.3`
      
      .. api-member::
         :name: :value:`unknown`
   

.. rst-class:: api-main-section

Properties
==========

.. _privacy.network.globalPrivacyControl:

globalPrivacyControl
--------------------

.. api-section-annotation-hack:: 

Allow users to query the status of 'Global Privacy Control'. This setting's value is of type boolean, defaulting to :code:`false`.

.. _privacy.network.httpsOnlyMode:

httpsOnlyMode
-------------

.. api-section-annotation-hack:: 

Allow users to query the mode for 'HTTPS-Only Mode'. This setting's value is of type HTTPSOnlyModeOption, defaulting to :code:`never`.

.. _privacy.network.networkPredictionEnabled:

networkPredictionEnabled
------------------------

.. api-section-annotation-hack:: 

If enabled, the browser attempts to speed up your web browsing experience by pre-resolving DNS entries, prerendering sites (:code:`&lt;link rel='prefetch' ...&gt;`), and preemptively opening TCP and SSL connections to servers.  This preference's value is a boolean, defaulting to :code:`true`.

.. _privacy.network.peerConnectionEnabled:

peerConnectionEnabled
---------------------

.. api-section-annotation-hack:: 

Allow users to enable and disable RTCPeerConnections (aka WebRTC).

.. _privacy.network.tlsVersionRestriction:

tlsVersionRestriction
---------------------

.. api-section-annotation-hack:: 

This property controls the minimum and maximum TLS versions. This setting's value is an object of :ref:`tlsVersionRestrictionConfig`.

.. _privacy.network.webRTCIPHandlingPolicy:

webRTCIPHandlingPolicy
----------------------

.. api-section-annotation-hack:: 

Allow users to specify the media performance/privacy tradeoffs which impacts how WebRTC traffic will be routed and how much local address information is exposed. This preference's value is of type IPHandlingPolicy, defaulting to :code:`default`.
