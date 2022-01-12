API
===

.. note:: To get the API swagger documetation, you can go to https://pharmwebapi.azurewebsites.net/index.html

.. autosummary::
   :toctree: The Api is protected by a STS/IDP Server ..and requires a toke to gain access.

   lumache

.. image:: Images/ApiSwagger.png

Multi-Tenancy
^^^^^^^^^^^^
Multi-tenancy architecture helps us to share the resources cost-efficiently and securely in cloud environments where the single instance of the software runs on a server and serves multiple tenants. In which statelessness plays a major role in scaling for millions of concurrent users. Statelessness means that every Http request(API) happens in complete isolation. When the client makes an Http request, it includes all the information necessary for the server to fulfill that request.



AutoOrders
^^^^^^^^^^
