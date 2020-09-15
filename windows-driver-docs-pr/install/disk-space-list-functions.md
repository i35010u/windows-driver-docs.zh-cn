---
title: 磁盘空间列表函数
description: 磁盘空间列表函数
ms.assetid: 850e9f41-b534-49f3-891d-c12c1126e52f
keywords:
- Setupapi.log 函数 WDK，磁盘空间列表
- 磁盘空间列表 WDK Setupapi.log
- 计算磁盘空间 WDK Setupapi.log
- 空间计算 WDK Setupapi.log
- 磁盘空间计算 WDK Setupapi.log
- 总磁盘空间计算 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5a22a042b31c0166d5f27aa6240bcdc3a7312a3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103064"
---
# <a name="disk-space-list-functions"></a>磁盘空间列表函数





磁盘空间列表函数用于创建和修改磁盘空间列表。 这些列表可用于计算处理将在安装过程中复制或删除的文件所需的总磁盘空间。

下表列出了可用于操作磁盘空间列表的函数。 有关详细的函数说明，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupaddinstallsectiontodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddInstallSectionToDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupaddinstallsectiontodiskspacelista)"><strong>SetupAddInstallSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>搜索 INF 文件的<em>DDInstall</em>部分中的<strong>CopyFile</strong>和<strong>DelFile</strong>指令，然后将这些部分中指定的文件操作添加到磁盘空间列表中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupaddsectiontodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddSectionToDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupaddsectiontodiskspacelista)"><strong>SetupAddSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>添加到磁盘空间列表 INF 文件的指定部分中列出的所有文件复制或删除操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupaddtodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddToDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupaddtodiskspacelista)"><strong>SetupAddToDiskSpaceList</strong></a></p></td>
<td align="left"><p>向磁盘空间列表添加单个删除或复制操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupcreatediskspacelista" data-raw-source="[&lt;strong&gt;SetupCreateDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupcreatediskspacelista)"><strong>SetupCreateDiskSpaceList</strong></a></p></td>
<td align="left"><p>创建磁盘空间列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupdestroydiskspacelist" data-raw-source="[&lt;strong&gt;SetupDestroyDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupdestroydiskspacelist)"><strong>SetupDestroyDiskSpaceList</strong></a></p></td>
<td align="left"><p>销毁磁盘空间列表并释放分配给它的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupquerydrivesindiskspacelista" data-raw-source="[&lt;strong&gt;SetupQueryDrivesInDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupquerydrivesindiskspacelista)"><strong>SetupQueryDrivesInDiskSpaceList</strong></a></p></td>
<td align="left"><p>使用 "磁盘空间" 列表中列出的文件操作所引用的驱动器列表填充调用方提供的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupqueryspacerequiredondrivea" data-raw-source="[&lt;strong&gt;SetupQuerySpaceRequiredOnDrive&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupqueryspacerequiredondrivea)"><strong>SetupQuerySpaceRequiredOnDrive</strong></a></p></td>
<td align="left"><p>检查磁盘空间列表以确定执行为特定驱动器列出的所有文件操作所需的空间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupremovefromdiskspacelista" data-raw-source="[&lt;strong&gt;SetupRemoveFromDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupremovefromdiskspacelista)"><strong>SetupRemoveFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>从磁盘空间列表中删除文件复制或删除操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupremoveinstallsectionfromdiskspacelista" data-raw-source="[&lt;strong&gt;SetupRemoveInstallSectionFromDiskSpaceList&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupremoveinstallsectionfromdiskspacelista)"><strong>SetupRemoveInstallSectionFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>搜索 INF 文件的<em>DDInstall</em>部分中的<strong>CopyFiles</strong>和<strong>DelFiles</strong>指令，并从磁盘空间列表中删除这些部分中指定的文件操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetupRemoveSectionFromDiskSpaceList</strong></p></td>
<td align="left"><p>从磁盘空间列表中删除 INF 文件的指定部分中列出的文件复制或删除操作。</p></td>
</tr>
</tbody>
</table>

 

