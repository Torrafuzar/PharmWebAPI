============
API Responses
============

.. contents::
   :local:

--------------------------------------------------------------------------------------------------------------------------------------------

OverView
----------

.. important:: 
   To get the API swagger documetation, you can go to https://pharmwebapi.azurewebsites.net/index.html
   
**PharmWeb** uses a simple, yet customizable global HTTP response and exception layput. All incoming HTTP requests wraps responses with a consistent response format for both successful and error results. The goal is to let you focus on your business code specific requirements. This enforcing a standard for all HTTP responses.   
   
--------------------------------------------------------------------------------------------------------------------------------------------

Responses
----------

Successful Reponse
^^^^^^^^^^^^^^^^^^

.. admonition:: Example of a Successful response

   Below is a example of the Successful ``Paging`` response for the ``/{__tenant__}/api/v{version}/Branch`` endpoint. 
   
Response Template

.. code-block:: console

    {
     "version": "string",
     "statusCode": 0,
     "message": "string",
     "isError": true,
     "responseException": {},
     "result": {}
    }
   
Successful Response Branches

.. code-block:: json

    {
    "message": "GET Request successful.",
    "result": {
        "page": 1,
        "pageSize": 50,
        "totalCount": 16,
        "data": [
            {
                "branchCode": "3333333",
                "title": "TESTING",
                "ownerUserId": "08d9d1d3-14f5-4ffa-815f-eb80fbb4da9b",
                "branchName": "TESTING",
                "addr1": "TESTING ADDRESS 1",
                "addr2": "TESTING ADDRESS 2",
                "addr3": "TESTING ADDRESS 3",
                "created": "2022-01-07T11:44:38.152981",
                "isActive": false
            }
        ]
    }

--------------------------------------------------------------------------------------------------------------------------------------------

Error Reponse
^^^^^^^^^^^^^^^^^^

.. admonition:: Example of a Error response

   Below is a example of the Error reponse  
   

Response Template

.. code-block:: console

  {
     "isError": "bool",
     "type": "string",
     "title": "string",
     "status": 0,
     "detail": "string",
     "instance": "string",
     "additionalProp1": {},
     "additionalProp2": {},
     "additionalProp3": {}
   }
   

Error Response (AutoOrder call with invalid info supplied)

.. code-block:: json

    {
       "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
       "title": "Bad Request",
       "status": 400,
       "traceId": "|d98118b0-4363e2c61f1eb2a3."
    }

Error Response (Branches call with invalid tendant info)

.. code-block:: json
    
    {
       "isError": true,
       "type": "https://httpstatuses.com/500",
       "title": "Internal Server Error",
       "status": 500,
       "detail": "Unknown database 'erx'",
       "instance": "/ErxTes/api/v1/Branch",
       "extensions": {}
    }

