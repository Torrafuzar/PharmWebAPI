Branch Register Process
=======================

.. warning:: 
   Please note the only a easyrx technicial can use this process as a normal user wil not be able to log in



.. autosummary::
   :toctree: Before using the migration client each brach needs to be registerd.
   
   A global user needs to be added for each branch to start the register process.
   
| **Registering a global brach user** 
| Go to our IDP https://easyrxpharmwebxsts.azurewebsites.net/ and login using your login details.
| Then goto Identity Server Admin, and then to Users and add new user.
| Username must be the branch RAMS number, Passwors must be the password of the local db located in the Pword file.
| User Phone Number Confirmed must be checked;
| User Lockout Enabled must be checked;
|Roles must be set to Administrator as Owner;

.. note:: Role Administartor must only be specified for the registering process, when the brach has been registerd, Admin role must be taken off.

| Logg-out and log in again using the details specified, to TEST if infomation has bee added corecctly, if loged in, allow all grants to give acces to the global user
   
   

   

