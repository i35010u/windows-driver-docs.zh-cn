---
title: 使用核心驱动程序
description: 使用核心驱动程序
ms.assetid: 333f3f17-0cdc-48d3-bb30-f8e2d7216d89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fffa11f020d3233267b23e614e818898019365f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339643"
---
# <a name="using-core-drivers"></a>使用核心驱动程序


打印驱动程序编写人员可以使用通过列出的核心模型的 INF，模型部分中的 GUID 并使用他们所写的核心推动因素**PackageAware**并**CoreDriverSections**关键字。

例如：

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
"My Device Description"  = DriverInstall_Vista, OEM_Company_NameABC_123A
; Core driver definition as discussed in the section Writing Core Drivers
"{GUID1}" = {GUID1}, {GUID1}

[DriverInstall_Vista]
CopyFiles=@file.dll
CoreDriverSections="{D20EA372-DD35-4950-9ED8-A6335AFE79F0},UNIDRV.OEM,UNIDRV_DATA,TTFSUB.OEM", "{GUID1},MANUFACTURER_CORE"
The package install section must also be added, and list all core driver dependencies:
[PrinterPackageInstallation.x86]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0},{GUID1}
```

 

 




