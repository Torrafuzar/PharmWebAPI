API
===

.. note:: To get the API swagger documetation, you can go to https://pharmwebapi.azurewebsites.net/index.html

.. important::
   https://pharmwebapi.azurewebsites.net/index.html


.. autosummary::
   :toctree: The Api is protected by a STS/IDP Server ..and requires a toke to gain access.

   lumache

.. image:: Images/ApiSwagger.png

URL Multi-Tenancy
^^^^^^^^^^^^^^^^^
Multi-tenancy architecture helps us to share the resources cost-efficiently and securely in cloud environments where the single instance of the software runs on a server and serves multiple tenants. In which statelessness plays a major role in scaling for millions of concurrent users. Statelessness means that every Http request(API) happens in complete isolation. When the client makes an Http request, it includes all the information necessary for the server to fulfill that request.

Our API can route database persistance in multibile patterns, depending on the needs of the client, database persistance get route by the ``{__tenant__}`` in the url. This value wil be provided on enrolments

.. code-block:: console

  /``Test``/api/v{version}/AutoOrders

Our Leganvy progarm Winscripts folloes the Single-tenant pattern, while the API uses Multi-tendant 1 or Multi-tendant 2 as shows below. 

.. image:: Images/Tendancy.png

URI Versioning
^^^^^^^^^^^^^^
To manage this complexity, version your API. Versioning helps us to iterate faster when the needed changes are identified in the APIs.

Using the URI is the most straightforward approach (and most commonly used as well) though it does violate the principle that a URI should refer to a unique resource. You are also guaranteed to break client integration when a version is updated.

The version need not be numeric, nor specified using the “v[x]” syntax.

.. code-block:: console

  /Test/api/v{version}/AutoOrders


AutoOrders
^^^^^^^^^^
.. seealso::

   Module :py:mod:`zipfile`
      Documentation of the :py:mod:`zipfile` standard module.

   `GNU tar manual, Basic Tar Format <http://link>`_
      Documentation for tar archive files, including GNU tar extensions.

.. code-block:: python
   :caption: this.py
   :name: this-py

   print 'Explicit is better than implicit.'
