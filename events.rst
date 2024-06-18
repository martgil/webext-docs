.. container:: sticky-sidebar

  ≡ events API

  * `Types`_

  .. include:: /overlay/developer-resources.rst

==========
events API
==========

.. role:: permission

.. role:: value

.. role:: code

The :code:`chrome.events` namespace contains common types used by APIs dispatching events to notify you when something interesting happens.

.. rst-class:: api-main-section

Types
=====

.. _events.Event:

Event
-----

.. api-section-annotation-hack:: 

An object which allows the addition and removal of listeners for a Chrome event.

.. api-header::
   :label: object

   - ``addListener(callback)`` Registers an event listener *callback* to an event.
   - ``addRules(eventName, webViewInstanceId, rules, [callback])`` Registers rules to handle events.
   - ``getRules(eventName, webViewInstanceId, [ruleIdentifiers], callback)`` Returns currently registered rules.
   - ``hasListener(callback)``
   - ``hasListeners()``
   - ``removeListener(callback)`` Deregisters an event listener *callback* from an event.
   - ``removeRules(eventName, webViewInstanceId, [ruleIdentifiers], [callback])`` Unregisters currently registered rules.

.. _events.Rule:

Rule
----

.. api-section-annotation-hack:: 

Description of a declarative rule for handling events.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``actions``
      :type: (array of any)
      
      List of actions that are triggered if one of the condtions is fulfilled.
   
   
   .. api-member::
      :name: ``conditions``
      :type: (array of any)
      
      List of conditions that can trigger the actions.
   
   
   .. api-member::
      :name: [``id``]
      :type: (string, optional)
      
      Optional identifier that allows referencing this rule.
   
   
   .. api-member::
      :name: [``priority``]
      :type: (integer, optional)
      
      Optional priority of this rule. Defaults to 100.
   
   
   .. api-member::
      :name: [``tags``]
      :type: (array of string, optional)
      
      Tags can be used to annotate rules and perform operations on sets of rules.
   

.. _events.UrlFilter:

UrlFilter
---------

.. api-section-annotation-hack:: 

Filters URLs for various criteria. See <a href='events#filtered'>event filtering</a>. All criteria are case sensitive.

.. api-header::
   :label: object

   
   .. api-member::
      :name: [``hostContains``]
      :type: (string, optional)
      
      Matches if the host name of the URL contains a specified string. To test whether a host name component has a prefix 'foo', use hostContains: '.foo'. This matches 'www.foobar.com' and 'foo.com', because an implicit dot is added at the beginning of the host name. Similarly, hostContains can be used to match against component suffix ('foo.') and to exactly match against components ('.foo.'). Suffix- and exact-matching for the last components need to be done separately using hostSuffix, because no implicit dot is added at the end of the host name.
   
   
   .. api-member::
      :name: [``hostEquals``]
      :type: (string, optional)
      
      Matches if the host name of the URL is equal to a specified string.
   
   
   .. api-member::
      :name: [``hostPrefix``]
      :type: (string, optional)
      
      Matches if the host name of the URL starts with a specified string.
   
   
   .. api-member::
      :name: [``hostSuffix``]
      :type: (string, optional)
      
      Matches if the host name of the URL ends with a specified string.
   
   
   .. api-member::
      :name: [``originAndPathMatches``]
      :type: (string, optional)
      
      Matches if the URL without query segment and fragment identifier matches a specified regular expression. Port numbers are stripped from the URL if they match the default port number. The regular expressions use the <a href="https://github.com/google/re2/blob/master/doc/syntax.txt">RE2 syntax</a>.
   
   
   .. api-member::
      :name: [``pathContains``]
      :type: (string, optional)
      
      Matches if the path segment of the URL contains a specified string.
   
   
   .. api-member::
      :name: [``pathEquals``]
      :type: (string, optional)
      
      Matches if the path segment of the URL is equal to a specified string.
   
   
   .. api-member::
      :name: [``pathPrefix``]
      :type: (string, optional)
      
      Matches if the path segment of the URL starts with a specified string.
   
   
   .. api-member::
      :name: [``pathSuffix``]
      :type: (string, optional)
      
      Matches if the path segment of the URL ends with a specified string.
   
   
   .. api-member::
      :name: [``ports``]
      :type: (array of integer or array of integer, optional)
      
      Matches if the port of the URL is contained in any of the specified port lists. For example :code:`[80, 443, [1000, 1200]]` matches all requests on port 80, 443 and in the range 1000-1200.
   
   
   .. api-member::
      :name: [``queryContains``]
      :type: (string, optional)
      
      Matches if the query segment of the URL contains a specified string.
   
   
   .. api-member::
      :name: [``queryEquals``]
      :type: (string, optional)
      
      Matches if the query segment of the URL is equal to a specified string.
   
   
   .. api-member::
      :name: [``queryPrefix``]
      :type: (string, optional)
      
      Matches if the query segment of the URL starts with a specified string.
   
   
   .. api-member::
      :name: [``querySuffix``]
      :type: (string, optional)
      
      Matches if the query segment of the URL ends with a specified string.
   
   
   .. api-member::
      :name: [``schemes``]
      :type: (array of string, optional)
      
      Matches if the scheme of the URL is equal to any of the schemes specified in the array.
   
   
   .. api-member::
      :name: [``urlContains``]
      :type: (string, optional)
      
      Matches if the URL (without fragment identifier) contains a specified string. Port numbers are stripped from the URL if they match the default port number.
   
   
   .. api-member::
      :name: [``urlEquals``]
      :type: (string, optional)
      
      Matches if the URL (without fragment identifier) is equal to a specified string. Port numbers are stripped from the URL if they match the default port number.
   
   
   .. api-member::
      :name: [``urlMatches``]
      :type: (string, optional)
      
      Matches if the URL (without fragment identifier) matches a specified regular expression. Port numbers are stripped from the URL if they match the default port number. The regular expressions use the <a href="https://github.com/google/re2/blob/master/doc/syntax.txt">RE2 syntax</a>.
   
   
   .. api-member::
      :name: [``urlPrefix``]
      :type: (string, optional)
      
      Matches if the URL (without fragment identifier) starts with a specified string. Port numbers are stripped from the URL if they match the default port number.
   
   
   .. api-member::
      :name: [``urlSuffix``]
      :type: (string, optional)
      
      Matches if the URL (without fragment identifier) ends with a specified string. Port numbers are stripped from the URL if they match the default port number.
   
