.. container:: sticky-sidebar

  ≡ experiments API

  * `Manifest file properties`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

===============
experiments API
===============

.. role:: permission

.. role:: value

.. role:: code

.. rst-class:: api-main-section

Manifest file properties
========================

.. api-member::
   :name: [``experiment_apis``]
   :type: (object, optional)

.. rst-class:: api-main-section

Types
=====

.. _experiments.APIChildScope:

APIChildScope
-------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`addon_child`
         
         .. api-member::
            :name: :value:`content_child`
         
         .. api-member::
            :name: :value:`devtools_child`
   

.. _experiments.APIEvent:

APIEvent
--------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`startup`
   

.. _experiments.APIEvents:

APIEvents
---------

.. api-section-annotation-hack:: 

.. api-header::
   :label: array of :ref:`experiments.APIEvent`

.. _experiments.APIParentScope:

APIParentScope
--------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`addon_parent`
         
         .. api-member::
            :name: :value:`content_parent`
         
         .. api-member::
            :name: :value:`devtools_parent`
   

.. _experiments.APIPath:

APIPath
-------

.. api-section-annotation-hack:: 

.. api-header::
   :label: array of string

.. _experiments.APIPaths:

APIPaths
--------

.. api-section-annotation-hack:: 

.. api-header::
   :label: array of :ref:`experiments.APIPath`

.. _experiments.ExperimentAPI:

ExperimentAPI
-------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``schema``
      :type: (:ref:`experiments.ExperimentURL`)
   
   
   .. api-member::
      :name: [``child``]
      :type: (object, optional)
      
      .. api-member::
         :name: ``paths``
         :type: (:ref:`experiments.APIPaths`)
      
      
      .. api-member::
         :name: ``scopes``
         :type: (array of :ref:`experiments.APIChildScope`)
      
      
      .. api-member::
         :name: ``script``
         :type: (:ref:`experiments.ExperimentURL`)
      
   
   
   .. api-member::
      :name: [``parent``]
      :type: (object, optional)
      
      .. api-member::
         :name: ``script``
         :type: (:ref:`experiments.ExperimentURL`)
      
      
      .. api-member::
         :name: [``events``]
         :type: (:ref:`experiments.APIEvents`, optional)
      
      
      .. api-member::
         :name: [``paths``]
         :type: (:ref:`experiments.APIPaths`, optional)
      
      
      .. api-member::
         :name: [``scopes``]
         :type: (array of :ref:`experiments.APIParentScope`, optional)
      
   

.. _experiments.ExperimentURL:

ExperimentURL
-------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: string
