---
title: 不共享文件的包感知打印驱动程序
description: 不共享文件的包感知打印驱动程序
ms.assetid: cd114766-37f4-43b5-8e2a-d85f95c973ab
keywords:
- 识别包的打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b76f1947ae78a9c321fe66068bf870900002489
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547813"
---
# <a name="package-aware-print-drivers-that-do-not-share-files"></a>不共享文件的包感知打印驱动程序


如果驱动程序包中的文件有唯一的名称，不会以任何其他驱动程序包将 PrinterPackageInstallation 部分添加到 INF 文件。 在该部分中，添加**PackageAware**= TRUE 关键字，如下面的示例的第 23 行中所示：

```cpp
[Version]
Signature="$Windows NT$"
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer
Provider="OEM Company"
CatalogFile=PackageAware.cat     ; Single Catalog file for all OS versions
DriverVer=10/10/2005, 1.2.3.4

[Manufacturer]
"OEM Company" = Company, NTx86.6.0

;Models section for installation of x86 driver on 
; Windows Vista and later
[Company.NTx86.6.0]
"My Device Description"  
   = DriverInstall_Vista, OEM_Company_NameABC_640A

[DriverInstall_Vista]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD

[PrinterPackageInstallation.x86]
PackageAware=TRUE

; Source Media Information Sections
[DestinationDirs]
DefaultDestDir=66000

[SourceDisksNames.x86]
1   = %MediaDescription%,,,"I386"

[SourceDisksFiles]
OEMRES.DLL  = 1
OEMABC.GPD  = 1
OEMCORE.DLL = 1

[Strings]
MediaDescription = "Description for Vendor provided media"
```

 

 




