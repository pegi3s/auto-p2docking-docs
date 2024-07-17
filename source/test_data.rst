Test data
*********

auto-p2docking includes several test data sets (protocols) that can be used as inspiration for developing a pipeline as well as learning how to use a given module. A graphical representation of the pipeline, run times, as well as the output generated when using such pipeline are also provided. Instructions on how to run these protocols are provided on the README.md file. In order to see the available protocols create a config and declare the 'dir' and ' project' variables
To run them, just follow the instructions that are given on the ``README.txt`` file for each test case. 

Specially, take care of the fact that the ``config`` file should be edited to put into ``dir`` the actual path to the test data directory in your computer.


Modules used
------------

The following table summarizes the modules used in each test.

.. csv-table::
   :file: files/modules.csv
   :header-rows: 1
   :class: longtable

Running times
-------------

These are the running times for the tests using a high-performance computing server (1TB of RAM with 96 cores, AMD EPYC 7401 24-Core Processor):

- Test 1a: ~ 13 minutes.
- Test 1b: ~45 minutes.
- Test 2a: ~13 minutes.
- Test 2b: 3 minutes.
- Test 2c: ~9.3 hours.
- Test 3a: ~3.8 hours.
- Test 3b: ~50 minutes.
- Test 4: ~6 minutes.
- Test 5: ~17 minutes.
- Test 6: ~1.25 hours
