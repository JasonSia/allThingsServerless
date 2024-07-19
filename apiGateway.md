**Renaming Api Gateway Resource?**
Its not available in the console but can be done with cli

> aws apigateway update-resource --rest-api-id \<rest-api-id \> --resource-id \<resource-id of the resource you want to rename\> --patch-operations op=replace,path=/pathPart,value=\<new name for the resource\>
