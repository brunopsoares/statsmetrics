============
StatsMetrics
============

This module contains metrics which you can use to export to analytics apps.

----------

Installation instructions:
--------------------------

Install via ``pip``:

.. code-block::

   $ pip install statsmetrics

*See ``pip`` installation instructions at http://www.pip-installer.org/en/latest/installing.html*

Available metrics:
------------------
 - Couchbase

Usage example:
--------------

.. code-block::

    from statsmetrics import couchbase as couchbasemetrics
    metrics = couchbasemetrics.get_metrics()

Response format:
----------------

.. code-block::

    'cluster': {
      'url': '/pools/default/',
      'metrics': [
          {'name':'storageTotals.ram.total','id':'storageTotals.ram.total','suffix':'bytes','labels':['name']},
          (... other cluster metrics)
      ]
    },
    'nodes': {
      'url': '/pools/nodes/',
      'metrics': [
          {'name':'systemStats.cpu_utilization_rate','id':'systemStats.cpu_utilization_rate','suffix':'count','labels':['name','hostname']},
          (... other nodes metrics)
      ]
    },
      'buckets': {
          'url': '/pools/default/buckets/',
          'metrics': [
              {'name':'basicStats.quotaPercentUsed','id':'basicStats.quotaPercentUsed','suffix':'percent','labels':['name','bucket']},
              (... other buckets metrics),
          ],
          'bucket_stats': [
              {'name':'avg_bg_wait_time','id':'avg_bg_wait_time','suffix':'seconds','labels':['name','bucket']},
              (... other bucket_stats metrics),
          ]
      }
    }


Testing the package:
--------------------

.. code-block::

    $ python test.py


Tips:
-----
Convert returned data to JSON format

.. code-block::

    import json
    from statsmetrics import couchbase as couchbasemetrics
    metrics = couchbasemetrics.get_metrics()
    print json.dumps(metrics, ensure_ascii=False)
