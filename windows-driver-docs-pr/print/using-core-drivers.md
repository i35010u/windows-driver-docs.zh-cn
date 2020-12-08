---
title: 使用核心驱动程序
description: 使用核心驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76cc8622b28f386b6325e2b49be0437117c833ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835467"
---
# <a name="using-core-drivers"></a>使用核心驱动程序


打印驱动程序编写器可以通过在 INF 的 "模型" 部分中列出核心模型 GUID 并使用 **PackageAware** 和 **CoreDriverSections** 关键字，来使用它们编写的核心驱动程序。

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

 

 




