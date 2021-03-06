---
title: "CreateTempFile Method"
ms.author: solsen
ms.custom: na
ms.date: 11/06/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# CreateTempFile Method
Creates a temporary file. This enables you to save data of any format to a temporary file. This file has a unique name and will be stored in a temporary file folder.

## Syntax
```
[Ok := ]  File.CreateTempFile([Encoding: TextEncoding])
```
> [!NOTE]  
> This method can be invoked without specifying the data type name.  
## Parameters
*File*  
&emsp;Type: [File](file-data-type.md)  
An instance of the [File](file-data-type.md) data type.  

*Encoding*  
&emsp;Type: [TextEncoding](../textencoding/textencoding-option.md)  
  


## Return Value
*Ok*  
&emsp;Type: [Boolean](../boolean/boolean-data-type.md)  
  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Remarks  
 You can use this method together with [NAME Method \(File\)](../../methods/devenv-name-method-file.md) and [CLOSE Method \(File\)](../../methods/devenv-close-method-file.md).  
  
## Example  
 This example creates a temporary file that has the text Hello and then deletes the file by using the File.CLOSE method. This example requires that you create the following variable.  
  
|Variable|DataType|  
|--------------|--------------|  
|FileName|File|  
  
```  
FileName.CREATETEMPFILE;  
FileName.WRITE('Hello');  
FileName.CLOSE;  
```  
  
## See Also
[File Data Type](file-data-type.md)  
[Getting Started with AL](../../devenv-get-started.md)  
[Developing Extensions](../../devenv-dev-overview.md)