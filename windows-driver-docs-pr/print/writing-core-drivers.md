---
title: 编写核心驱动程序
description: 编写核心驱动程序
ms.assetid: 3a41a91b-3cc3-462a-8836-448203ccb4c2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3a540cb9c657a470872dd52be14c5b36b8b646
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547293"
---
# <a name="writing-core-drivers"></a>编写核心驱动程序


打印驱动程序编写人员可以使用 Windows Vista 提供了核心驱动程序功能。 若要使核心驱动程序，生成一个可以使用其他驱动程序包来指代构成核心驱动程序的文件集的 GUID。 例如，在 Ntprint.inf，Unidrv 核心驱动程序文件定义显示在下面的示例：

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

使用此定义，打印驱动程序 INF 文件到核心驱动程序文件通过使用可以引用**CoreDriverSections**关键字前面的示例中所示。

请务必注意，核心驱动程序必须保持与早期版本的兼容性。 多个驱动程序可能会使用核心驱动程序，因此它必须继续使用现有的驱动程序更新时，依赖于它。 核心驱动程序必须作为驱动程序包的一部分提供。

核心驱动程序定义模型部分，其中包括设备说明的是核心驱动程序的 GUID。 例如：

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

核心驱动程序必须包括版本信息在安装部分中，通过使用**DriverVer**关键字。 安装部分还必须列出核心驱动程序所需的所有文件。 使用新**AlwaysExcludeFromSelect**关键字，以确保不向用户在 UI 中显示的核心驱动程序。

 

 




