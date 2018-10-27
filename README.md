# GADS_Config_Updater
powershell scripts that aid in fetching & formatting data for updating config file for GADS.

* How to use:

The scripts are written to fetch all attributes of desired name, list them and print them to a file.
The GADS configuration file is in .xml format and thus, creating OU structure from Attributes in Google Gsuite regquires
OU's to be listed in .xml format. one <orgName> for each attribute. Example:
  
            <search>
             <priority>$1</priority>
             <suspended>false</suspended>
             <scope>SUBTREE</scope>
             <orgName>/ADM/OU name here</orgName>
             <filter>(&amp;(objectCategory=person)(objectClass=user)(mail=*DOMAIN.COM*)(physicalDeliveryOfficeName=OU name here))</filter>
            </search>
  
  The scripts create this structure for each attribute automatically and creates a file on desktop containing the structure. 
  This enables the configuration file for GADS to be updated easily.
  
  'GADS_config_update_from_file' takes the data from a text file, presuming the data was already printed out and is available locally.
  'GADS_config_update_from_ad' will query Active Directory in the desired DistinguishedName path given to the variable in the script.
  
  The 'builder' function will then create this structure for every attribute stored in the array, and print the file to the desktop. 
  
  * Prerequisites: 
    if using '..from ad' file:
  
    * ActiveDirectory for powershell enabled in Server Roles
    * You need access to query the LDAP server before the script can access the data. Verify this by logging on to a machine with access
      to Active Directory. Open Powershell and type:
      
        import-activedirectory
        $scope = 'Write your base DN where you want to find attributes here. eg: OU=something,OU=something,DC=something,DC=something'
        get-aduser -filter * -searchbase = $scope
   
    if this worked: you have access. 
    
   
