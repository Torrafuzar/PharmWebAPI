Branch Register Process
=======================

.. warning:: 
   Please note the only a easyrx technicial can use this process as a normal user wil not be able to log in


.. autosummary::
   :toctree: Before using the migration client each brach needs to be registerd.
   
   A global user needs to be added for each branch to start the register process.
   
| **Registering a global branch user**

| Go to our IDP https://easyrxpharmwebxsts.azurewebsites.net/ and login using your login details.

| Then goto Identity Server Admin, and then to Users and add new user.
| Username must be the branch RAMS number, Password must be the password of the local db located in the Pword file.
| User Phone Number Confirmed must be checked;
| User Lockout Enabled must be checked;
| Roles must be set to Administrator and Owner;

.. note:: Role Administartor must only be specified for the registering process, when the brach has been registerd, Admin role must be taken off.

| Log-out and log in again using the details specified, to TEST if infomation has bee added corecctly, if loged in, allow all grants to give acces to the global user.
| Log-out and start the migration process to register the branch, if infomation has not been added corectly, invalid grad wil be shows as an error.
| ** Log in again and remove the Administartor role for the global braach user you have added


   

   

