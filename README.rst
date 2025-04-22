|Build| |Group| |PyVersion| |Status| |PyPiVersion| |License| |Docs|

IBKR_Trading_API
------------


The goal of the IB-insync library is to make working with the
`Trader Workstation API <http://interactivebrokers.github.io/tws-api/>`_
from Interactive Brokers as easy as possible.

The main features are:

* An easy to use linear style of programming;
* An `IB component <https://ib-insync.readthedocs.io/api.html#module-ib_insync.ib>`_
  that automatically keeps in sync with the TWS or IB Gateway application;
* A fully asynchonous framework based on
  `asyncio <https://docs.python.org/3/library/asyncio.html>`_
  and
  `eventkit <https://github.com/erdewit/eventkit>`_
  for advanced users;
* Interactive operation with live data in Jupyter notebooks.

Be sure to take a look at the
`notebooks <https://ib-insync.readthedocs.io/notebooks.html>`_,
the `recipes <https://ib-insync.readthedocs.io/recipes.html>`_
and the `API docs <https://ib-insync.readthedocs.io/api.html>`_.

Spoof detector
------------
Visualizes the bid and ask orders and sales in single window with different type of charts. Run `python spoof_detector/spoof_detector.py --help`. You will see all the options

![alt text](docs/lineplot.png)

![alt text](docs/heatmap.png)

Installation
------------

::

    pip install ib_insync

Requirements:

* Python 3.6 or higher;
* A running TWS or IB Gateway application (version 1023 or higher).
  Make sure the
  `API port is enabled <https://interactivebrokers.github.io/tws-api/initial_setup.html>`_
  and 'Download open orders on connection' is checked.

The ibapi package from IB is not needed.

Example
-------

This is a complete script to download historical data:

.. code-block:: python

    from ib_insync import *
    # util.startLoop()  # uncomment this line when in a notebook

    ib = IB()
    ib.connect('127.0.0.1', 7497, clientId=1)

    contract = Forex('EURUSD')
    bars = ib.reqHistoricalData(
        contract, endDateTime='', durationStr='30 D',
        barSizeSetting='1 hour', whatToShow='MIDPOINT', useRTH=True)

    # convert to pandas dataframe (pandas needs to be installed):
    df = util.df(bars)
    print(df)

Output::

                       date      open      high       low     close  volume  \
    0   2019-11-19 23:15:00  1.107875  1.108050  1.107725  1.107825      -1
    1   2019-11-20 00:00:00  1.107825  1.107925  1.107675  1.107825      -1
    2   2019-11-20 01:00:00  1.107825  1.107975  1.107675  1.107875      -1
    3   2019-11-20 02:00:00  1.107875  1.107975  1.107025  1.107225      -1
    4   2019-11-20 03:00:00  1.107225  1.107725  1.107025  1.107525      -1
    ..                  ...       ...       ...       ...       ...     ...
    705 2020-01-02 14:00:00  1.119325  1.119675  1.119075  1.119225      -1


Documentation
-------------

The complete `API documentation <https://ib-insync.readthedocs.io/api.html>`_.

`Changelog <https://ib-insync.readthedocs.io/changelog.html>`_.


