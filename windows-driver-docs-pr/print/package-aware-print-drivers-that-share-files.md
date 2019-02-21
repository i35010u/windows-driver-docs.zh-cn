---
title: 识别包的共享文件的打印驱动程序
description: 识别包的共享文件的打印驱动程序
ms.assetid: dcf4e7b4-f0f4-4644-9f5c-c01c1b6c4221
keywords:
- 识别包的打印驱动程序 WDK
- 核心 WDK 打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e63c3910ee2f3615d5bac7293b4faad227a8b47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521863"
---
# <a name="package-aware-print-drivers-that-share-files"></a>识别包的共享文件的打印驱动程序


如果多个打印驱动程序的包共享的驱动程序文件，必须进行共享的文件隔离到核心驱动程序。 例如，Unidrv 是许多打印驱动程序使用，文件的集合，因此 Unidrv 是核心驱动程序。

Unidrv 打印驱动程序使用需求和包含 INF 文件指令，如适用于 Windows XP 中的 INF 文件的以下部分中所示：

```cpp
[UniDrvInstall]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD
DataSection=UNIDRV_DATA
Include=NTPRINT.INF
Needs=UNIDRV.OEM,TTFSUB.OEM
```

在 Windows Vista 中，识别包的驱动程序应使用新**CoreDriverSections**关键字时引用 Unidrv 文件，如适用于 Windows Vista 中的 INF 文件的以下部分中所示：

```cpp
[UniDrvInstall_Vista]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD
CoreDriverSections="{D20EA372-DD35-4950-9ED8-A6335AFE79F0}, 
 UNIDRV.OEM, UNIDRV_DATA, TTFSUB.OEM"
```

在 Windows Vista 中，对 Ntprint.inf 引用不再需要因为 Unidrv 打包为核心驱动程序，并由其全局唯一标识符 (GUID)。 当使用核心驱动程序，不要使用**DataSection**关键字，而是请参阅此部分中，但**CoreDriverSections**关键字。

下表中列出了核心打印包文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>核心文件</th>
<th>GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UNIDRV</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F0}</p></td>
</tr>
<tr class="even">
<td><p>PSCRIPT</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F1}</p></td>
</tr>
<tr class="odd">
<td><p>PCLXL</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F2}</p></td>
</tr>
<tr class="even">
<td><p>绘图器</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F4}</p></td>
</tr>
<tr class="odd">
<td><p>XPSDRV</p></td>
<td><p>{D20EA372-DD35-4950-9ED8-A6335AFE79F5}</p></td>
</tr>
</tbody>
</table>

 

可以引用多个核心驱动程序部分;例如：

```cpp
CoreDriverSections="{GUID1}, SectionName1, SectionName2", "{GUID2}, SectionName3"
```

在安装的驱动程序，取决于核心驱动程序时，打印的安装程序将查找该驱动程序存储区中的核心驱动程序的最新版本，并将安装最新版本。

本部分包括以下主题：

[编写核心驱动程序](writing-core-drivers.md)

[使用核心驱动程序](using-core-drivers.md)

[核心驱动程序示例](core-driver-sample.md)

 

 




