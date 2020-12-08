---
title: 共享文件的包感知打印驱动程序
description: 共享文件的包感知打印驱动程序
keywords:
- 包感知打印驱动程序 WDK
- 核心驱动程序 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bab1462287fb419ae45e69ef86a2c0566e41f4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807661"
---
# <a name="package-aware-print-drivers-that-share-files"></a>共享文件的包感知打印驱动程序


当多个打印驱动程序包共享驱动程序文件时，共享文件必须隔离到核心驱动程序中。 例如，Unidrv 是许多打印驱动程序使用的文件集合，因此 Unidrv 是核心驱动程序。

Unidrv 打印驱动程序使用需要并包括 INF 文件指令，如 Windows XP INF 文件的以下部分所示：

```cpp
[UniDrvInstall]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD
DataSection=UNIDRV_DATA
Include=NTPRINT.INF
Needs=UNIDRV.OEM,TTFSUB.OEM
```

在 Windows Vista 中，在引用 Unidrv 文件时，程序包感知驱动程序应使用 new **CoreDriverSections** 关键字，如适用于 Windows VISTA 的 INF 文件的以下部分所示：

```cpp
[UniDrvInstall_Vista]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD
CoreDriverSections="{D20EA372-DD35-4950-9ED8-A6335AFE79F0}, 
 UNIDRV.OEM, UNIDRV_DATA, TTFSUB.OEM"
```

在 Windows Vista 中，不再需要对 Ntprint.inf 的引用，因为 Unidrv 会打包为核心驱动程序，并由其全局唯一标识符 (GUID) 来引用。 使用核心驱动程序时，请不要使用 **DataSection** 关键字，而是通过 **CoreDriverSections** 关键字引用此部分。

下表列出了核心打印包文件。

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
<td><p>绘图</p></td>
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

安装依赖于核心驱动程序的驱动程序时，打印安装程序将在驱动程序存储区中查找该核心驱动程序的最新版本，并将安装最新版本。

本节包括下列主题：

[编写核心驱动程序](writing-core-drivers.md)

[使用核心驱动程序](using-core-drivers.md)

[核心驱动程序示例](core-driver-sample.md)

 

 




