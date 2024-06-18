.. container:: sticky-sidebar

  ≡ geckoProfiler API

  * `Permissions`_
  * `Functions`_
  * `Events`_
  * `Types`_

  .. include:: /overlay/developer-resources.rst

=================
geckoProfiler API
=================

.. role:: permission

.. role:: value

.. role:: code

Exposes the browser's profiler.

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`geckoProfiler`

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`geckoProfiler` is required to use ``messenger.geckoProfiler.*``.

.. rst-class:: api-main-section

Functions
=========

.. _geckoProfiler.dumpProfileToFile:

dumpProfileToFile(fileName)
---------------------------

.. api-section-annotation-hack:: 

Gathers the profile data from the current profiling session, and writes it to disk. The returned promise resolves to a path that locates the created file.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``fileName``
      :type: (string)
      
      The name of the file inside the profile/profiler directory
   

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.getProfile:

getProfile()
------------

.. api-section-annotation-hack:: 

Gathers the profile data from the current profiling session.

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.getProfileAsArrayBuffer:

getProfileAsArrayBuffer()
-------------------------

.. api-section-annotation-hack:: 

Gathers the profile data from the current profiling session. The returned promise resolves to an array buffer that contains a JSON string.

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.getProfileAsGzippedArrayBuffer:

getProfileAsGzippedArrayBuffer()
--------------------------------

.. api-section-annotation-hack:: 

Gathers the profile data from the current profiling session. The returned promise resolves to an array buffer that contains a gzipped JSON string.

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.getSymbols:

getSymbols(debugName, breakpadId)
---------------------------------

.. api-section-annotation-hack:: 

Gets the debug symbols for a particular library.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``debugName``
      :type: (string)
      
      The name of the library's debug file. For example, 'xul.pdb
   
   
   .. api-member::
      :name: ``breakpadId``
      :type: (string)
      
      The Breakpad ID of the library
   

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.pause:

pause()
-------

.. api-section-annotation-hack:: 

Pauses the profiler, keeping any profile data that is already written.

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.resume:

resume()
--------

.. api-section-annotation-hack:: 

Resumes the profiler with the settings that were initially used to start it.

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.start:

start(settings)
---------------

.. api-section-annotation-hack:: 

Starts the profiler with the specified settings.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``settings``
      :type: (object)
      
      .. api-member::
         :name: ``bufferSize``
         :type: (integer)
         
         The maximum size in bytes of the buffer used to store profiling data. A larger value allows capturing a profile that covers a greater amount of time.
      
      
      .. api-member::
         :name: ``features``
         :type: (array of :ref:`geckoProfiler.ProfilerFeature`)
         
         A list of active features for the profiler.
      
      
      .. api-member::
         :name: ``interval``
         :type: (number)
         
         Interval in milliseconds between samples of profiling data. A smaller value will increase the detail of the profiles captured.
      
      
      .. api-member::
         :name: [``threads``]
         :type: (array of string, optional)
         
         A list of thread names for which to capture profiles.
      
      
      .. api-member::
         :name: [``windowLength``]
         :type: (number, optional)
         
         The length of the window of time that's kept in the buffer. Any collected samples are discarded as soon as they are older than the number of seconds specified in this setting. Zero means no duration restriction.
      
   

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. _geckoProfiler.stop:

stop()
------

.. api-section-annotation-hack:: 

Stops the profiler and discards any captured profile data.

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. rst-class:: api-main-section

Events
======

.. _geckoProfiler.onRunning:

onRunning
---------

.. api-section-annotation-hack:: 

Fires when the profiler starts/stops running.

.. api-header::
   :label: Parameters for onRunning.addListener(listener)

   
   .. api-member::
      :name: ``listener(isRunning)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``isRunning``
      :type: (boolean)
      
      Whether the profiler is running or not. Pausing the profiler will not affect this value.
   

.. api-header::
   :label: Required permissions

   - :permission:`geckoProfiler`

.. rst-class:: api-main-section

Types
=====

.. _geckoProfiler.ProfilerFeature:

ProfilerFeature
---------------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`java`
         
         .. api-member::
            :name: :value:`js`
         
         .. api-member::
            :name: :value:`mainthreadio`
         
         .. api-member::
            :name: :value:`fileio`
         
         .. api-member::
            :name: :value:`fileioall`
         
         .. api-member::
            :name: :value:`nomarkerstacks`
         
         .. api-member::
            :name: :value:`screenshots`
         
         .. api-member::
            :name: :value:`seqstyle`
         
         .. api-member::
            :name: :value:`stackwalk`
         
         .. api-member::
            :name: :value:`jsallocations`
         
         .. api-member::
            :name: :value:`nostacksampling`
         
         .. api-member::
            :name: :value:`nativeallocations`
         
         .. api-member::
            :name: :value:`ipcmessages`
         
         .. api-member::
            :name: :value:`audiocallbacktracing`
         
         .. api-member::
            :name: :value:`cpu`
         
         .. api-member::
            :name: :value:`notimerresolutionchange`
         
         .. api-member::
            :name: :value:`cpuallthreads`
         
         .. api-member::
            :name: :value:`samplingallthreads`
         
         .. api-member::
            :name: :value:`markersallthreads`
         
         .. api-member::
            :name: :value:`unregisteredthreads`
         
         .. api-member::
            :name: :value:`processcpu`
         
         .. api-member::
            :name: :value:`power`
         
         .. api-member::
            :name: :value:`responsiveness`
         
         .. api-member::
            :name: :value:`cpufreq`
         
         .. api-member::
            :name: :value:`bandwidth`
         
         .. api-member::
            :name: :value:`memory`
   

.. _geckoProfiler.supports:

supports
--------

.. api-section-annotation-hack:: 

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: :value:`windowLength`
   
