---
title: Using the add-ImageDriverPackages Command
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9dc78909-a4d1-42a2-af8f-21ebcbfe8302
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Using the add-ImageDriverPackages Command

>Applies To: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

adds driver packages from the driver store to a boot image. The image version must be Windows 7 or Windows Server 2008 R2 or later.
for examples of how you can use this command, see [Examples](#BKMK_examples).
## Syntax
```
wdsutil /add-ImageDriverPackages [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} 
[/Filename:<File name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```
## Parameters
|Parameter|Description|
|-------|--------|
|/Server:<Server name>|Specifies the name of the server. This can be the NetBIOS name or the FQDN. If no server name is specified, the local server is used.|
media:<Image name>|Specifies the name of the image to add the driver to.|
mediatype:Boot|Specifies the type of image to add the driver to. Driver packages can be added only to boot images.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Specifies the architecture of the boot image. Because it is possible to have the same image name for boot images in different architectures, you should specify the architecture to ensure the correct image is used.|
|/Filename:<File name>|Specifies the file name. If the image cannot be uniquely identified by name, the file name must be specified.|
|/Filtertype:<Filter type>|Specifies the attribute of the driver package to search for. You can specify multiple attributes in a single command. You must also specify **/Operator** and **/Value** with this option.<br /><br /><Filter type> can be one of the following:<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/Operator:{Equal &#124; NotEqual &#124; GreaterOrEqual &#124; LessOrEqual &#124; Contains}|The relationship between the attribute and the values. You can only specify **Contains** with string attributes. You can only specify **GreaterOrEqual** and **LessOrEqual** with date and version attributes.|
|/Value:<Value>|Specifies the value to search for relative to the specified <attribute>. You can specify multiple values for a single **/Filtertype**. The list below outlines the attributes that you can specify for each filter. For more information about these attributes, see [Driver and Package attributes](http://go.microsoft.com/fwlink/?LinkId=166895) (http://go.microsoft.com/fwlink/?LinkId=166895).<br /><br />-   PackageId - Specify a valid GUID. For example: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-   PackageName   Specify any string value.<br />-   PackageEnabled - Specify **Yes** or **No**.<br />-   Packagedateadded - Specify the date in the following format: YYYY/MM/DD<br />-   PackageInfFilename   Specify any string value.<br />-   PackageClass - Specify a valid class name or class GUID. For example: **DiskDrive**, **Net**, or {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-   PackageProvider   Specify any string value.<br />-   PackageArchitecture - Specify **x86**,  **x64**, or **ia64**.<b />-   PackageLocale - Specify a valid language identifier. For example: **en-US** or **es-ES**.<br />-   PackageSigned - Specify **Yes** or **No**.<br />-   PackagedatePublished - Specify the date in the following format: YYYY/MM/DD<br />-   Packageversion - Specify the version in the following format: a.b.x.y. For example: 6.1.0.0<br />-   Driverdescription   Specify any string value.<br />-   DriverManufacturer   Specify any string value.<br />-   DriverHardwareId - Specify any string value.<br />-   DrivercompatibleId - Specify any string value.<br />-   DriverExcludeId - Specify any string value.<br />-   DriverGroupId - Specify a valid GUID. For example: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-   DriverGroupName   Specify any string value.|
## <a name="BKMK_examples"></a>Examples
To add driver packages to a boot image, type one of the following:
```
wdsutil /add-ImageDriverPackagemedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /Filtertype:DriverGroupName /Operator:Equal /Value:x86Bus /Filtertype:PackageProvider /Operator:Contains /Value:Provider1 /Filtertype:Packageversion /Operator:GreaterOrEqual /Value:6.1.0.0
```
```
wdsutil /verbose /add-ImageDriverPackagemedia: "WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
```
wdsutil /verbose /add-ImageDriverPackagemedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Value:System /Value:DiskDrive /Value:HDC /Value:SCSIAdapter
```
#### additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
[Using the add-ImageDriverPackage Command](using-the-add-imagedriverpackage-command.md)
[Using the add-AllDriverPackages subcommand](using-the-add-alldriverpackages-subcommand.md)
