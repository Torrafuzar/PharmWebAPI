Usage
=====

.. _Security:

To use PharmWeb API, access must be given URL:
You can view the full swagger documentation of the address below.

.. code-block:: console

   https://pharmwebapi.azurewebsites.net/index.html
   
The API is protected, and uses the OpenID Connect (OIDC) and OAuth 2.0 standards for ASP.NET Core. It's designed to provide a common way to authenticate requests to all of your applications, whether they're web, native, mobile, or API endpoints. 

Gaining Access Token
----------------

To get access to the API, a access token must be requested, calling our STS (Secure Token Server) or IDP (Identity Profider)

.. code-block:: console

  https://easyrxpharmwebxsts.azurewebsites.net

The token endpoint at IdentityServer implements the OAuth 2.0 protocol, and you could use raw HTTP to access it. However, we have a client library called IdentityModel, that encapsulates the protocol interaction in an easy to use API.

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

