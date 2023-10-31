# -WS_2008_R2_Administration

# -Restore deleted AD object without AD recycle bin active.
This is a standard bash script, you need to run it with root account.

## Context
	- OS : Windows Server 2008 R2 ver.6.1,
 	- Domain : dc=test,dc=com (test.com),
  		- No AD recycle bin actived,
    		- "computertest1" AD object deleted.
      
## Procedure
	- Launch "ldp.exe" with administrator right,
 		- Options -> Controls
   			-> Load Predefined
     		-> Return deleted objects
       		-> Return recycled objects
	  
![ALT](/Referentiel/0_ldp options 1.PNG)
  
![ALT](/Referentiel/1_ldp options 2.PNG)

  	- Connection -> Bind
   		-> Launch bind utility with administrator right.

![ALT](/Referentiel/2_ldp bind 1.PNG)

![ALT](/Referentiel/3_ldp bind 2.PNG)

![ALT](/Referentiel/4_ldp bind 3.PNG)

	- View -> Tree
 		-> BaseDN: dc=test,dc=com
   		-> **WARNING : Case sensitive** 

![ALT](/Referentiel/5_ldp view 1.PNG)

![ALT](/Referentiel/6_ldp view 2.PNG)

	- The Active Directory should appear,
 		- Search "CN=Deleted Objects,DC=test,DC=com"
   			-> **WARNING : Case sensitive** 
   		- Search the "computertest1" object
     			-> Right click on the object -> Modify
	
![ALT](/Referentiel/7_ldp ad.PNG)

![ALT](/Referentiel/8_ldp obj.PNG)

	- In the "Edit Entry" board :
 		-> Attribute : isDeleted
   		-> Value : keep empty
     		-> Operation : Delete
       		-> Press "Enter" button

  	- The command should appear in the "Entry List" board
   
   	- In the "Edit Entry" board :
    		-> Attribute : distinguishedName
      		-> Value : cn=computertest1,cn=Computers,dc=test,dc=com
			-> **WARNING : Case sensitive** 
		-> Operation : Replace
  		-> Box checked : Synchronous and Extended
    		-> Press "Enter" button

![ALT](/Referentiel/9_ldp attributs.PNG)

      	- The command should be appear in the "Entry List" board,
       		-> Press "Run" button to restore the object.
      		
![ALT](/Referentiel/10_ldp result.PNG)
