---
title: 编写核心驱动程序
description: 编写核心驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a0d2098101ce4d339d4d9a531f97296eb673889
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785777"
---
# <a name="writing-core-drivers"></a>编写核心驱动程序


打印驱动程序编写器可以使用 Windows Vista 提供的核心驱动程序功能。 若要创建核心驱动程序，请生成一个 GUID，其他驱动程序包可以使用该 GUID 来引用构成核心驱动程序的文件集。 例如，在 Ntprint.inf 中，Unidrv core 驱动程序文件定义如下例所示：

```cpp
[Microsoft.NTx86]
"{D20EA372-DD35-4950-9ED8-A6335AFE79F0}" =  
  {D20EA372-DD35-4950-9ED8-A6335AFE79F0}, 
  {D20EA372-DD35-4950-9ED8-A6335AFE79F0}
[{D20EA372-DD35-4950-9ED8-A6335AFE79F0}]
CopyFiles=UNIDRV,PJLMON.DLL,@TTFSUB.GPD,@LOCALE.GPD,@MSXPSINC.GPD
[UNIDRV]
; Unidrv files and pjlmon sections follow...
```

使用此定义，打印驱动程序 INF 文件可以通过使用 **CoreDriverSections** 关键字（如前面的示例中所示）来引用核心驱动程序文件。

请务必注意，核心驱动程序必须保持与早期版本的兼容性。 因为有多个驱动程序可以使用核心驱动程序，所以它必须继续使用在更新时依赖于它的现有驱动程序。 核心驱动程序必须作为驱动程序包的一部分提供。

核心驱动程序使用模型部分定义，其中包括作为核心驱动程序 GUID 的设备说明。 例如：

```cpp
; Model section
[Company.NTx86]
"{GUID1}" = {GUID1}, {GUID1}

; Install section - must list all files in the core printer driver
[{GUID1}]
DriverVer = MM/DD/YYYY,1.1.1.1
CopyFiles=MANUFACTURER_CORE_FILESET

; Core Driver Section, can use print-specific INF keywords here
[MANUFACTURER_CORE]
CopyFiles=MANUFACTURER_CORE_FILESET

[MANUFACTURER_CORE_FILESET]
File1.dll
File2.dll
File3.dll

[ControlFlags]
AlwaysExcludeFromSelect = {GUID1}
```

核心驱动程序必须在安装部分包含版本信息，方法是使用 **DriverVer** 关键字。 "安装" 部分还必须列出核心驱动程序所需的所有文件。 使用 new **AlwaysExcludeFromSelect** 关键字可确保核心驱动程序不会在用户界面中显示给用户。

 

 




