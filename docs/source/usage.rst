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

Add the ``IdentityModel`` NuGet package to your client. 
This can be done either via Visual Studio's Nuget Package manager or dotnet CLI::

IdentityModel includes a client library to use with the discovery endpoint. This way you only need to know the base-address of IdentityServer - the actual endpoint addresses can be read from the metadata::

    // discover endpoints from metadata
    var client = new HttpClient();
    var disco = await client.GetDiscoveryDocumentAsync("https://localhost:5001");
    if (disco.IsError)
    {
        Console.WriteLine(disco.Error);
        return;
    }
.. note:: If you get an error connecting it may be that you are running `https` and the development certificate for ``localhost`` is not trusted. You can run ``dotnet dev-certs https --trust`` in order to trust the development certificate. This only needs to be done once.

Next you can use the information from the discovery document to request a token to IdentityServer to access ``api1``::

    // request token
    var tokenResponse = await client.RequestClientCredentialsTokenAsync(new ClientCredentialsTokenRequest
    {
        Address = disco.TokenEndpoint,

        ClientId = "client",
        ClientSecret = "secret",
        Scope = "api1"
    });
    
    if (tokenResponse.IsError)
    {
        Console.WriteLine(tokenResponse.Error);
        return;
    }

    Console.WriteLine(tokenResponse.Json);
