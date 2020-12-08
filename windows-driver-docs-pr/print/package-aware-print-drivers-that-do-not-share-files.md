---
title: 不共享文件的包感知打印驱动程序
description: 不共享文件的包感知打印驱动程序
keywords:
- 包感知打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7b958b03ec3215f7868d19ef1c362926509f4ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807665"
---
# <a name="package-aware-print-drivers-that-do-not-share-files"></a>不共享文件的包感知打印驱动程序


当驱动程序包中的文件是唯一命名的，并且不会出现在任何其他驱动程序包中时，请将 PrinterPackageInstallation 节添加到 INF 文件中。 在该部分中，添加 " **PackageAware**= TRUE" 关键字，如以下示例第23行中所示：

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

 

 




