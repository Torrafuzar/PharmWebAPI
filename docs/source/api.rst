============
PharmWeb API
============

.. contents::
   :local:

--------------------------------------------------------------------------------------------------------------------------------------------

OverView
----------

.. important:: 
   To get the API swagger documetation, you can go to https://pharmwebapi.azurewebsites.net/index.html

.. attention::
   The Api is protected by a STS/IDP Server ..and requires a toke to gain access.
   
.. image:: Images/ApiSwagger.png

.. info:: API Response Layout
   All responses from the api will be in a standard layout, consistent response format for both successful and error results.
   
.. code-block:: json
    
   {
   "version": "string",
   "statusCode": 0,
   "message": "string",
   "isError": true,
   "responseException": {},
   "result": {}
   }

--------------------------------------------------------------------------------------------------------------------------------------------

Multi-Tenancy (Url routing)
---------------------------
Multi-tenancy architecture helps us to share the resources cost-efficiently and securely in cloud environments where the single instance of the software runs on a server and serves multiple tenants. In which statelessness plays a major role in scaling for millions of concurrent users. Statelessness means that every Http request(API) happens in complete isolation. When the client makes an Http request, it includes all the information necessary for the server to fulfill that request.

Our API can route database persistance in multibile patterns, depending on the needs of the client, database persistance get route by the ``{__tenant__}`` in the url. This value wil be provided on enrolments

  /**Test**/api/v{version}/Test

Our Leganvy progarm Winscripts folloes the Single-tenant pattern, while the API uses Multi-tendant 1 or Multi-tendant 2 as shows below. 

.. image:: Images/Tendancy.png

--------------------------------------------------------------------------------------------------------------------------------------------

Versioning (Url Routing)
------------------------
To manage this complexity, version your API. Versioning helps us to iterate faster when the needed changes are identified in the APIs.

Using the URI is the most straightforward approach (and most commonly used as well) though it does violate the principle that a URI should refer to a unique resource. You are also guaranteed to break client integration when a version is updated.

Versining get routed by url path ``v{version}``

The version need not be numeric, nor specified using the “v[x]” syntax.

  /Test/api/**v1**/Test
  
--------------------------------------------------------------------------------------------------------------------------------------------

Responses
-------------

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



API Calls
---------

.. Info::
   
   Please refer to https://pharmwebapi.azurewebsites.net/index.html for the full APi documentation
   
--------------------------------------------------------------------------------------------------------------------------------------------
   

AutoOrders 
^^^^^^^^^^

``/{__tenant__}/api/v{version}/AutoOrders``

.. admonition:: Info

   **Auto Orders** call creates Orders in pharmweb to be send the a branch for dispesing, an *Autoorder* can be of type
   
AutoOrder Types 

* Script - Used to dispense a normal script on winscripts (OrderType = 0) 
* OrderDirect - Used to send stock orders (OrderType = 1)
* OrderWise - Used to send stock orders (OrderType = 2)
* XProCure - Used to send stock orders (OrderType = 3)
* Orders (WareHouse Order) - Used to send automated orders from a warehouse (OrderType = 4) 
* ERx (WareHouse Order) - Used to send Scriopts to brances for stock control (OrderType = 5)

**Getting Orders**
  Fetching of Orders will only be used by *Winscripts* to :superscript:`Auto Dispense` at the branch.
  
**Adding Orders**
  Adding of orders will create a order depending on the branch to be send to be  :superscript:`Auto Dispense` at each branch.
  
  To create an Order a POST request needs to be made at ``/{__tenant__}/api/v{version}/AutoOrders`` with a *json* body as shown below.
  
  .. code-block:: json

    {
    "branchCode": "1111111",
    "orderName": "RX1", 
    "referenceNo": "1",
    "dateTime": "2022-01-10T12:00:00.000Z",
    "referenceDate": "2022-01-10T12:00:00.000Z",
    "numberOfItems": "2",
    "customerInfo": {
        "branchId": "12345678",
        "firstName": "JACK",
        "surname": "DANIELS",
        "title": "MR",
        "idNumber": "7908125066081",
        "masNumber": "123",
        "mainMemberDepCode": "1",
        "initials": "J",
        "dateAdded": "2022-01-10T12:00:00.000Z",
        "work": "555-5555",
        "home": "666-6666",
        "cellular": "0734571345",
        "eMail": "mrdaniels@jackdanilsupholstry.com",
        "refCode": "123",
        "custMasInfo": {
            "primaryMasNumber": "123",
            "primaryPayCode": "CASH",
            "primaryMasCode": "CAS"
        }
    },
    "orderStatus": "1",
    "orderType": "5",
    "items": [
        {
            "branchStockId": "703987001",
            "cost": "50.00",
            "quantity": "1",
            "retail": "100.00",
            "stockDescription": "ALTOSEC 20MG CAP 28",
            "itemNo": "1",
            "nappiCode": "703987001",
            "dosage": "TDS",
            "ddu": "30",
            "barCode": "",
            "repeats": "6",
            "currRepeat": "1",
            "days": "30"
        },
        {
            "branchStockId": "768375010",
            "cost": "100.00",
            "quantity": "2",
            "retail": "500.00",
            "stockDescription": "ADCO SYNALEVE CAP 100",
            "itemNo": "2",
            "nappiCode": "768375010",
            "dosage": "2 TIMES DAILY",
            "ddu": "TDS",
            "barCode": "",
            "repeats": "12",
            "currRepeat": "1",
            "days": "30"
        }
    ]
}
  
**Required Fields** 

  ``orderName`` **type:** *string* **maxLength:** **100** *minLength:* **0** :subscript:`(Ordername can be anyname as log as its unique with every POST)`
  
  ``referenceNo`` *type:* **string** *maxLength:* **100** *minLength:* **0** :subscript:`(Reference number as unique trasnaction number from the external source)`    

  ``branchCode`` *type:* **string** *maxLength:* **10** *minLength:* **0** :subscript:`(This is a branch ref code, you can get a list for brachces for the API)`     
   
  ``branchId`` *type:* **string** *maxLength:* **100**  :subscript:`(This is a unique customerid from from the external software)`     
   
  ``title`` *type:* **string** *maxLength:* **7**
    
  ``firstName`` *type:* **string** *maxLength:* **7**

  ``surname`` *type:* **string** *maxLength:* **30**

  ``stockDescription`` *type:* **string** *maxLength:* **100**
  
  ``branchstockId`` :subscript:`(This is a unique stockid from from the external software)`     

  ``quantity`` *type:* **number** **

  ``cost`` *type:* **number** *maxLength:* **30**

  ``retail`` *type:* **number** *maxLength:* **30**
  
--------------------------------------------------------------------------------------------------------------------------------------------
 
Branch
^^^^^^

``/{__tenant__}/api/v{version}/Branch``

.. admonition:: Info

   **Branch** Add and register branches, for external users only GET post wil be used to get all branches BranchCode, 
 
.. infomation:: BranchCode

   BranchCode ..is every branch unique indetifier to be used when adding orders ot getting stock for example, this is used to filter the results.

Branch ``GET`` reponse

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
   
Stock
^^^^^

``/{__tenant__}/api/v{version}/Stock``

.. admonition:: Info

   **Stock URL** is used to get and maintain individial stock items, all normal CRUD call can be made for single items.
   
   Please see documetaion @ https://pharmwebapi.azurewebsites.net/index.html

.. infomation:: BranchStockId

   BranchStockId ..is  unique indetifier to be used when adding stock, with all fields supplied on post, it can generate a ID for you, or you can use an external value fot this.

--------------------------------------------------------------------------------------------------------------------------------------------

StockCollection
^^^^^^^^^^^^^^^

``/{__tenant__}/api/v{version}/StockCollectionController``

.. admonition:: Info 

   **StockCollection** Adds and update the stock master list to the DB ....you must use a collection array json to `POST` stock. This opion is the quickest when adding or        updating stock. Max of 500 items must be send at a time. Stock will be added or updated by the API generated `BranchStockID` or external system StockCode

   Please see documetaion @ https://pharmwebapi.azurewebsites.net/index.html

.. infomation:: BranchStockId

   BranchStockId ..is  unique indetifier to be used when adding stock, with all fields supplied on post, it can generate a ID for you, or you can use an external value fot this.
   
Below is a example json `POST` of 2 items, and FrontShop item and Dispensing item.

.. code-block:: json

      [
    {
        "bId": 5,
        "branchStockId": "",
        "sku": "",
        "description": "8TA10 R 10 TELKOM",
        "packSize": 1.0,
        "deptCode": 0,
        "locationCode": 0,
        "taxCode": 15,
        "reOrderLevel": 0.0,
        "maxLevel": 0.0,
        "posRetailForDisp": false,
        "external": "1|8TA10",
        "disProd": false,
        "stockTakeFlag": false,
        "lockDescription": false,
        "lockPackSize": false,
        "excludeRepeats": false,
        "stockPos": {
            "averageCost": 8.43,
            "posRetail": 10.0,
            "promptForDesc": false,
            "maxDiscount": 0.0,
            "noDiscount": false,
            "overideRetail": false,
            "isService": false,
            "loyaltyGroup": 0,
            "stockRep": 0,
            "special": 0,
            "mAmt": 0.0,
            "mPer": 0.0
        },
        "stockPharm": {
            "uniqueCode": "",
            "strength": "",
            "formCode": "",
            "schedule": "",
            "therapeuticClass": "",
            "sepCost": 0.0,
            "retail": 0.0,
            "lastUpdate": "0001-01-01T00:00:00",
            "prevSepCost": 0.0,
            "prevRetail": 0.0,
            "discDateTime": "0001-01-01T00:00:00",
            "stockLinkId": 0,
            "sepLock": false
        },
        "stockCodes": [
            {
                "code": "1|8TA10",
                "barcode": true,
                "search": false,
                "isDeleted": false,
                "gId": 0
            }
        ],
        "gId": 0
    },
    {
        "bId": 1002,
        "branchStockId": "",
        "sku": "",
        "description": "BIOPLUS VIT-ALITY MAGNESIUM EFF 10",
        "packSize": 10.0,
        "deptCode": 0,
        "locationCode": 0,
        "taxCode": 15,
        "reOrderLevel": 0.0,
        "maxLevel": 0.0,
        "uniqueCode": "3002066001",
        "posRetailForDisp": false,
        "external": "LP9002758",
        "disProd": false,
        "stockTakeFlag": false,
        "lockDescription": false,
        "lockPackSize": false,
        "excludeRepeats": false,
        "stockPos": {
            "averageCost": 36.88,
            "posRetail": 65.95,
            "promptForDesc": false,
            "maxDiscount": 0.0,
            "noDiscount": false,
            "overideRetail": false,
            "isService": false,
            "loyaltyGroup": 0,
            "stockRep": 0,
            "special": 0,
            "mAmt": 0.0,
            "mPer": 0.0
        },
        "stockPharm": {
            "uniqueCode": "3002066001",
            "strength": "",
            "formCode": "EFT",
            "schedule": "9",
            "therapeuticClass": "A11 00",
            "sepCost": 46.16,
            "retail": 69.24,
            "nappi": "3002066",
            "lastUpdate": "2022-01-12T11:34:10",
            "prevSepCost": 46.16,
            "prevRetail": 69.24,
            "manCode": "AID",
            "discDateTime": "1899-12-30T00:00:00",
            "stockLinkId": 0,
            "sepLock": false
        },
        "stockCodes": [
            {
                "code": "6009695588125",
                "barcode": true,
                "search": false,
                "isDeleted": false,
                "gId": 0
            }
        ],
        "gId": 0
    }
]

**Required Fields and Infomation** 

  ``bid`` **NotRequired** **type:** *string* **maxLength:** **50** :subscript:`(Bid can be item index count or external system stock id)`

``branchStockId`` **Required** **type:** *string* **maxLength:** **50** :subscript:`(The branchStockId, is the API or db globals stock id, if no BranchStockId is supplied, one will be auto generated by the API, else a unique Id can be supplied by the external system. This ID is requered)`

``packSize`` **Required** **type:** *number* :subscript:`(PackSize is the qty in size of an item, if packsize is unknown, o can be send`

  ``bid`` **NotRequired** **type:** *string* **maxLength:** **50** :subscript:`(Bid can be item index count or external system stock id)`

  ``stockPos``  :subscript:`(Stock pos is an items frontshop values, this can be left emety if no values exist)`

  ``averageCost`` **Required** **type:** *number*  :subscript:`(The frontshop cost of an item)`

  ``posRetail`` **Required** **type:** *number*  :subscript:`(The frontshop retail of an item)`

  ``stockPharm``  :subscript:`(Items dispensing values)`

  ``uniqueCode`` **Required** **type:** *string* **maxLength:** **16** :subscript:`(RSA unique identifier for dispensing items)`

  ``strength`` **Required** **type:** *string* **maxLength:** **8** :subscript:`(Dispensing items strength)`

  ``formCode`` **Required** **type:** *string* **maxLength:** **5** :subscript:`(Format of the dispansing item like, CAP for capsules and TAB for tablets)`

  ``schedule`` **Required** **type:** *string* **maxLength:** **1** :subscript:`(Dispensing schedule indicator)`

  ``therapeuticClass`` **Required** **type:** *string* **maxLength:** **6** :subscript:`(Supplied by external system, value can be blank)`

  ``sepCost`` **Required** **type:** *number*  :subscript:`(Single exist price of dispensing items, use the determine pricing when dispesning a script)`

  ``stockcodes``  :subscript:`(An array of barcodes, supplied by external system, and item can have multibile barcodes, this tag can be left blank if no values is supplied)`
  
  ``stockCodes.branchStockId`` **Required** **type:** *string* **maxLength:** **50** :subscript:`(The branchStockId, is the API or db globals stock id, if no BranchStockId is supplied, one will be auto generated by the API, else a unique Id can be supplied by the external system. This ID is requered)`

  ``code`` **Required** **type:** *string* **maxLength:** **20** :subscript:`(Frontshop barcode, as supplied by external system)`

  

--------------------------------------------------------------------------------------------------------------------------------------------
   
   

   
