.. container:: sticky-sidebar

  ≡ types API

  * `Types`_

  .. include:: /overlay/developer-resources.rst

=========
types API
=========

.. role:: permission

.. role:: value

.. role:: code

Contains types used by other schemas.

.. rst-class:: api-main-section

Types
=====

.. _types.LevelOfControl:

LevelOfControl
--------------

.. api-section-annotation-hack:: 

One of<ul>

* :value:`not_controllable`: cannot be controlled by any extension</li>

* :value:`controlled_by_other_extensions`: controlled by extensions with higher precedence</li>

* :value:`controllable_by_this_extension`: can be controlled by this extension</li>

* :value:`controlled_by_this_extension`: controlled by this extension</li></ul>

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`not_controllable`
         
         .. api-member::
            :name: :value:`controlled_by_other_extensions`
         
         .. api-member::
            :name: :value:`controllable_by_this_extension`
         
         .. api-member::
            :name: :value:`controlled_by_this_extension`
   

.. _types.Setting:

Setting
-------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   - ``clear(details, [callback])`` Clears the setting, restoring any default value.
   - ``get(details, callback)`` Gets the value of a setting.
   - ``set(details, [callback])`` Sets the value of a setting.

.. _types.SettingScope:

SettingScope
------------

.. api-section-annotation-hack:: 

The scope of the Setting. One of<ul>

* :value:`regular`: setting for the regular profile (which is inherited by the incognito profile if not overridden elsewhere),</li>

* :value:`regular_only`: setting for the regular profile only (not inherited by the incognito profile),</li>

* :value:`incognito_persistent`: setting for the incognito profile that survives browser restarts (overrides regular preferences),</li>

* :value:`incognito_session_only`: setting for the incognito profile that can only be set during an incognito session and is deleted when the incognito session ends (overrides regular and incognito_persistent preferences).</li></ul> Only :value:`regular` is supported by Firefox at this time.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`regular`
         
         .. api-member::
            :name: :value:`regular_only`
         
         .. api-member::
            :name: :value:`incognito_persistent`
         
         .. api-member::
            :name: :value:`incognito_session_only`
   
