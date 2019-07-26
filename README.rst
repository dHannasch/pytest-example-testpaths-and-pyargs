Example showing the interaction between testpaths and pyargs.

We might expect that if both testpaths and pyargs are set in setup.cfg, then pytest would run tests both from the package specified with pyargs and the directories specified with testpaths, just as it does on the command line.

.. code-block:: bash

  $ pytest --pyargs string testdir1 testdir2
  ======================================================= test session starts ========================================================
  platform linux -- Python 3.7.3, pytest-5.0.1, py-1.8.0, pluggy-0.12.0
  rootdir: /tmp/pytest-example-testpaths-and-pyargs, inifile: setup.cfg
  collected 2 items                                                                                                                  

  testdir1/test_1.py .                                                                                                         [ 50%]
  testdir2/test_2.py .                                                                                                         [100%]

  ===================================================== 2 passed in 0.47 seconds =====================================================

But in fact, when pyargs is specified in the configuration file, testpaths in the same file is completely ignored.

.. code-block:: bash

  $ pytest
  ======================================================= test session starts ========================================================
  platform linux -- Python 3.7.3, pytest-5.0.1, py-1.8.0, pluggy-0.12.0
  rootdir: /tmp/pytest-example-testpaths-and-pyargs, inifile: setup.cfg
  collected 0 items                                                                                                                  

  =================================================== no tests ran in 0.00 seconds ===================================================

Adding directories to addopts instead of testpaths naturally works just like adding them on the command line: in that case, tests are run both from the pyargs package and from the specified directories.

