##### Function : Administration Process
##### ADMINReqDeleteInNAB - Create a "Delete in Address Book" request.
---
```
#include <adminp.h>
STATUS LNPUBLIC ADMINReqDeleteInNAB(

	DBHANDLE  dbhAdmin4,
	char far *chAuthor,
	char far *chUserName,
	char far *chMailServerName,
	char far *chMailFileName,
	char far *chDeleteMailFile,
	ADMINReqParams far *arpAdminReqParamsPtr,
	WORD  wAdminReqParamsSize);
```
**Description :**

This function creates a "Delete in Address Book" request in the Administration 
Requests database (admin4.nsf).

**Parameters :**
Input :
dbhAdmin4  -  Handle of the Administration Request database (admin4.nsf) that is the destination of the created Admin Request note.

chAuthor  -  A pointer to the Author's name (hierarchical names MUST be in canonical format).

chUserName  -  A pointer to the User's name being deleted (hierarchical names MUST be in canonical format).

chMailServerName  -  A pointer to the Mail Server name (hierarchical names MUST be in canonical format).

chMailFileName  -  A pointer to the Mail file name including path relative to the Domino data directory.

chDeleteMailFile  -  A pointer to a string indicating whether to delete the mail file:

          "0" = Don't delete mail file
          "1" = Delete just mail file specified in person record
          "2" = Delete mail file specified in person record & all replicas

wAdminReqParamsSize  -  Size of the buffer (ADMINReqParams structure) that the arpAdminReqParamsPtr parameter points to.

Output :
(routine)  -  Return status of the call - indicates either success or what the error is.

NOERROR

ERR_xxx - Error returned by lower level functions. Call OSLoadString to interpret code.


arpAdminReqParamsPtr  -  Pointer to an ADMINReqParams structure.


**Sample Usage :**
```
if (error = NSFDbOpen (AdminDBPath, &hAdminReq))
{
	return (ERR(error));
}

if (error = ADMINReqDeleteInNAB (
	hAdminReq,
 "CN=Alan Admin/O=Org",
	"CN=Joe User/O=Org",
 MAIL_SRVR,
 MAIL_FILE,
 "1",
 &ARPptr,
 sizeof(ARPptr)) )
{
	error = NSFDbClose (hAdminReq);
 return (ERR(error));
}
```
**See Also :**
[ADMINReqChkAccessMoveReplica](/domino-c-api-docs/reference/Func/ADMINReqChkAccessMoveReplica)
[ADMINReqChkAccessNewReplica](/domino-c-api-docs/reference/Func/ADMINReqChkAccessNewReplica)
[ADMINReqDeleteInACL](/domino-c-api-docs/reference/Func/ADMINReqDeleteInACL)
[ADMINReqMoveComplete](/domino-c-api-docs/reference/Func/ADMINReqMoveComplete)
[ADMINReqMoveUserInHier](/domino-c-api-docs/reference/Func/ADMINReqMoveUserInHier)
[ADMINReqParams](/domino-c-api-docs/reference/Data/ADMINReqParams)
[ADMINReqRecertify](/domino-c-api-docs/reference/Func/ADMINReqRecertify)
[ADMINReqRename](/domino-c-api-docs/reference/Func/ADMINReqRename)
---
